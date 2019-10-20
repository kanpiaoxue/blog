#java net 编程(Socket,netty)
###发表时间：2013-10-14
###分类：Netty,java,socket
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1956800" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1956800</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>经常要用到网络编程。目前常用的服务器端有的Socket编程，还有NIO编程。</p> 
 <p>针对NIO编程，这里选择了一个成熟的框架Netty来编写服务器端。</p> 
 <p>而Socket的Server端，采用线程池来构造，能满足日常的一般需求。</p> 
 <p>&nbsp;</p> 
 <p>========== netty</p> 
 <p>EchoServer.java</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.net.InetSocketAddress;
import java.util.concurrent.Executors;

import org.apache.log4j.Logger;
import org.jboss.netty.bootstrap.ServerBootstrap;
import org.jboss.netty.channel.ChannelFactory;
import org.jboss.netty.channel.ChannelPipeline;
import org.jboss.netty.channel.ChannelPipelineFactory;
import org.jboss.netty.channel.Channels;
import org.jboss.netty.channel.socket.nio.NioServerSocketChannelFactory;
import org.jboss.netty.handler.codec.frame.DelimiterBasedFrameDecoder;
import org.jboss.netty.handler.codec.frame.Delimiters;
import org.jboss.netty.handler.codec.string.StringDecoder;
import org.jboss.netty.handler.codec.string.StringEncoder;

public class EchoServer {
	private static final Logger LOGGER = Logger.getLogger(EchoServer.class);

	private static final int PORT = 10007;
	private static final String FRAMER = "framer";
	private static final String DECODER = "decoder";
	private static final String ENCODER = "encoder";
	private static final String HANDLER = "handler";

	/**
	 * @param args
	 */
	public static void main(String[] args) {

		LOGGER.info("start netty echo server.");
		ChannelFactory factory = new NioServerSocketChannelFactory(
				Executors.newCachedThreadPool(),
				Executors.newCachedThreadPool());

		ServerBootstrap bootstrap = new ServerBootstrap(factory);

		bootstrap.setPipelineFactory(new ChannelPipelineFactory() {
			public ChannelPipeline getPipeline() {
				ChannelPipeline pipeline = Channels.pipeline();
				pipeline.addLast(FRAMER, new DelimiterBasedFrameDecoder(
						Integer.MAX_VALUE, Delimiters.lineDelimiter()));
				pipeline.addLast(DECODER, new StringDecoder());
				pipeline.addLast(ENCODER, new StringEncoder());
				pipeline.addLast(HANDLER, new EchoServerHandler());
				return pipeline;
			}
		});

		bootstrap.setOption("child.tcpNoDelay", true);
		bootstrap.setOption("child.keepAlive", true);

		bootstrap.bind(new InetSocketAddress(PORT));

	}

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>EchoServerHandler.java</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.util.concurrent.atomic.AtomicInteger;

import org.apache.log4j.Logger;
import org.jboss.netty.buffer.ChannelBuffer;
import org.jboss.netty.buffer.ChannelBuffers;
import org.jboss.netty.channel.Channel;
import org.jboss.netty.channel.ChannelHandlerContext;
import org.jboss.netty.channel.ChannelStateEvent;
import org.jboss.netty.channel.ExceptionEvent;
import org.jboss.netty.channel.MessageEvent;
import org.jboss.netty.channel.SimpleChannelHandler;

import com.alibaba.fastjson.JSON;

public class EchoServerHandler extends SimpleChannelHandler {
	private static final Logger LOGGER = Logger.getLogger(EchoServer.class);

	private static final AtomicInteger COUNT = new AtomicInteger();

	@Override
	public void messageReceived(ChannelHandlerContext ctx, MessageEvent e) {
		String inputString = (String) e.getMessage();

		try {
			TransportMessage request = JSON.parseObject(inputString,
					TransportMessage.class);

			String response = null;
			if (request.getCode() % 2 == 0) {
				response = JSON.toJSONString(new TransportMessage(7100,
						"request.getState()%2 == 0" + request.getContent()));
			} else {
				response = JSON.toJSONString(new TransportMessage(8100, request
						.getContent()));
			}

			Channel channel = e.getChannel();

			byte[] arr = new StringBuilder(response).append("\tcount:")
					.append(COUNT.getAndIncrement()).append("\n").toString()
					.getBytes();
			ChannelBuffer word = ChannelBuffers.buffer(arr.length);
			word.writeBytes(arr);
			channel.write(word);
			if (LOGGER.isDebugEnabled()) {
				LOGGER.debug(Thread.currentThread().getName() + ":"
						+ e.getRemoteAddress() + " receives message : "
						+ inputString + " -- send message : " + response);
			}
			
			System.out.println(Thread.currentThread().getName() + ":"
						+ e.getRemoteAddress() + " receives message : "
						+ inputString + " -- send message : " + response);
			
		} catch (Exception e1) {
			LOGGER.error("Error:" + e.getMessage(), e1);
		}
	}

	@Override
	public void channelConnected(ChannelHandlerContext ctx, ChannelStateEvent e)
			throws Exception {
		ctx.sendUpstream(e);
	}

	@Override
	public void channelClosed(ChannelHandlerContext ctx, ChannelStateEvent e)
			throws Exception {
		ctx.sendUpstream(e);
	}

	@Override
	public void exceptionCaught(ChannelHandlerContext ctx, ExceptionEvent e) {
		LOGGER.error("Error:" + e.getCause().getMessage(), e.getCause());
		Channel ch = e.getChannel();
		ch.close();
	}
}</pre> 
 <p>&nbsp;</p> 
 <p>TransportMessage.java</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class TransportMessage {
	private int code;
	private String content;

	public TransportMessage(int code, String content) {
		super();
		this.code = code;
		this.content = content;
	}

	public TransportMessage() {
		super();
	}

	public int getCode() {
		return code;
	}

	public void setCode(int code) {
		this.code = code;
	}

	public String getContent() {
		return content;
	}

	public void setContent(String content) {
		this.content = content;
	}

	@Override
	public int hashCode() {
		final int prime = 37;
		int result = 17;
		result = prime * result + code;
		result = prime * result + ((content == null) ? 0 : content.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		TransportMessage other = (TransportMessage) obj;
		if (code != other.code)
			return false;
		if (content == null) {
			if (other.content != null)
				return false;
		} else if (!content.equals(other.content))
			return false;
		return true;
	}

	@Override
	public String toString() {
		return "TransportMessage [code=" + code + ", content=" + content + "]";
	}

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>======== socket server (with thread pool)</p> 
 <p>SocketServer.java</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingQueue;

public class SocketServer implements Runnable {

	private final String name;
	private final ServerSocket server;

	private final BlockingQueue&lt;Socket&gt; queue;

	public SocketServer(String name, BlockingQueue&lt;Socket&gt; queue, int port)
			throws IOException {
		super();
		this.name = name;
		this.server = new ServerSocket(port);
		this.server.setReuseAddress(true);
		this.queue = queue;
		System.out.println(server + " start to run.");
	}

	@Override
	public void run() {
		Thread.currentThread().setName(name);
		while (true) {
			try {
				queue.put(server.accept());
			} catch (IOException e) {
				e.printStackTrace();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}

		}

	}

	/**
	 * @param args
	 * @throws IOException
	 */
	public static void main(String[] args) throws IOException {
		int port = 7777;
		int threadPoolSize = Runtime.getRuntime().availableProcessors() * 6;
		BlockingQueue&lt;Socket&gt; queue = new LinkedBlockingQueue&lt;Socket&gt;();
		ExecutorService exec = Executors.newCachedThreadPool();
		exec.execute(new SocketServer("producer", queue, port));
		for (int i = 0; i &lt; threadPoolSize; i++) {
			exec.execute(new Consumer(queue, "consumer-" + i));
		}
		exec.shutdown();

	}

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>Consumer.java</p> 
 <pre name="code" class="java">import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.atomic.AtomicInteger;

import com.alibaba.fastjson.JSON;

public class Consumer implements Runnable {
	private static final AtomicInteger count = new AtomicInteger();
	private final BlockingQueue&lt;Socket&gt; queue;
	private final String name;

	public Consumer(BlockingQueue&lt;Socket&gt; queue, String name) {
		super();
		this.queue = queue;
		this.name = name;
	}

	public void run() {
		Thread.currentThread().setName(name);
		System.out.println(name + " start to run.");
		while (true) {
			try {
				consume(queue.take());
			} catch (Exception e) {
				e.printStackTrace();
			}
		}

	}

	private void consume(Socket socket) throws IOException {
		try {
			socket.setTcpNoDelay(true);

			BufferedReader br = getReader(socket);
			PrintWriter pw = getWriter(socket);
			for (String msg = br.readLine(); msg != null; msg = br.readLine()) {
				System.out.println(Thread.currentThread().getName()
						+ " receive msg : " + msg + " from "
						+ socket.getRemoteSocketAddress() + ":"
						+ socket.getPort());

				String response = echoMsg(msg);
				pw.println(response);
				pw.flush();
				System.out.println(Thread.currentThread().getName()
						+ " send msg: " + response);
				if (msg.equalsIgnoreCase("bye")) {
					break;
				}
			}
		} finally {
			if (null != socket) {
				try {
					socket.close();
					System.out.println(Thread.currentThread().getName()
							+ " closes " + socket);
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
	}

	private PrintWriter getWriter(Socket socket) throws IOException {
		return new PrintWriter(socket.getOutputStream());
	}

	private BufferedReader getReader(Socket socket) throws IOException {
		return new BufferedReader(
				new InputStreamReader(socket.getInputStream()));
	}

	private String echoMsg(String request) {

		TransportMessage msg = JSON
				.parseObject(request, TransportMessage.class);

		return msg.getCode() + " --&gt; world_" + count.getAndIncrement();
	}

}</pre> 
 <p>&nbsp;</p> 
 <p>=== socket client</p> 
 <p>SocketClient.java</p> 
 <pre name="code" class="java">import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;
import java.net.UnknownHostException;

import com.alibaba.fastjson.JSON;

public class SocketClient {

	
	private final Socket socket;

	public SocketClient(String host, int port) throws UnknownHostException,
			IOException {
		this.socket = new Socket(host, port);
		this.socket.setTcpNoDelay(true);
		this.socket.setTrafficClass(0x08 | 0x10);
		this.socket.setReuseAddress(true);
		
	}

	private PrintWriter getWriter(Socket socket) throws IOException {
		return new PrintWriter(socket.getOutputStream());
	}

	private BufferedReader getReader(Socket socket) throws IOException {
		return new BufferedReader(
				new InputStreamReader(socket.getInputStream()));
	}

	private void talk() {
		try {
			BufferedReader br = getReader(socket);
			PrintWriter pw = getWriter(socket);
			for (int i = 0; i &lt; 100; i++) {
				TransportMessage tm = new TransportMessage(i, "Hello_" + i);
				String msg = JSON.toJSONString(tm);
				pw.println(msg);
				pw.flush();
				System.out.println("send msg : " + msg);

				System.out.println("receive msg : " + br.readLine());

			}

		} catch (Exception e) {
			e.printStackTrace();
		} finally {
			if (null != socket) {
				try {
					socket.close();
				} catch (IOException ex) {
					ex.printStackTrace();
				}
			}
		}

	}

	public static void main(String[] args) throws UnknownHostException,
			IOException {
		String host = "192.168.123.53";
		int port = 7777;
//		int port = 10007;

		for (int i = 0; i &lt; 100000; i++) {
			new SocketClient(host, port).talk();
		}

	}
}</pre> 
 <p>&nbsp;</p> 
</div>