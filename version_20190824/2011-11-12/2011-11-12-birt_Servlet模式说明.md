#birt Servlet模式说明
###发表时间：2011-11-12
###分类：birt
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1255008" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1255008</a>

---

<p> </p>
<pre name="code" class="xml">&lt;!-- Viewer Servlet, Supports SOAP --&gt;
&lt;servlet&gt;
  &lt;servlet-name&gt;ViewerServlet&lt;/servlet-name&gt;
  &lt;servlet-class&gt;org.eclipse.birt.report.servlet.ViewerServlet&lt;/servlet-class&gt;
&lt;/servlet&gt;

&lt;!-- Engine Servlet --&gt;
&lt;servlet&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;servlet-class&gt;org.eclipse.birt.report.servlet.BirtEngineServlet&lt;/servlet-class&gt;
&lt;/servlet&gt;

&lt;!--   

        frameset ---- 采用Ajax框架，可以显示工具条，导航条和TOC面板，实现复杂的操作，

                             如分页处理，导出数据，导出报表，打印等。

                             该模式下会自动生成report document文件(预览report design文件)到特定的目录

                             (用户可以用参数指定，也可以定义在web.xml里)。采用Ajax，速度较慢。

--&gt;

&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;ViewerServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/frameset&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt;

&lt;!--

       run ---- 也采用Ajax框架，但不实现frameset的复杂功能，

                   不会生成临时的report document文件(预览report design文件)，也不支持分页，

                   这个主要是应用在BIRT Designer里的preview tab里，

                   可以支持cancel操作，其它不怎么常用。采用Ajax，速度较慢。

--&gt;
&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;ViewerServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/run&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt;


&lt;!-- 

       preview --- 没有用到Ajax框架，直接调用底层Engine API对报表进行render，

                         把生成的报表内容直接输出到浏览器。

                         这种模式和run模式调用的是相同的Engine API，

                         唯一区别在于run采用Ajax获取报表内容，而preview直接输出到浏览器。

                         如果要支持分页，用户需要在URL上定义__page和__pagerange参数。

                         需要特别说明的是，在这几种预览模式中，preview的速度是最快的。  

--&gt;
&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/preview&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt;

&lt;!-- 

      download --- 用于导出报表数据，

                           当你使用frameset工具条里的导出数据功能时，会用到这个模式。

--&gt;

&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/download&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt;

  

&lt;!--  

     parameter --- 该模式主要用于生成一个参数对话框，一般用户不常用，

                           用户可以直接通过提供的JSP Tag--parameterPage去实现参数对话框，不需要直接调用。

--&gt;

&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/parameter&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt; 

&lt;!-- 

      document --- 该模式主要是为了从report design文件生成report document文件。

                           用户可以在URL上提定document文件生成存放的路径(存放在server端)，如果未指定，

                           会直接生成rptdocument发送到客户端浏览器，用户可以下载到客户端。 

--&gt;

&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/document&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt;

&lt;!-- 

      output --- 该模式类似于frameset，会自动生成report document文件(预览report design文件)，

                      区别在于output不采用Ajax，而是将生成的报表内容直接输出到浏览器。

--&gt; 

&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/output&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt; 


&lt;!-- 

      extract--- 。

--&gt; 
&lt;servlet-mapping&gt;
  &lt;servlet-name&gt;EngineServlet&lt;/servlet-name&gt;
  &lt;url-pattern&gt;/extract&lt;/url-pattern&gt;
&lt;/servlet-mapping&gt;
</pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>引用来源：&nbsp;</p>
<p><a href="http://www.birthome.cn/read.php?tid=1650">http://www.birthome.cn/read.php?tid=1650</a></p>
<p><span style="white-space: pre;"> </span></p>