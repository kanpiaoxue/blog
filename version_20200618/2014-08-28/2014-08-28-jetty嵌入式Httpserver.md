#jetty嵌入式Httpserver
###发表时间：2014-08-28
###分类：java,jetty
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2110496" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2110496</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我们经常会用程序提供对外的http服务，如 REST 风格的 API 提供给其他的客户来调用我们的服务或者进行一些信息的查询。我们会将这些程序写成WEB程序，提供这样的REST服务。我这里介绍用jetty（一个高性能的Servlet服务器，纯Java编写）编写一个嵌入式的HttpServer。例子的内容很简单，只是提供一些提示。</p> 
 <p>代码如下：</p> 
 <pre name="code" class="java">package test;

import org.eclipse.jetty.server.Request;
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.server.handler.AbstractHandler;
import org.eclipse.jetty.server.handler.ContextHandler;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * &lt;pre&gt;
 * JettyExampleServer.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月28日 下午4:05:25&lt;br&gt;
 * Description : 利用Jetty实现简单的嵌入式Httpserver
 * &lt;/pre&gt;
 */
public class JettyExampleServer {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(JettyExampleServer.class);

    /**
     * &lt;pre&gt;
     * @param args
     * &lt;/pre&gt;
     */
    public static void main(String[] args) {
        try {
            // 进行服务器配置
            Server server = new Server(8080);
            LOGGER.info("server start.");
            ContextHandler context = new ContextHandler();
            // 设置搜索的URL地址
            context.setContextPath("/search");
            context.setResourceBase(".");
            context.setClassLoader(Thread.currentThread()
                    .getContextClassLoader());
            server.setHandler(context);
            context.setHandler(new HelloHandler());
            // 启动服务器
            server.start();
            server.join();
        } catch (Exception e) {
            e.printStackTrace();
        }

    }

}

class HelloHandler extends AbstractHandler {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(JettyExampleServer.class);

    @Override
    public void handle(String target, Request baseRequest,
            HttpServletRequest request, HttpServletResponse response)
            throws IOException, ServletException {

        /**
         * &lt;pre&gt;
         * 从 URL 里面得到传递过来的参数：
         *  http://localhost:8080/search?query=hello
         * 如果你需要传递更多的参数，可以这么写：
         *  http://localhost:8080/search?query=hello&amp;name=ZhangLili
         * 从这里开始，你可以写自己的代码逻辑。
         * 
         * [注意：GET方法的请求，URL 的最大长度是 1024个字节]
         * &lt;/pre&gt;
         */

        String query = request.getParameter("query");
        // String name = request.getParameter("name");

        LOGGER.info(String.format("receive query: %s", query));

        String result = "welcome to my server.";
        if (null != query &amp;&amp; query.equals("hello")) {
            result = query + ", " + result;
        }
        LOGGER.info(String.format("response is: %s", result));

        // 将服务器处理后的结果返回给调用URL的客户端
        print(baseRequest, response, result);
    }

    /**
     * &lt;pre&gt;
     * @param baseRequest
     * @param response
     * @param result 需要返回给客户的结果
     * @throws IOException
     * 将结果 result 返回给客户
     * &lt;/pre&gt;
     */
    private void print(Request baseRequest, HttpServletResponse response,
            String result) throws IOException {
        response.setContentType("text/json;charset=utf-8");
        response.setStatus(HttpServletResponse.SC_OK);
        baseRequest.setHandled(true);
        response.getWriter().println(result);
    }
}
</pre> 
 <p>&nbsp;</p> 
 <p>它需要的jar请看附件。附件中有完整的代码，下载之后将lib目录的jar都放在classpath下面，该程序就可以运行。访问地址，如：http://localhost:8080/search?query=hello</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>============================</p> 
 <p>下面的例子是用jetty嵌入式server实现HttpServlet的例子。可以进行GET和POST请求</p> 
 <pre name="code" class="java">package test;

import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.servlet.ServletContextHandler;
import org.eclipse.jetty.servlet.ServletHolder;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import test.servlet.SearchServlet;

/**
 * &lt;pre&gt;
 * JettyServletExampleServer.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年9月2日 下午4:53:49&lt;br&gt;
 * Description : 利用Jetty实现简单的嵌入式Httpserver，利用HttpServlet进行编程
 * &lt;/pre&gt;
 */
public class JettyServletExampleServer {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(JettyServletExampleServer.class);

    /**
     * &lt;pre&gt;
     * @param args
     * &lt;/pre&gt;
     */
    public static void main(String[] args) {
        try {
            Server server = new Server(8080);

            ServletContextHandler context = new ServletContextHandler(
                    ServletContextHandler.SESSIONS);
            context.setContextPath("/");
            server.setHandler(context);

            context.addServlet(new ServletHolder(new SearchServlet()),
                    "/search");
            LOGGER.info("server start.");
            server.start();
            server.join();
        } catch (Exception e) {
            e.printStackTrace();
        }

    }

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * Copyright baidu.com CDC [2000-2014]
 * &lt;/pre&gt;
 */
package test.servlet;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import test.utils.Tools;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * &lt;pre&gt;
 * HelloServlet.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年9月2日 下午4:55:40&lt;br&gt;
 * Description : HttpServlet
 * &lt;/pre&gt;
 */
public class SearchServlet extends HttpServlet {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(SearchServlet.class);

    /**
     * &lt;pre&gt;
     * &lt;/pre&gt;
     */

    private static final long serialVersionUID = -4012838481920999524L;

    /**
     * 写在这里的代码都是 POST 请求
     */
    @Override
    public void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String query = request.getParameter("query");

        LOGGER.info(String.format("receive query: %s", query));

        String result = "welcome to my server. It's a POST request.";
        if (null != query &amp;&amp; !query.trim().equals("")) {
            result = query + ", " + result;
        }
        LOGGER.info(String.format("response is: %s", result));

        Tools.printToJson(result, response);
    }

    /**
     * 写在这里的代码都是 GET 请求
     */
    @Override
    public void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        String query = request.getParameter("query");

        LOGGER.info(String.format("receive query: %s", query));

        String result = "welcome to my server. It's a GET request.";
        if (null != query &amp;&amp; !query.trim().equals("")) {
            result = query + ", " + result;
        }
        LOGGER.info(String.format("response is: %s", result));

        Tools.printToJson(result, response);
    }
}
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package test.utils;

import org.eclipse.jetty.server.Request;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.http.HttpServletResponse;

/**
 * &lt;pre&gt;
 * Tools.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年9月2日 下午4:57:06&lt;br&gt;
 * Description : 工具类
 * &lt;/pre&gt;
 */
public class Tools {

    private Tools() {
        super();
    }

    /**
     * &lt;pre&gt;
     * @param baseRequest
     * @param response
     * @param result 需要返回给客户的结果
     * @throws IOException
     * 将结果 result 返回给客户
     * &lt;/pre&gt;
     */
    public static void print(Request baseRequest, HttpServletResponse response,
            String result) throws IOException {
        response.setContentType("text/json;charset=utf-8");
        response.setStatus(HttpServletResponse.SC_OK);
        baseRequest.setHandled(true);
        response.getWriter().println(result);
    }
    

    /**
     * 直接输出 json 字符串
     * 
     * @param json
     */
    public static void printToJson(String json, HttpServletResponse response) {
        try {
            response.setCharacterEncoding("UTF-8");
            response.setContentType("text/json");
            response.setDateHeader("Expires", 0);
            PrintWriter out = response.getWriter();
            out.print(json);
            out.flush();
            out.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
</pre> 
 <p>&nbsp;</p> 
 <p>源码详见附件</p> 
 <p>&nbsp;</p> 
 <p>我还有一篇问题，是用jetty和spring结合的：&nbsp;</p> 
 <h3 style="font-size: 16px; padding-top: 10px;"><a style="color: #108ac6; text-decoration: underline;" href="/blog/2068591">嵌入jetty的springMVC可运行jar的REST+</a></h3> 
 <p>关于嵌入式 jetty 更多的内容请参考：<a href="http://wiki.eclipse.org/Jetty/Tutorial/Embedding_Jetty">&nbsp;http://wiki.eclipse.org/Jetty/Tutorial/Embedding_Jetty</a></p> 
 <p>&nbsp;</p> 
</div>