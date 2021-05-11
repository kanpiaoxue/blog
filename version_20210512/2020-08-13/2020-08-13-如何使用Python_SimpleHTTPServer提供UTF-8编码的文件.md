#如何使用Python SimpleHTTPServer提供UTF-8编码的文件?
###发表时间：2020-08-13
###分类：python,shell,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2516271" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2516271</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>如何使用Python SimpleHTTPServer提供UTF-8编码的文件?</p> 
 <p>参考资料：&nbsp;<a href="https://stackoverflow.com/questions/15288891/how-can-i-serve-files-with-utf-8-encoding-using-python-simplehttpserver">https://stackoverflow.com/questions/15288891/how-can-i-serve-files-with-utf-8-encoding-using-python-simplehttpserver</a></p> 
 <p>&nbsp;</p> 
 <p>python2</p> 
 <pre name="code" class="python">python -c "import SimpleHTTPServer; m = SimpleHTTPServer.SimpleHTTPRequestHandler.extensions_map; m[''] = 'text/plain'; m.update(dict([(k, v + ';charset=UTF-8') for k, v in m.items()])); SimpleHTTPServer.test();" 8001</pre> 
 <p>&nbsp;</p> 
 <p>python3</p> 
 <pre name="code" class="python">python3 -c "from http.server import test, SimpleHTTPRequestHandler as RH; RH.extensions_map={k:v+';charset=UTF-8' for k,v in RH.extensions_map.items()}; test(RH,port=8002)"</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>原文如下：&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">Had the same problem, the following code worked for me.</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">To start a SimpleHTTPServer with UTF-8 encoding, simply copy/paste the following in terminal (for Python 2).</p> 
 <pre class="lang-py prettyprint prettyprinted"><code style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: transparent; white-space: inherit;"><span class="pln">python </span><span class="pun">-</span><span class="pln">c </span><span class="str">"import SimpleHTTPServer; m = SimpleHTTPServer.SimpleHTTPRequestHandler.extensions_map; m[''] = 'text/plain'; m.update(dict([(k, v + ';charset=UTF-8') for k, v in m.items()])); SimpleHTTPServer.test();"</span></code></pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">Ensure that you have the correct charset in your HTML files beforehand.</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;"><strong style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; line-height: inherit; font-family: inherit; vertical-align: baseline;">EDIT</strong>: Update for Python 3:</p> 
 <pre class="lang-py prettyprint prettyprinted"><code style="margin: 0px; padding: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: transparent; white-space: inherit;"><span class="pln">python3 </span><span class="pun">-</span><span class="pln">c </span><span class="str">"from http.server import test, SimpleHTTPRequestHandler as RH; RH.extensions_map={k:v+';charset=UTF-8' for k,v in RH.extensions_map.items()}; test(RH)"</span></code></pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">The&nbsp;<code>test</code>&nbsp;function also accepts arguments like&nbsp;<code>port</code>&nbsp;and&nbsp;<code>bind</code>&nbsp;so that it's possible to specify the address and the port to listen on.</p> 
 <p>&nbsp;</p> 
</div>