#Netty4 httpserver
###发表时间：2014-12-04
###分类：Netty,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2163332" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2163332</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * AjaxResult.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年12月4日 下午6:01:05&lt;br&gt;
 * Description : ajax请求结果
 * &lt;/pre&gt;
 */
public class AjaxResult {
    private int code;
    private String message;
    private Object body;

    public static AjaxResult SUCCESS = new AjaxResult(0, "success");
    public static AjaxResult FAILURE = new AjaxResult(1, "failure");

    /**
     * &lt;pre&gt;
     * @param code
     * @param message
     * &lt;/pre&gt;
     */
    private AjaxResult(int code, String message) {
        super();
        this.code = code;
        this.message = message;
    }

    /**
     * &lt;pre&gt;
     * @return the body
     * &lt;/pre&gt;
     */
    public Object getBody() {
        return body;
    }

    /**
     * &lt;pre&gt;
     * @return the code
     * &lt;/pre&gt;
     */
    public int getCode() {
        return code;
    }

    /**
     * &lt;pre&gt;
     * @return the message
     * &lt;/pre&gt;
     */
    public String getMessage() {
        return message;
    }

    /**
     * &lt;pre&gt;
     * @param body the body to set
     * &lt;/pre&gt;
     */
    public AjaxResult setBody(Object body) {
        this.body = body;
        return this;
    }

    /**
     * &lt;pre&gt;
     * @param code the code to set
     * &lt;/pre&gt;
     */
    public AjaxResult setCode(int code) {
        this.code = code;
        return this;
    }

    /**
     * &lt;pre&gt;
     * @param message the message to set
     * &lt;/pre&gt;
     */
    public AjaxResult setMessage(String message) {
        this.message = message;
        return this;
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import static io.netty.handler.codec.http.HttpHeaders.Names.CONNECTION;
import static io.netty.handler.codec.http.HttpHeaders.Names.CONTENT_LENGTH;
import static io.netty.handler.codec.http.HttpHeaders.Names.CONTENT_TYPE;
import static io.netty.handler.codec.http.HttpHeaders.Names.EXPIRES;
import static io.netty.handler.codec.http.HttpResponseStatus.NOT_FOUND;
import static io.netty.handler.codec.http.HttpResponseStatus.OK;
import static io.netty.handler.codec.http.HttpVersion.HTTP_1_1;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.alibaba.fastjson.JSON;
import com.google.common.base.Charsets;

import io.netty.buffer.ByteBuf;
import io.netty.buffer.Unpooled;
import io.netty.channel.ChannelHandlerContext;
import io.netty.channel.ChannelInboundHandlerAdapter;
import io.netty.handler.codec.http.DefaultFullHttpResponse;
import io.netty.handler.codec.http.FullHttpResponse;
import io.netty.handler.codec.http.HttpContent;
import io.netty.handler.codec.http.HttpHeaders;
import io.netty.handler.codec.http.HttpHeaders.Values;
import io.netty.handler.codec.http.HttpMethod;
import io.netty.handler.codec.http.HttpRequest;
import io.netty.handler.codec.http.HttpResponseStatus;
import io.netty.handler.codec.http.QueryStringDecoder;

import java.io.UnsupportedEncodingException;
import java.util.List;
import java.util.Map;
import java.util.Map.Entry;
import java.util.regex.Pattern;

/**
 * &lt;pre&gt;
 * HttpServerInboundHandler.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年12月4日 下午4:51:07&lt;br&gt;
 * Description : HttpServerInboundHandler
 * &lt;/pre&gt;
 */
public class HttpServerInboundHandler extends ChannelInboundHandlerAdapter {

    private static final Logger LOGGER = LoggerFactory
            .getLogger(HttpServerInboundHandler.class);

    private static final Pattern SEND_TASK_FOR_METHOD_GET_PATTERN = Pattern
            .compile("/dmap-sf/query(?:\\?.*)?");

    private static final Pattern SEND_TASK_FOR_METHOD_POST_PATTERN = Pattern
            .compile("/dmap-sf/sendMsg(?:\\?.*)?");

    private HttpRequest request;
    private boolean isGet;
    private boolean isPost;

    /**
     * POST: http://localhost:8844/dmap-sf/sendMsg?hello=df&amp;world=women body: we
     * are togather
     *
     * GET: http://localhost:8844/dmap-sf/query?hello=df&amp;world=women
     */
    @Override
    public void channelRead(ChannelHandlerContext ctx, Object msg)
            throws Exception {
        if (msg instanceof HttpRequest) {
            request = (HttpRequest) msg;

            String uri = request.getUri();
            HttpMethod method = request.getMethod();

            isGet = method.equals(HttpMethod.GET);
            isPost = method.equals(HttpMethod.POST);

            System.out.println(String.format("Uri:%s method %s", uri, method));

            if (SEND_TASK_FOR_METHOD_GET_PATTERN.matcher(uri).matches()
                    &amp;&amp; isGet) {
                System.out.println("doing something here.");
                String param = "hello";
                String str = getParamerByNameFromGET(param);
                System.out.println(param + ":" + str);
            }
            if (SEND_TASK_FOR_METHOD_POST_PATTERN.matcher(uri).matches()
                    &amp;&amp; isPost) {
                System.out.println("doing something here.");
            } else {
                String responseString = JSON.toJSONString(AjaxResult.FAILURE
                        .setMessage(String.format(
                                "Cann't find the url:%s for method:%s", uri,
                                method.name())));

                writeHttpResponse(responseString, ctx, NOT_FOUND);
                return;
            }

        }

        if (!isGet) {
            if (msg instanceof HttpContent) {
                HttpContent content = (HttpContent) msg;

                ByteBuf buf = content.content();
                String bodyString = buf.toString(Charsets.UTF_8);

                System.out.println("body: " + bodyString);

                String l = getParamerByNameFromPOST("hello", bodyString);
                System.out.println(l);

                buf.release();
                String responseString = JSON.toJSONString(AjaxResult.SUCCESS);
                writeHttpResponse(responseString, ctx, OK);
            }
        }
    }

    @Override
    public void channelReadComplete(ChannelHandlerContext ctx) throws Exception {
        ctx.flush();
    }

    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) {
        LOGGER.error(cause.getMessage());
        ctx.close();
    }

    private String getParamerByNameFromGET(String name) {
        QueryStringDecoder decoderQuery = new QueryStringDecoder(
                request.getUri());
        return getParameterByName(name, decoderQuery);
    }

    private String getParamerByNameFromPOST(String name, String body) {
        QueryStringDecoder decoderQuery = new QueryStringDecoder("some?" + body);
        return getParameterByName(name, decoderQuery);
    }

    /**
     * &lt;pre&gt;
     * @param name
     * @param decoderQuery
     * @return
     * &lt;/pre&gt;
     */
    private String getParameterByName(String name,
            QueryStringDecoder decoderQuery) {
        Map&lt;String, List&lt;String&gt;&gt; uriAttributes = decoderQuery.parameters();
        for (Entry&lt;String, List&lt;String&gt;&gt; attr : uriAttributes.entrySet()) {
            String key = attr.getKey();
            for (String attrVal : attr.getValue()) {
                if (key.equals(name)) {
                    return attrVal;
                }
            }
        }
        return null;
    }

    private void writeHttpResponse(String responseString,
            ChannelHandlerContext ctx, HttpResponseStatus status)
                    throws UnsupportedEncodingException {
        FullHttpResponse response = new DefaultFullHttpResponse(HTTP_1_1,
                status, Unpooled.wrappedBuffer(responseString
                        .getBytes(Charsets.UTF_8)));
        response.headers().set(CONTENT_TYPE, "text/json");
        response.headers().set(CONTENT_LENGTH,
                response.content().readableBytes());
        response.headers().set(EXPIRES, 0);
        if (HttpHeaders.isKeepAlive(request)) {
            response.headers().set(CONNECTION, Values.KEEP_ALIVE);
        }
        ctx.write(response);
        ctx.flush();
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;

import io.netty.bootstrap.ServerBootstrap;
import io.netty.channel.ChannelFuture; 
import io.netty.channel.ChannelInitializer; 
import io.netty.channel.ChannelOption; 
import io.netty.channel.EventLoopGroup; 
import io.netty.channel.nio.NioEventLoopGroup; 
import io.netty.channel.socket.SocketChannel; 
import io.netty.channel.socket.nio.NioServerSocketChannel;
import io.netty.handler.codec.http.HttpRequestDecoder; 
import io.netty.handler.codec.http.HttpResponseEncoder; 
/**
 * &lt;pre&gt;
 * HttpServer.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年12月4日 下午4:52:39&lt;br&gt;
 * Description : HttpServer
 * &lt;/pre&gt;
 */


public class HttpServer {

    private static Log log = LogFactory.getLog(HttpServer.class);
    
    public void start(int port) throws Exception {
        EventLoopGroup bossGroup = new NioEventLoopGroup();
        EventLoopGroup workerGroup = new NioEventLoopGroup();
        try {
            ServerBootstrap b = new ServerBootstrap();
            b.group(bossGroup, workerGroup).channel(NioServerSocketChannel.class)
                    .childHandler(new ChannelInitializer&lt;SocketChannel&gt;() {
                                @Override
                                public void initChannel(SocketChannel ch) throws Exception {
                                    ch.pipeline().addLast(new HttpResponseEncoder());
                                    ch.pipeline().addLast(new HttpRequestDecoder());
                                    ch.pipeline().addLast(new HttpServerInboundHandler());
                                }
                            }).option(ChannelOption.SO_BACKLOG, 128) 
                    .childOption(ChannelOption.SO_KEEPALIVE, true);

            ChannelFuture f = b.bind(port).sync();

            f.channel().closeFuture().sync();
        } finally {
            workerGroup.shutdownGracefully();
            bossGroup.shutdownGracefully();
        }
    }

    public static void main(String[] args) throws Exception {
        HttpServer server = new HttpServer();
        log.info("Http Server listening on 8844 ...");
        server.start(8844);
    }
}</pre> 
 <p>&nbsp;</p> 
</div>