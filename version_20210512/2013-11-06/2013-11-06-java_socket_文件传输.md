#java socket 文件传输
###发表时间：2013-11-06
###分类：java,socket
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1972137" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1972137</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>闲着无聊，写了一个基于java的socket文件传输。</p> 
 <p>是这样设计的：</p> 
 <p>1、Server</p> 
 <p>提供文件传输的server服务器端，接收client发送过来的文件。</p> 
 <p>提供多线程并发处理，能同时处理多个client的文件传输请求。</p> 
 <p>2、Client</p> 
 <p>根据提供的参数指定的server以及本地文件的路径，进行文件传输</p> 
 <p>&nbsp;</p> 
 <p>client的代码</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileInputStream;
import java.io.IOException;
import java.net.InetAddress;
import java.net.InetSocketAddress;
import java.net.Socket;
import java.net.SocketAddress;

import org.apache.commons.io.IOUtils;
import org.apache.commons.lang.StringUtils;
import org.apache.log4j.Logger;

public class FileClient {
	private static final Logger LOGGER = Logger.getLogger(FileClient.class);
	private Socket socket;

	public void sendFile(File file, String host, int port) throws IOException {
		if (!file.exists() || !file.isFile()) {
			throw new IllegalArgumentException("file : " + file
					+ " is not a valid file!");
		}
		connect(host, port);
		sendFile(file);
		close();
	}

	private void sendFile(File file) throws IOException {
		BufferedOutputStream fileOutput = new BufferedOutputStream(
				socket.getOutputStream());
		BufferedInputStream input = new BufferedInputStream(
				new FileInputStream(file));
		IOUtils.copy(input, fileOutput);
		fileOutput.flush();

		IOUtils.closeQuietly(input);
		IOUtils.closeQuietly(fileOutput);
	}

	private void close() throws IOException {
		if (isConnected()) {
			socket.close();
		}
	}

	private boolean isConnected() {
		return null != socket &amp;&amp; socket.isConnected() &amp;&amp; !socket.isClosed();
	}

	private void connect(String host, int port) throws IOException {
		if (isConnected()) {
			return;
		}
		socket = new Socket();
		socket.setKeepAlive(true);
		socket.setReuseAddress(true);
		InetAddress addr = InetAddress.getByName(host);
		SocketAddress endpoint = new InetSocketAddress(addr, port);
		socket.connect(endpoint);

	}

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		String filePath = System.getProperty("file");
		if (StringUtils.isEmpty(filePath)) {
			LOGGER.error("Error: JVM argumengs -Dfile is null !");
			return;
		}
		String host = System.getProperty("host");
		if (StringUtils.isEmpty(host)) {
			LOGGER.error("Error: JVM argumengs -Dhost is null !");
			return;
		}
		String portString = System.getProperty("port");
		if (StringUtils.isEmpty(portString)) {
			LOGGER.error("Error: JVM argumengs -Dport is null !");
			return;
		}
		int port = Integer.valueOf(portString).intValue();
		File file = new File(filePath);
		FileClient client = new FileClient();
		try {
			LOGGER.info("start to transfer file : " + file);
			long before = System.currentTimeMillis();
			client.sendFile(file, host, port);
			LOGGER.info("transfer file : " + file
					+ " successfully! It consumes "
					+ (System.currentTimeMillis() - before) + " ms.");
		} catch (IOException e) {
			LOGGER.error("Error:" + e.getMessage(), e);
		}

	}

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;server的代码：</p> 
 <pre name="code" class="java">import java.io.File;
import java.net.Socket;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.LinkedBlockingQueue;

public class Bootstrap {

	/**
	 * @param args
	 */
	public static void main(String[] args) throws Exception{
		int cpuTimes = 4;
		int port = 7777;
		BlockingQueue&lt;Socket&gt; queue = new LinkedBlockingQueue&lt;Socket&gt;();
		ExecutorService exec = Executors.newCachedThreadPool();
		exec.execute(new FileEchoServer("server-1", port, queue));
		File path = new File("E:/temp");
		for (int i = 0, count = Runtime.getRuntime().availableProcessors()
				* cpuTimes; i &lt; count; i++) {
			exec.execute(new FileConsumer("socket-" + i, queue,path));
		}
		exec.shutdown();

	}

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.io.IOException;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.concurrent.BlockingQueue;

import org.apache.log4j.Logger;

/**
 * @author kanpiaoxue
 *
 */
public class FileEchoServer implements Runnable {
	protected static final Logger LOGGER = Logger.getLogger(FileEchoServer.class);
	protected final ServerSocket serverSocket;
	protected final BlockingQueue&lt;Socket&gt; queue;
	protected final String name;

	public FileEchoServer(String name, int port, BlockingQueue&lt;Socket&gt; queue)
			throws IOException {
		serverSocket = new ServerSocket(port);
		serverSocket.setReuseAddress(true);
		LOGGER.info(serverSocket);
		this.queue = queue;
		this.name = name;
	}

	@Override
	public void run() {
		setName(name);
		while (true) {
			try {
				queue.put(serverSocket.accept());
			} catch (Exception e) {
				LOGGER.error("Error:" + e.getMessage(), e);
			}
		}
	}

	private void setName(String name) {
		Thread.currentThread().setName(name);
		LOGGER.info(name + " start to work.");
	}
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.net.Socket;
import java.util.concurrent.BlockingQueue;

import org.apache.log4j.Logger;

/**
 * @author kanpiaoxue
 *
 */
public abstract class AbstractSocketConsumer implements Runnable {
	protected static final Logger LOGGER = Logger
			.getLogger(AbstractSocketConsumer.class);
	protected final String name;
	protected final BlockingQueue&lt;Socket&gt; queue;

	public AbstractSocketConsumer(String name, BlockingQueue&lt;Socket&gt; queue) {
		super();
		this.name = name;
		this.queue = queue;
	}

	private void setName(String name) {
		Thread.currentThread().setName(name);
		LOGGER.info(name + " start to work.");
	}

	@Override
	public void run() {
		setName(name);
		while (true) {
			try {
				consume(queue.take());
			} catch (Exception e) {
				LOGGER.error("Error:" + e.getMessage(), e);
			}
		}

	}

	protected abstract void consume(Socket socket) throws Exception;

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.File;
import java.io.FileOutputStream;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.atomic.AtomicLong;

import org.apache.commons.io.IOUtils;

import com.wanmei.net.slef.file.AbstractSocketConsumer;

public class FileConsumer extends AbstractSocketConsumer {

	private File filePath;
	private static final AtomicLong FILE_COUNT = new AtomicLong();

	public FileConsumer(String name, BlockingQueue&lt;Socket&gt; queue, File path) {
		super(name, queue);
		this.filePath = path;
	}

	@Override
	protected void consume(Socket socket) throws Exception {
		LOGGER.info("start to receive file from "
				+ socket.getInetAddress().getHostName() + ":"
				+ socket.getPort());
		long before = System.currentTimeMillis();
		File file = new File(filePath, "file-" + FILE_COUNT.getAndIncrement());
		if (file.exists()) {
			file.delete();
		}
		BufferedOutputStream fileOutput = new BufferedOutputStream(
				new FileOutputStream(file));
		BufferedInputStream input = new BufferedInputStream(
				socket.getInputStream());
		IOUtils.copy(input, fileOutput);

		fileOutput.flush();

		PrintWriter response = new PrintWriter(socket.getOutputStream());

		String responseString = echo(socket);
		response.println(responseString);
		response.flush();

		if (null != socket) {
			IOUtils.closeQuietly(input);
			IOUtils.closeQuietly(fileOutput);
			IOUtils.closeQuietly(response);
			socket.close();
		}
		LOGGER.info("transfer file : " + file + " successfully! It consumes "
				+ (System.currentTimeMillis() - before) + " ms.");
	}

	private String echo(Socket socket) {
		return "Transfer file " + socket.getLocalAddress().getHostName() + ":"
				+ socket.getLocalPort() + " OK!";
	}

}</pre> 
 <p>&nbsp;</p> 
 <p>这个进行过测试，代码是可以运行的。这里的代码有其他的的依赖的jar包，就是apache下面的commons下面的一些常用包：</p> 
 <p>org.apache.commons.io.IOUtils</p> 
 <p>org.apache.commons.lang.StringUtils</p> 
 <p>org.apache.log4j.Logger</p> 
 <p>&nbsp;</p> 
 <p>后记：这里只是简单的写了一个socket的文件传输。其实这里的代码的实际应用意义不是很大。</p> 
 <p>一般我们进行文件传输的时候，还需要进行一些必要的工作，比如：文件大小的校验，或者文件的MD5的校验，用来保证文件传输之前和传输之后的完整性，正确性。</p> 
 <p>这里给出一个提示：</p> 
 <p>client：可以在发送文件的client里面写2个socket，第一个socket用来告诉服务器“我要给你传输一个文件，这个文件的名字是：file-test.txt，它的MD5是：XXXXXXXXXX，文件的大小是xxxxxbytes”。当这个socket从服务器得到允许“yes”的消息，以及服务器创建的临时ServerSocket的host、port之后，开始用第二个socket进行文件传输。</p> 
 <p>server：在server中，当一个socket接到client发送的“我要给你传输一个文件，这个文件的名字是：file-test.txt，它的MD5是：XXXXXXXXXX，文件的大小是xxxxxbytes”的消息之后，判断是否需要client进行文件发送（例如根据文件的大小，判断当前的服务器有足够的磁盘空间存放客户端发送来的文件。如果文件大小够存放client传输过来的文件，那么进行下一步。如果不够存放client传输过来的文件，那么告知client，当前的服务器磁盘空间已满，不能进行文件传输。）。如果需要，则把该文件的名称，该文件的MD5记录到本地的内存中，然后建立一个临时的ServerSocket对象（指定任意端口），再通过上面的socket回复给client的第一个socket，告诉他可以（yes），并告知client的第一个socket这个临时的ServerSocket的对象的host，port。好允许client利用第二个socket进行文件传输，将文件流写给这里的ServerSocket。</p> 
 <p>当Server端判断出文件接收完毕，马上对该接收到的文件生成MD5校验码，将该校验码与之前client第一个socket传送来的MD5校验码进行校对。发现一致，继续等待下一个文件的传输任务的到来；如果不一致，可以告诉client，该文件需要进行重传。</p> 
 <p>这里需要注意的一个地方是：当server端启动多个线程进行文件接收的时候，最好不要用文件大小来判断磁盘空间是否可以存放client传输过来的文件。为什么？因为server接收文件是并行的。当其中一个线程接收到文件的磁盘检查的时候，该服务器的磁盘空间确实够存放文件，就会告诉client进行文件传输。这个时候很有可能，server的另一个线程也接到文件大小的检验的任务，开始检查磁盘空间是否够存放client传输的文件。发现空间是够用的，也告诉了当前的client可以进行文件传输。这个时候，会产生问题的：当server的磁盘空间就剩下1G的时候，一个client传输的文件是600M，另一个client传输的文件是700M，就会造成2个client的文件都无法完成传输而报错。因为它们占用服务器空间的大小，超过了服务器现在的空间大小。</p> 
 <p>那么该如何处理服务器磁盘空间大小检查的问题呢？没有更好的办法，服务器只能采用单线程的服务器文件传输。另一个方法，服务器程序内含一个文件大小检查的线程，定时（间隔10秒）检查服务器的空间是否达到预警阀值（这个阀值最好设置的大一点，比如1T的大小，可以存放半天的数据传输）。当到达预警阀值，可以发送预警信息（电子邮件、手机短信）给管理员，要求他进行磁盘空间的扩展。</p> 
 <p>&nbsp; &nbsp;另一个文件传输的方法：采用一个socket进行文件传输，而不是像上面那样采用2个socket，一个用来发送文件的具体信息，一个用来传输文件。如果需要采用一个socket，就需要自己写一个协议。其实这样的协议是存在的，如 http 协议。我们也可以自己写一个传输文件的协议，该协议分为2个部分。第一部分，header，用来存放文件的必要信息，比如：文件大小，文件名称，文件的MD5等等；第二部分，body，用来存放文件的流内容。这样，client可以在按照协议发送给服务器一个封装好的内容，server呢按照协议进行解析出header、body，然后存放文件。这样做就会复杂一点，要想简化，可以采用http协议来传输文件。http具有“协议、header、body”的完整结构，可以满足文件传输的需要。</p> 
 <p>上面给出的思路，大致能实现文件的安全传输，里面包含了文件传输，文件完整性/准确性校验，文件传输发生错误之后的重传机制。这个思路，和FTP的文件传输相似。可以进行参考。</p> 
 <p>&nbsp;</p> 
</div>