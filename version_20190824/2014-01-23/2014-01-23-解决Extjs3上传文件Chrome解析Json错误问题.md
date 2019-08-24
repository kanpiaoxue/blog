#解决Extjs3上传文件Chrome解析Json错误问题
###发表时间：2014-01-23
###分类：javascript,Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2008665" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2008665</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>今天用ExtJS 3.1 进行文件上传，参照的是它的ext-3.1.1\examples\form\file-upload.js 的例子。用的浏览器是Google的Chrome，发现一个BUG。</p> 
 <p>我的后台程序返回的json是下面的形式：</p> 
 <pre name="code" class="java">{"errors":"","success":true}	</pre> 
 <p>&nbsp;<br>浏览器始终报错，告诉我JSON的格式不正确。一直想不明白为什么。</p> 
 <p>我在Chrome浏览器里面看到返回前台的json就是{"errors":"","success":true}，但是页面就是报错。我怀疑是Ext有问题。</p> 
 <p>我Debug了Ext的js，发现下面的代码有问题：ext-all.js</p> 
 <pre name="code" class="js">Ext.util.JSON = new (function(){
    var useHasOwn = !!{}.hasOwnProperty,
        isNative = function() {
            var useNative = null;

            return function() {
                if (useNative === null) {
                    useNative = Ext.USE_NATIVE_JSON &amp;&amp; window.JSON &amp;&amp; JSON.toString() == '[object JSON]';
                }
        
                return useNative;
            };
        }(),
        pad = function(n) {
            return n &lt; 10 ? "0" + n : n;
        },
        doDecode = function(json){
        		// 这里有问题。我后台返回的是 {"errors":"","success":true}	
        		// 但这里的 json 里面的内容却是： "&lt;pre style="word-wrap: break-word; white-space: pre-wrap;"&gt;{"errors":"","success":true}&lt;/pre&gt;"
        		// 让我百思不得其解。我只好去网上找了一个哥们的代码来救急。Chrome下面是正确的，其他浏览器没测试。请大家注意。
            return eval("(" + json + ')');    
        },
       .... </pre> 
 <p>&nbsp;</p> 
 <p>我在<a href="http://www.oschina.net/code/snippet_590489_24448">&nbsp;http://www.oschina.net/code/snippet_590489_24448</a></p> 
 <p>找了个方法，放在自己的页面里面，就好用了。</p> 
 <p>这段代码是：</p> 
 <pre name="code" class="js">&lt;script type="text/javascript"&gt;
		Ext.USE_NATIVE_JSON = true;
		window.JSON = {
			"stringify":Ext.util.JSON.doEncode,
			"parse":function(json){
				var str = json;
				var spos = str.indexOf("&gt;");
				var epos = 0;
				if(spos != -1){
					 epos = str.indexOf("&lt;",spos);
					
					str = str.substr(spos+1,epos-spos-1); 
				}
				return eval("("+str+")");
			},
			"toString":function(){
				return '[object JSON]';
			}
		};
	&lt;/script&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>