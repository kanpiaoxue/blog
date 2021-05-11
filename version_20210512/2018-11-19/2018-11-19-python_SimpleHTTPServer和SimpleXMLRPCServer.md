#python SimpleHTTPServer和SimpleXMLRPCServer
###发表时间：2018-11-19
###分类：python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434037" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434037</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">python有2个非常有用的内置服务器：</p> 
 <p style="font-size: 14px;">SimpleHTTPServer和SimpleXMLRPCServer</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">指定端口：</p> 
 <pre name="code" class="java">python -m SimpleHTTPServer 8000</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">在python3中上面的命令行是不能用，因为SimpleHTTPServer 在python3中被移动到了&nbsp;http.server 中。因此python3的调用方式如下：</p> 
 <pre name="code" class="java">python3 -m http.server 8000</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">官方文档：&nbsp;<a href="https://docs.python.org/2/library/simplehttpserver.html">https://docs.python.org/2/library/simplehttpserver.html</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <div class="admonition note" style="margin-top: 10px; margin-bottom: 10px; padding: 7px; background-color: #eeeeee; border: 1px solid #cccccc; font-family: sans-serif; font-size: 16px;"> 
  <p class="admonition-title" style="margin-right: 10px; margin-bottom: 5px; font-weight: bold; display: inline; text-align: justify; line-height: 20.8px;">Note</p> &nbsp; 
  <p style="text-align: justify; line-height: 20.8px; margin-bottom: 5px; display: inline;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background: #d6d6d6; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module has been merged into&nbsp;<code class="xref py py-mod docutils literal notranslate" style="background: #d6d6d6; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">http.server</span></code>&nbsp;in Python 3. The&nbsp;<a class="reference internal" style="color: #355f7c;" href="https://docs.python.org/2/glossary.html#term-2to3"><span class="xref std std-term">2to3</span></a>&nbsp;tool will automatically adapt imports when converting your sources to Python 3.</p> 
 </div> 
 <div class="admonition warning" style="margin-top: 10px; margin-bottom: 10px; padding: 7px; background-color: #ffe4e4; border: 1px solid #ff6666; font-family: sans-serif; font-size: 16px;"> 
  <p class="admonition-title" style="margin-right: 10px; margin-bottom: 5px; font-weight: bold; display: inline; text-align: justify; line-height: 20.8px;">Warning</p> &nbsp; 
  <p style="text-align: justify; line-height: 20.8px; margin-bottom: 5px; display: inline;"><a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background: #efc2c2; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;is not recommended for production. It only implements basic security checks.</p> 
 </div> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">《Serving Files with Python's SimpleHTTPServer Module》：<a href="https://stackabuse.com/serving-files-with-pythons-simplehttpserver-module/">https://stackabuse.com/serving-files-with-pythons-simplehttpserver-module/</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>