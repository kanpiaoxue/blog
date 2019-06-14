#Spring mvc controller AOP 失效问题
###发表时间：2015-11-20
###分类：Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2258193" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2258193</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p><a href="http://stackoverflow.com/questions/17834958/spring-aop-is-not-working-in-with-mvc-structure?rq=1">&nbsp;http://stackoverflow.com/questions/17834958/spring-aop-is-not-working-in-with-mvc-structure?rq=1</a>&nbsp;</p> 
 <p id="breadcrumbs" style="font-size: 12px; line-height: 18px; padding: 6px 15px; border-width: 1px 1px 0px; border-top-style: solid; border-right-style: solid; border-left-style: solid; border-top-color: #ebebeb; border-right-color: #ebebeb; border-left-color: #ebebeb; font-family: arial, helvetica, sans-serif; color: #666666; background-position: 0% 100%;">You are here:&nbsp;<a style="color: #336699;" href="http://mergetag.com/">Home</a>&nbsp;»&nbsp;<a style="color: #336699;" href="http://mergetag.com/category/development/">Development</a>&nbsp;»&nbsp;<strong>Spring AOP Advice on Annotated Controllers</strong></p> 
 <div class="singlepost" style="color: #666666; font-family: arial, helvetica, sans-serif; font-size: 12px; line-height: 18px;"> 
  <div id="post-main-630" class="post" style="margin: 0px 0px 20px; padding: 0px; clear: both;"> 
   <div class="entry" style="margin: 0px 0px 15px; padding: 15px; border: 1px solid #ebebeb;"> 
    <h1 class="post-title single" style=""><a style="color: #333333;" title="Permanent Link to Spring AOP Advice on Annotated Controllers" href="http://mergetag.com/spring-aop-advice-on-annotated-controllers-2/" rel="bookmark">Spring AOP Advice on Annotated Controllers</a></h1> 
    <div class="meta single" style="margin: 0px 0px 15px; padding: 0px 0px 5px; font-size: 8pt; border-bottom-width: 1px; border-bottom-style: dotted; border-bottom-color: #dddddd;"> 
     <span class="meta-author"><a style="color: #336699;" title="Posts by Paco" href="http://mergetag.com/author/Paco/" rel="author">Paco</a>&nbsp;|&nbsp;</span>
     <span class="meta-date">April 2, 2013 </span>
     <span class="meta-comments">|&nbsp;<a style="color: #336699;" title="Comments for Spring AOP Advice on Annotated Controllers" href="http://mergetag.com/spring-aop-advice-on-annotated-controllers-2/#comments" rel="bookmark">1 Comment</a></span> 
    </div> 
    <p style="margin-bottom: 15px; text-align: justify;"><a style="color: #336699;" href="http://mergetag.com/wp-content/uploads/2013/04/aspect.jpg"><img class="alignleft size-thumbnail wp-image-621" style="border: 1px solid #ebebeb; float: left; max-width: 97%; padding: 3px; height: auto; clear: left; margin: 0px 10px 15px 0px;" title="AOP Definition" src="http://mergetag.com/wp-content/uploads/2013/04/aspect-150x150.jpg" alt="AOP Definition" width="150" height="150"></a>Spring AOP (<strong>Aspect-oriented programming</strong>) framework is used to modularize cross-cutting concerns in aspects. If you want a more simple definition you can think of them as a&nbsp;<strong>Interceptor but with more options configurations possible. &nbsp;</strong>In Spring there are two different constructs that get called “interceptors”. First, there are&nbsp;<a style="color: #336699;" href="http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/mvc.html#mvc-handlermapping-interceptor" rel="nofollow">Handler Interceptors</a>, which are part of the Spring MVC framework (and similar to Interceptors in Struts 2), and give you the ability to add interceptor logic to requests. &nbsp;But you also have Method Interceptors, which are part of the&nbsp;<a style="color: #336699;" href="http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/aop.html" rel="nofollow">Spring AOP</a>&nbsp;framework. These are much more general mechanism than Handler Interceptors, but also potentially more complex. In AOP terminology, such interceptors provide a means of coding the “aspects” you’re talking about.</p> 
    <p style="margin-bottom: 15px; text-align: justify;">In this article we are not going to cover how Spring AOP work, I am going to present the solution to an error that could appear when you want to use advices with controller methods in Spring 3 using annotation and non declarative configurations.</p> 
    <h1 style="">¿What is the problem?</h1> 
    <p style="margin-bottom: 15px;">You need to make some processing (before and/or after) the execution of a controller. You want to use the AspectJ annotation in Spring to do that. Your code could be something like:</p> 
    <div class="wp_syntax" style="color: #110000; border: 1px solid silver; margin: 0px 0px 1.5em; width: 918.71875px; background-color: #f9f9f9;"> 
     <table style="border-collapse: collapse !important; margin: 0px !important; max-width: 100%; overflow: hidden; border: none !important; padding: 0px !important; width: 918px;">
      <tbody>
       <tr style="background: #f5f5f5;"> 
        <td class="line_numbers" style="border: none !important; padding: 0px !important; vertical-align: top !important;"> <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
</pre> </td> 
        <td class="code" style=""> <pre class="java">@Controller&nbsp;
<span style="font-weight: bold;">public</span> <span style="font-weight: bold;">class</span> TestController <span style="color: #009900;">{</span>&nbsp;
&nbsp;
@RequestMapping<span style="color: #009900;">(</span><span style="color: #0000ff;">"/test.fo"</span><span style="color: #009900;">)</span>&nbsp;
<span style="font-weight: bold;">public</span> <span style="color: #003399;">String</span> test<span style="color: #009900;">(</span>ModelMap model<span style="color: #009900;">)</span>&nbsp;
&nbsp;
<span style="color: #009900;">{</span>&nbsp;
&nbsp;
model <span style="color: #339933;">=</span> <span style="font-weight: bold;">new</span> ModelMap<span style="color: #009900;">(</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>&nbsp;
&nbsp;
<span style="font-weight: bold;">return</span> <span style="color: #0000ff;">"test.jsp"</span><span style="color: #339933;">;</span>&nbsp;
&nbsp;
<span style="color: #009900;">}</span>
<span style="color: #009900;">}</span></pre> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <p style="margin-bottom: 15px;">The aspect has to include an advice which will be executed before and after the controller is invoked by a request. Using annotation your aspect could be something similar to:</p> 
    <div class="wp_syntax" style="color: #110000; border: 1px solid silver; margin: 0px 0px 1.5em; width: 918.71875px; background-color: #f9f9f9;"> 
     <table style="border-collapse: collapse !important; margin: 0px !important; max-width: 100%; overflow: hidden; border: none !important; padding: 0px !important; width: 918px;">
      <tbody>
       <tr style="background: #f5f5f5;"> 
        <td class="line_numbers" style="border: none !important; padding: 0px !important; vertical-align: top !important;"> <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
</pre> </td> 
        <td class="code" style=""> <pre class="java">@Aspect
<span style="font-weight: bold;">public</span> <span style="font-weight: bold;">class</span> StateAspectImpl <span style="font-weight: bold;">extends</span> StateAspectI<span style="color: #009900;">{</span>
&nbsp;
<span style="font-weight: bold;">private</span> <span style="font-weight: bold;">static</span> <span style="font-weight: bold;">final</span> Log LOG <span style="color: #339933;">=</span> LogFactory.<span style="color: #006633;">getLog</span><span style="color: #009900;">(</span>StateAspectImpl.<span style="font-weight: bold;">class</span><span style="color: #009900;">)</span><span style="color: #339933;">;</span>
&nbsp;
@Pointcut<span style="color: #009900;">(</span><span style="color: #0000ff;">"within(@org.springframework.stereotype.Controller *)"</span><span style="color: #009900;">)</span> <span style="color: #666666; font-style: italic;">//we define a pointcut for all controllers</span>
<span style="font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> classPointcut<span style="color: #009900;">(</span><span style="color: #009900;">)</span> <span style="color: #009900;">{</span><span style="color: #009900;">}</span>
&nbsp;
@Pointcut<span style="color: #009900;">(</span><span style="color: #0000ff;">"execution(* *getViewNew(..))"</span><span style="color: #009900;">)</span> <span style="color: #666666; font-style: italic;">// the methods that ends in getViewNew are join to this pointcut</span>
<span style="font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> methodPointcut<span style="color: #009900;">(</span><span style="color: #009900;">)</span> <span style="color: #009900;">{</span><span style="color: #009900;">}</span>
&nbsp;
<span style="color: #008000; font-style: italic; font-weight: bold;">/**
* Operations*/</span>
&nbsp;
@Around<span style="color: #009900;">(</span><span style="color: #0000ff;">"classPointcut() &amp;&amp; methodPointcut() &amp;&amp; args(request,modelMap)"</span><span style="color: #009900;">)</span>
<span style="font-weight: bold;">public</span> ModelMap recoverStateView<span style="color: #009900;">(</span>ProceedingJoinPoint joinPoint, HttpServletRequest request, ModelMap modelMap<span style="color: #009900;">)</span> <span style="font-weight: bold;">throws</span> <span style="color: #003399;">Throwable</span> <span style="color: #009900;">{</span>
&nbsp;
<span style="color: #666666; font-style: italic;">//the operations that you want execute</span>
&nbsp;
<span style="color: #009900;">}</span></pre> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <p style="margin-bottom: 15px;"><strong>So you want to advice all the methods that contains getViewNew in the name from all classes annotated with @Controller.&nbsp;</strong>When you execute this code deploying the app in a server it&nbsp;doesn’t&nbsp;work and&nbsp;don’t&nbsp;raise any error or exception.</p> 
    <h1 style="">The cause is…</h1> 
    <p style="margin-bottom: 15px;">After debugging the code I realized that the advice is never been executed. So I tried to look for a solution in&nbsp;<a style="color: #336699;" href="http://stackoverflow.com/">StackOverflow</a>. Some of the question/answer that I find there were:</p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/3310115/spring-aop-advice-on-annotated-controllers">http://stackoverflow.com/questions/3310115/spring-aop-advice-on-annotated-controllers</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/789759/how-can-i-apply-an-aspect-using-annotations-in-spring">http://stackoverflow.com/questions/789759/how-can-i-apply-an-aspect-using-annotations-in-spring</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/9310927/aspect-not-executed-in-spring">http://stackoverflow.com/questions/9310927/aspect-not-executed-in-spring</a></p> 
    <p style="margin-bottom: 15px;">But anyone of these discussion and the solutions that are proposed in, works in my situation. The question that point me in the right direction was:</p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/3991249/how-can-i-combine-aspect-with-controller-in-spring-3">http://stackoverflow.com/questions/3991249/how-can-i-combine-aspect-with-controller-in-spring-3</a></p> 
    <p style="margin-bottom: 15px;">The source of the problem is: Spring AOP is based on a proxy generation, that executed the advices in the pointcuts that you declare.<strong>For&nbsp;accomplish this, the classes that contain the methods that match with the pointcuts which you created (the classes we want to intercept the execution) have to be declared with component scanning in the domain on the DispatcherServlet.</strong></p> 
    <p style="margin-bottom: 15px;">At this point, if your using a xml file to describe the dispatched servlet, like</p> 
    <div class="wp_syntax" style="color: #110000; border: 1px solid silver; margin: 0px 0px 1.5em; width: 918.71875px; background-color: #f9f9f9;"> 
     <table style="border-collapse: collapse !important; margin: 0px !important; max-width: 100%; overflow: hidden; border: none !important; padding: 0px !important; width: 918px;">
      <tbody>
       <tr style="background: #f5f5f5;"> 
        <td class="line_numbers" style="border: none !important; padding: 0px !important; vertical-align: top !important;"> <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
</pre> </td> 
        <td class="code" style=""> <pre class="xml"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">"1.0"</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">"UTF-8"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;web-app</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">"2.4"</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://java.sun.com/xml/ns/j2ee"</span></span>
<span style="color: #009900;"><span style="color: #000066;">xmlns:xsi</span>=<span style="color: #ff0000;">"http://www.w3.org/2001/XMLSchema-instance"</span></span>
<span style="color: #009900;"><span style="color: #000066;">xsi:schemaLocation</span>=<span style="color: #ff0000;">"http://java.sun.com/xml/ns/j2ee</span>
http://java.sun.com/xml/ns/j2ee/web-app_2_4.xsd"<span style="color: #000000; font-weight: bold;">&gt;</span></span>
&nbsp;
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;servlet&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;servlet-name&gt;</span></span>springmvc<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/servlet-name&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;servlet-class&gt;</span></span>org.springframework.web.servlet.DispatcherServlet<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/servlet-class&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;load-on-startup&gt;</span></span>1<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/load-on-startup&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/servlet&gt;</span></span>
&nbsp;
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;servlet-mapping&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;servlet-name&gt;</span></span>springmvc<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/servlet-name&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;url-pattern&gt;</span></span>/<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/url-pattern&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/servlet-mapping&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/web-app&gt;</span></span></pre> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <p style="margin-bottom: 15px;">for the web.xml file, and:</p> 
    <div class="wp_syntax" style="color: #110000; border: 1px solid silver; margin: 0px 0px 1.5em; width: 918.71875px; background-color: #f9f9f9;"> 
     <table style="border-collapse: collapse !important; margin: 0px !important; max-width: 100%; overflow: hidden; border: none !important; padding: 0px !important; width: 1238px;">
      <tbody>
       <tr style="background: #f5f5f5;"> 
        <td class="line_numbers" style="border: none !important; padding: 0px !important; vertical-align: top !important;"> <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
14
15
16
17
18
19
20
21
22
23
24
25
26
27
28
29
30
31
32
33
</pre> </td> 
        <td class="code" style=""> <pre class="xml"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">"1.0"</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">"UTF-8"</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;beans</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">"http://www.springframework.org/schema/beans"</span></span>
<span style="color: #009900;"><span style="color: #000066;">xmlns:xsi</span>=<span style="color: #ff0000;">"http://www.w3.org/2001/XMLSchema-instance"</span> <span style="color: #000066;">xmlns:context</span>=<span style="color: #ff0000;">"http://www.springframework.org/schema/context"</span></span>
<span style="color: #009900;"><span style="color: #000066;">xmlns:mvc</span>=<span style="color: #ff0000;">"http://www.springframework.org/schema/mvc"</span></span>
<span style="color: #009900;"><span style="color: #000066;">xsi:schemaLocation</span>=<span style="color: #ff0000;">"http://www.springframework.org/schema/beans</span>
http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
http://www.springframework.org/schema/mvc
http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
http://www.springframework.org/schema/context
http://www.springframework.org/schema/context/spring-context-3.0.xsd"<span style="color: #000000; font-weight: bold;">&gt;</span></span>
&nbsp;
<span style="color: #808080; font-style: italic;">&lt;!-- not strictly necessary for this example, but still useful, see http://static.springsource.org/spring/docs/3.0.x/spring-framework-reference/html/mvc.html#mvc-ann-controller for more information --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;context:component-scan</span> <span style="color: #000066;">base-package</span>=<span style="color: #ff0000;">"springmvc.web"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
&nbsp;
<span style="color: #808080; font-style: italic;">&lt;!-- the mvc resources tag does the magic --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;mvc:resources</span> <span style="color: #000066;">mapping</span>=<span style="color: #ff0000;">"/resources/**"</span> <span style="color: #000066;">location</span>=<span style="color: #ff0000;">"/resources/"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
&nbsp;
<span style="color: #808080; font-style: italic;">&lt;!-- also add the following beans to get rid of some exceptions --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;bean</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;bean</span></span>
<span style="color: #009900;"><span style="color: #000066;">class</span>=<span style="color: #ff0000;">"org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/bean&gt;</span></span>
&nbsp;
<span style="color: #808080; font-style: italic;">&lt;!-- JSTL resolver --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;bean</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">"viewResolver"</span></span>
<span style="color: #009900;"><span style="color: #000066;">class</span>=<span style="color: #ff0000;">"org.springframework.web.servlet.view.InternalResourceViewResolver"</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"viewClass"</span></span>
<span style="color: #009900;"><span style="color: #000066;">value</span>=<span style="color: #ff0000;">"org.springframework.web.servlet.view.JstlView"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"prefix"</span> <span style="color: #000066;">value</span>=<span style="color: #ff0000;">"/WEB-INF/jsp/"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;property</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">"suffix"</span> <span style="color: #000066;">value</span>=<span style="color: #ff0000;">".jsp"</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/bean&gt;</span></span>
&nbsp;
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/beans&gt;</span></span></pre> </td> 
       </tr>
      </tbody>
     </table> 
    </div> 
    <div style="text-align: justify;">
     for the spring servlet configuration file, the solution works without problem and the advice is executed before and after the method on the Controller classes.
    </div> 
    <p style="margin-bottom: 15px; text-align: justify;">But, what happen if you&nbsp;don’t&nbsp;have a dispatcher servlet&nbsp;XML&nbsp;file and&nbsp;<strong>you are using a class that extends&nbsp;WebMvcConfigurerAdapter to create the servlet configuration. In this case the advice is never executed because the controllers are not created in the domain of the DispatcherServlet</strong>.</p> 
    <h1 style="">The solution is…</h1> 
    <p style="margin-bottom: 15px;">There are two possible solutions to this problem:</p> 
    <ol style="margin-left: 40px;"> 
     <li style="margin-left: 0px;">Change the configuration of your spring application to use a xml configuration instead of the&nbsp;WebMvcConfigurerAdapter.</li> 
     <li style="margin-left: 0px;">Create a aop xml file to declare the class that implement the advice and to configure the aop proxy to make use of this advice.</li> 
    </ol> 
    <div>
     I recommended the second solution in the case in which you were using programmatic configuration of Spring instead of declarative. In that case the xml file could be:
    </div> 
    <div>
     &nbsp;
    </div> 
    <div> 
     <div class="wp_syntax" style="color: #110000; border: 1px solid silver; margin: 0px 0px 1.5em; width: 918.71875px; background-color: #f9f9f9;"> 
      <table style="border-collapse: collapse !important; margin: 0px !important; max-width: 100%; overflow: hidden; border: none !important; padding: 0px !important; width: 1407px;">
       <tbody>
        <tr style="background: #f5f5f5;"> 
         <td class="line_numbers" style="border: none !important; padding: 0px !important; vertical-align: top !important;"> <pre>1
2
3
4
5
6
7
8
9
10
11
12
13
</pre> </td> 
         <td class="code" style=""> <pre class="xml"><span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;?xml</span> <span style="color: #000066;">version</span>=<span style="color: #ff0000;">'1.0'</span> <span style="color: #000066;">encoding</span>=<span style="color: #ff0000;">'UTF-8'</span><span style="color: #000000; font-weight: bold;">?&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;beans</span> <span style="color: #000066;">xmlns</span>=<span style="color: #ff0000;">'http://www.springframework.org/schema/beans'</span></span>
<span style="color: #009900;"><span style="color: #000066;">xmlns:xsi</span>=<span style="color: #ff0000;">'http://www.w3.org/2001/XMLSchema-instance'</span> <span style="color: #000066;">xmlns:aop</span>=<span style="color: #ff0000;">'http://www.springframework.org/schema/aop'</span></span>
<span style="color: #009900;"><span style="color: #000066;">xsi:schemaLocation</span>=<span style="color: #ff0000;">'http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.1.xsd'</span><span style="color: #000000; font-weight: bold;">&gt;</span></span>
&nbsp;
<span style="color: #808080; font-style: italic;">&lt;!-- AOP support --&gt;</span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;bean</span> <span style="color: #000066;">id</span>=<span style="color: #ff0000;">'stateAspectImpl'</span> <span style="color: #000066;">class</span>=<span style="color: #ff0000;">'...ui.aspect.StateAspectImpl'</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;aop:aspectj-autoproxy&gt;</span></span>
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;aop:include</span> <span style="color: #000066;">name</span>=<span style="color: #ff0000;">'stateAspectImpl'</span> <span style="color: #000000; font-weight: bold;">/&gt;</span></span>
&nbsp;
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/aop:aspectj-autoproxy&gt;</span></span>
&nbsp;
<span style="color: #009900;"><span style="color: #000000; font-weight: bold;">&lt;/beans&gt;</span></span></pre> </td> 
        </tr>
       </tbody>
      </table> 
     </div> 
     <p style="margin-bottom: 15px;">The disadvantage of this solution is:&nbsp;<strong>each time you have to create a new advice, you have to remember change the xml file to declare the advice and &nbsp;add the advice to the proxy.</strong></p> 
    </div> 
    <p style="margin-bottom: 15px;">——————————————–</p> 
    <p style="margin-bottom: 15px;">References:</p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://static.springsource.org/spring/docs/3.2.x/spring-framework-reference/html/aop.html">Spring AOP Reference Documentation.</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://www.javacodegeeks.com/2012/09/spring-adding-aop-support.html">Article in Java Geek Codes: a quick tutorial with full code.</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/3310115/spring-aop-advice-on-annotated-controllers">http://stackoverflow.com/questions/3310115/spring-aop-advice-on-annotated-controllers</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/789759/how-can-i-apply-an-aspect-using-annotations-in-spring">http://stackoverflow.com/questions/789759/how-can-i-apply-an-aspect-using-annotations-in-spring</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/9310927/aspect-not-executed-in-spring">http://stackoverflow.com/questions/9310927/aspect-not-executed-in-spring</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/3991249/how-can-i-combine-aspect-with-controller-in-spring-3">http://stackoverflow.com/questions/3991249/how-can-i-combine-aspect-with-controller-in-spring-3</a></p> 
    <p style="margin-bottom: 15px;"><a style="color: #336699;" href="http://stackoverflow.com/questions/1483063/spring-mvc-3-and-handling-static-content-am-i-missing-something">http://stackoverflow.com/questions/1483063/spring-mvc-3-and-handling-static-content-am-i-missing-something</a></p> 
    <p style="margin-bottom: 15px;">&nbsp;</p> 
    <div style="clear: both;">
     &nbsp;
    </div> 
    <p class="tags" style="margin-bottom: 5px; clear: both;"><strong>Tags:&nbsp;</strong><a style="color: #336699;" href="http://mergetag.com/tag/aop/" rel="tag">aop</a>,&nbsp;<a style="color: #336699;" href="http://mergetag.com/tag/featured/" rel="tag">featured</a>,&nbsp;<a style="color: #336699;" href="http://mergetag.com/es/tag/java/" rel="tag">java</a>,&nbsp;<a style="color: #336699;" href="http://mergetag.com/tag/spring/" rel="tag">spring</a></p> 
    <p class="cats" style="margin-bottom: 15px; clear: both;"><strong>Category</strong>:&nbsp;<a style="color: #336699;" href="http://mergetag.com/category/development/" rel="category tag">Development</a>,&nbsp;<a style="color: #336699;" href="http://mergetag.com/category/development/java-development/" rel="category tag">Java</a></p> 
   </div> 
  </div> 
 </div> 
</div>