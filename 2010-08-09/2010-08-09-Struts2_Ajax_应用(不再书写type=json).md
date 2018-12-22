#Struts2 Ajax 应用（不再书写type="json"）
###发表时间：2010-08-09
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/732788" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/732788</a>

---

<p>最近看了一些帖子，发现一些朋友在使用Ajax和Struts2的结合的时候遇到了困惑和问题。特此，我将自己在实际应用中的解决方案拿出来和大家共享。希望可以给那些还没有找到更合适的Ajax方法的朋友提供一些启发。</p>
<p>问题：</p>
<p>struts2 的书籍以及文章中，多数在Ajax应用的时候，要求在struts.xml文件中需要对ajax的返回类型进行配置。如：</p>
<p>type="json"。使用这个配置的时候，必须使用struts2的json插件的jar包。</p>
<p>解决方案：</p>
<p>我给出的方案是：</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp; 不使用struts2的json插件的jar包，不需要配置struts.xml中的type="json"</p>
<p>具体实现如下：</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp; 使用json-lib.jar(下载地址：<a href="http://sourceforge.net/projects/json-lib/files/">http://sourceforge.net/projects/json-lib/files/</a>)，需要的环境和jar包：</p>
<p>Json-lib requires (at least) the following dependencies in your classpath: </p>
<ul> 
 <li>jakarta commons-lang 2.4 </li> 
 <li>jakarta commons-beanutils 1.7.0 </li> 
 <li>jakarta commons-collections 3.2 </li> 
 <li>jakarta commons-logging 1.1.1 </li> 
 <li>ezmorph 1.0.6 </li> 
</ul>
<p>web页面，js里面，我书写的代码（jQuery）：</p>
<p>&nbsp;</p>
<pre name="code" class="js">var options = {
    url: 'test/jsonTest.do',
    type:'POST',
    dataType:'json',//指定返回数据的解析类型，也可以是 xml
    data:{
     name:'lilei',
     sex:'1'
    },
    success:function(rs){
     if(rs.person){
      alert(rs.name + '\t' + rs.sex);
    }
    },
    error: function(rs){},
    timeout:3000
};

$.ajax(options);
</pre>
<p>&nbsp;struts.xml 配置文件：</p>
<pre name="code" class="xml">&lt;package name="test" namespace="/test" extends="struts-default"&gt;
	&lt;action name="jsonTest" class="test.JsonTestAction" method="jsonTest"&gt;
	&lt;!-- 注意，这里我什么都没有写，是空的 因为JsonTestAction里面的jsonTest的返回类型为 void --&gt;
	&lt;/action&gt;
&lt;/package&gt;	</pre>
<p>&nbsp;Action&nbsp; JsonTestAction的代码：</p>
<pre name="code" class="java">public class JsonTestAction extends ActionSupport implements
		ServletResponseAware {
			private HttpServletResponse response;
			
			// -------------- tool methods
			
			
			/**
			 * 注意：因为struts2.xml 里面没有写 &lt;result&gt;&lt;/result&gt; 这个项，所有这里的类型是 void，而不是 String
			 * 
			 *
			 *
			 */
			public void jsonTest(){
				String name = ServletActionContext.getRequest().getParameter("name");
				Integer sex = Integer.valueOf(ServletActionContext.getRequest().getParameter("sex"));
				
				JSONObject json = new JSONObject();
				json.put("name",name);
				if(sex.initValue == 1){
					json.put("sex","男"):
				}else{
					json.put("sex","女"):
				}
				printToJson(json.toString());
			}
			
	/**
	 * 这里我指定了放回的类型 "text/json" 也可以是xml等其他类型
	 * 用response直接将数据打回到页面的 ajax 的请求里面去
	 *
	 */		
	private void printToJson(String jsonStr) {
		try {
			response.setCharacterEncoding("UTF-8");
			response.setContentType("text/json");
			response.setDateHeader("Expires", 0);
			PrintWriter out = response.getWriter();

			out.println(jsonStr);

			out.flush();
			out.close();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	//实现 ServletResponseAware 接口，必须实现的方法
	public void setServletResponse(HttpServletResponse response) {
		this.response = response;
	}
}			 </pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>这样，就可以通过上面的Action类，将所要的数据，通过response直接到回到ajax的请求里面去。</p>
<p>问题解决。</p>
<p>&nbsp;</p>
<p>如果朋友们有更好的方法，请在这里留言。谢谢</p>