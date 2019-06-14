#Java socket client与server的通讯
###发表时间：2013-11-28
###分类：socket,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1982148" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1982148</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在CSDN上面有人问client如何与server通讯的问题，就是一问一答。我这里写了个例子，留存一下：</p> 
 <pre name="code" class="java">import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.io.Reader;
import java.io.Writer;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingQueue;

import org.apache.commons.io.IOUtils;
import org.apache.log4j.Logger;

/**
 * &lt;pre&gt;
 * @author kanpiaoxue
 * Date 2013-11-27
 * &lt;/pre&gt;
 */
public class TalkSocketServer {
	private static final Logger LOGGER = Logger
			.getLogger(TalkSocketServer.class);

	class Producer implements Runnable {
		private BlockingQueue&lt;Socket&gt; queue;
		private ServerSocket server;

		public Producer(String name, BlockingQueue&lt;Socket&gt; queue, int port) {
			super();
			this.queue = queue;
			try {
				Thread.currentThread().setName(name);
				server = new ServerSocket(port);
			} catch (IOException e) {
				LOGGER.error("Error:" + e.getMessage(), e);
			}
		}

		@Override
		public void run() {
			LOGGER.info(server + " start to work.");
			while (true) {
				try {
					queue.put(server.accept());
				} catch (Exception e) {
					LOGGER.error("Error:" + e.getMessage(), e);
				}
			}

		}
	}

	class Consumer implements Runnable {

		private BlockingQueue&lt;Socket&gt; queue;

		public Consumer(String name, BlockingQueue&lt;Socket&gt; queue) {
			super();
			this.queue = queue;
			Thread.currentThread().setName(name);
		}

		@Override
		public void run() {
			while (true) {
				Socket socket = null;
				try {
					socket = queue.take();
					consume(socket);
				} catch (Exception e) {
					LOGGER.error("Error:" + e.getMessage(), e);
				} finally {
					if (null != socket) {
						try {
							socket.close();
							LOGGER.info(socket + " closed.");
						} catch (IOException e) {
						}
					}
				}
			}

		}

		private void consume(Socket socket) throws Exception {
			PrintWriter writer = new PrintWriter(socket.getOutputStream());
			BufferedReader reader = new BufferedReader(new InputStreamReader(
					socket.getInputStream()));
			sendMsg(writer, "Welcome to talking system!");
			for (String request = reader.readLine(); null != request; request = reader
					.readLine()) {
				if (request.trim().equalsIgnoreCase("bye")) {
					sendMsg(writer, "Good bye " + socket + " !");
					closeAll(writer, reader, socket);
					break;
				}
				sendMsg(writer, socket + "You say [" + request + "] to me.");
			}

			// close all resource
			closeAll(writer, reader, socket);
		}

		private void closeAll(Writer writer, Reader reader, Socket socket)
				throws IOException {
			IOUtils.closeQuietly(writer);
			IOUtils.closeQuietly(reader);
			socket.close();
		}

		private void sendMsg(PrintWriter writer, String msg) {
			writer.println(msg);
			writer.flush();
		}
	}

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		TalkSocketServer t = new TalkSocketServer();
		ExecutorService exec = Executors.newCachedThreadPool();
		BlockingQueue&lt;Socket&gt; queue = new LinkedBlockingQueue&lt;Socket&gt;();
		int port = 7777;
		exec.execute(t.new Producer("producer", queue, port));
		for (int i = 0, j = Runtime.getRuntime().availableProcessors() * 2; i &lt; j; i++) {
			exec.execute(t.new Consumer("consumer-" + i, queue));
		}
		exec.shutdown();
	}

}








import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.io.Reader;
import java.io.Writer;
import java.net.Socket;

import org.apache.commons.io.IOUtils;
import org.apache.log4j.Logger;

/**
 * 
 * @author kanpiaoxue
 * 
 */
public class TestSocketClient {
	private static final Logger LOGGER = Logger
			.getLogger(TestSocketClient.class);

	private Socket socket;

	/**
	 * @param host
	 * @param port
	 */
	public TestSocketClient(String host, int port) {
		super();
		try {
			socket = new Socket(host, port);
			LOGGER.info(socket + " start to work.");
		} catch (Exception e) {
			LOGGER.error("Error:" + e.getMessage(), e);
		}
	}

	public void talk() throws Exception {
		BufferedReader localReader = new BufferedReader(new InputStreamReader(
				System.in));
		PrintWriter writer = new PrintWriter(socket.getOutputStream());
		BufferedReader reader = new BufferedReader(new InputStreamReader(
				socket.getInputStream()));
		System.out.println(reader.readLine());
		System.out.println("enter message :");
		for (String request = localReader.readLine(); null != request; request = localReader
				.readLine()) {
			sendMsg(writer, request);
			System.out.println(reader.readLine());
			if (request.trim().equalsIgnoreCase("bye")) {
				break;
			}
		}

		IOUtils.closeQuietly(localReader);
		closeAll(writer, reader, socket);

	}

	private void closeAll(Writer writer, Reader reader, Socket socket)
			throws IOException {
		IOUtils.closeQuietly(writer);
		IOUtils.closeQuietly(reader);
		socket.close();
	}

	private void sendMsg(PrintWriter writer, String msg) {
		writer.println(msg);
		writer.flush();
	}

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		try {
			new TestSocketClient("localhost", 7777).talk();
		} catch (Exception e) {
			LOGGER.error("Error:" + e.getMessage(), e);
		}

	}

}</pre> 
 <p>&nbsp;</p> 
</div>