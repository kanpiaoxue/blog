#SimpleHTTPServer — Simple HTTP request handler
###发表时间：2018-10-08
###分类：python,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431786" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431786</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>简单示例：</p> 
 <pre name="code" class="java">python -m SimpleHTTPServer 8080</pre> 
 <p>&nbsp;后面的端口不填，会采用默认端口8000。它会将当前所在的文件夹设置为默认的WebRoot的目录，在浏览器敲入本机地址：</p> 
 <pre name="code" class="java">http://localhost:8080</pre> 
 <p>&nbsp;如果当前文件夹有index.html文件，会默认显示该文件；否则，会以文件列表的形式显示目录下所有文件。这样就实现了最基本的文件分享。</p> 
 <p>&nbsp;</p> 
 <p>官网地址：</p> 
 <p>SimpleHTTPServer — Simple HTTP request handler</p> 
 <p><a href="https://docs.python.org/2/library/simplehttpserver.html">https://docs.python.org/2/library/simplehttpserver.html</a></p> 
 <p>&nbsp;</p> 
 <p>原文：</p> 
 <p>&nbsp;</p> 
 <div class="admonition note" style="margin-top: 10px; margin-bottom: 10px; padding: 7px; background-color: #eeeeee; border: 1px solid #cccccc; font-family: sans-serif; font-size: 16px;"> 
  <p class="first admonition-title" style="margin-right: 10px; margin-bottom: 5px; font-weight: bold; display: inline; text-align: justify; line-height: 20.8px;">Note</p> &nbsp; 
  <p class="last" style="text-align: justify; line-height: 20.8px; margin-bottom: 5px; display: inline;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background: #d6d6d6; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module has been merged into&nbsp;<code class="xref py py-mod docutils literal notranslate" style="background: #d6d6d6; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">http.server</span></code>&nbsp;in Python 3. The&nbsp;<a class="reference internal" style="color: #355f7c;" href="https://docs.python.org/2/glossary.html#term-2to3"><span class="xref std std-term">2to3</span></a>&nbsp;tool will automatically adapt imports when converting your sources to Python 3.</p> 
 </div> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module defines a single class,&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPRequestHandler</span></code></a>, which is interface-compatible with&nbsp;<a class="reference internal" style="color: #355f7c;" title="BaseHTTPServer.BaseHTTPRequestHandler" href="https://docs.python.org/2/library/basehttpserver.html#BaseHTTPServer.BaseHTTPRequestHandler"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">BaseHTTPServer.BaseHTTPRequestHandler</span></code></a>.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module defines the following class:</p> 
 <dl class="class" style="margin-bottom: 15px; font-family: sans-serif; font-size: 16px;"> 
  <dt id="SimpleHTTPServer.SimpleHTTPRequestHandler"> 
   <em class="property">class&nbsp;</em>
   <code class="descclassname" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em;">SimpleHTTPServer.</code>
   <code class="descname" style="background-color: transparent; padding: 0px 1px; font-size: 1.2em; font-weight: bold;">SimpleHTTPRequestHandler</code>
   <span class="sig-paren">(</span>
   <em>request</em>,&nbsp;
   <em>client_address</em>,&nbsp;
   <em>server</em>
   <span class="sig-paren">)</span> 
  </dt> 
  <dd style="margin-top: 3px; margin-bottom: 10px; text-align: justify; line-height: 20.8px;"> 
   <p style="line-height: 20.8px;">This class serves files from the current directory and below, directly mapping the directory structure to HTTP requests.</p> 
   <p style="line-height: 20.8px;">A lot of the work, such as parsing the request, is done by the base class&nbsp;<a class="reference internal" style="color: #355f7c;" title="BaseHTTPServer.BaseHTTPRequestHandler" href="https://docs.python.org/2/library/basehttpserver.html#BaseHTTPServer.BaseHTTPRequestHandler"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">BaseHTTPServer.BaseHTTPRequestHandler</span></code></a>. This class implements the&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler.do_GET" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler.do_GET"><code class="xref py py-func docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">do_GET()</span></code></a>&nbsp;and&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler.do_HEAD" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler.do_HEAD"><code class="xref py py-func docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">do_HEAD()</span></code></a>&nbsp;functions.</p> 
   <p style="line-height: 20.8px;">The following are defined as class-level attributes of&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPRequestHandler</span></code></a>:</p> 
   <dl class="attribute" style="margin-bottom: 15px;"> 
    <dt id="SimpleHTTPServer.SimpleHTTPRequestHandler.server_version">
     <code class="descname" style="background-color: transparent; padding: 0px 1px; font-size: 1.2em; font-weight: bold;">server_version</code>
    </dt> 
    <dd style="margin-top: 3px; margin-bottom: 10px; line-height: 20.8px;"></dd> 
   </dl> 
   <p style="line-height: 20.8px;">This will be&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">"SimpleHTTP/"</span>&nbsp;<span class="pre">+</span>&nbsp;<span class="pre">__version__</span></code>, where&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">__version__</span></code>&nbsp;is defined at the module level.</p> 
   <dl class="attribute" style="margin-bottom: 15px;"> 
    <dt id="SimpleHTTPServer.SimpleHTTPRequestHandler.extensions_map">
     <code class="descname" style="background-color: transparent; padding: 0px 1px; font-size: 1.2em; font-weight: bold;">extensions_map</code>
    </dt> 
    <dd style="margin-top: 3px; margin-bottom: 10px; line-height: 20.8px;"> 
     <p style="line-height: 20.8px;">A dictionary mapping suffixes into MIME types. The default is signified by an empty string, and is considered to be&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">application/octet-stream</span></code>. The mapping is used case-insensitively, and so should contain only lower-cased keys.</p> 
    </dd> 
   </dl> 
   <p style="line-height: 20.8px;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPRequestHandler</span></code></a>&nbsp;class defines the following methods:</p> 
   <dl class="method" style="margin-bottom: 15px;"> 
    <dt id="SimpleHTTPServer.SimpleHTTPRequestHandler.do_HEAD"> 
     <code class="descname" style="background-color: transparent; padding: 0px 1px; font-size: 1.2em; font-weight: bold;">do_HEAD</code>
     <span class="sig-paren">(</span>
     <span class="sig-paren">)</span> 
    </dt> 
    <dd style="margin-top: 3px; margin-bottom: 10px; line-height: 20.8px;"> 
     <p style="line-height: 20.8px;">This method serves the&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'HEAD'</span></code>&nbsp;request type: it sends the headers it would send for the equivalent&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">GET</span></code>&nbsp;request. See the&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler.do_GET" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler.do_GET"><code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">do_GET()</span></code></a>&nbsp;method for a more complete explanation of the possible headers.</p> 
    </dd> 
   </dl> 
   <dl class="method" style="margin-bottom: 15px;"> 
    <dt id="SimpleHTTPServer.SimpleHTTPRequestHandler.do_GET"> 
     <code class="descname" style="background-color: transparent; padding: 0px 1px; font-size: 1.2em; font-weight: bold;">do_GET</code>
     <span class="sig-paren">(</span>
     <span class="sig-paren">)</span> 
    </dt> 
    <dd style="margin-top: 3px; margin-bottom: 10px; line-height: 20.8px;"> 
     <p style="line-height: 20.8px;">The request is mapped to a local file by interpreting the request as a path relative to the current working directory.</p> 
     <p style="line-height: 20.8px;">If the request was mapped to a directory, the directory is checked for a file named&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">index.html</span></code>&nbsp;or&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">index.htm</span></code>&nbsp;(in that order). If found, the file’s contents are returned; otherwise a directory listing is generated by calling the&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">list_directory()</span></code>&nbsp;method. This method uses&nbsp;<a class="reference internal" style="color: #355f7c;" title="os.listdir" href="https://docs.python.org/2/library/os.html#os.listdir"><code class="xref py py-func docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">os.listdir()</span></code></a>&nbsp;to scan the directory, and returns a&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">404</span></code>&nbsp;error response if the&nbsp;<code class="xref py py-func docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">listdir()</span></code>&nbsp;fails.</p> 
     <p style="line-height: 20.8px;">If the request was mapped to a file, it is opened and the contents are returned. Any&nbsp;<a class="reference internal" style="color: #355f7c;" title="exceptions.IOError" href="https://docs.python.org/2/library/exceptions.html#exceptions.IOError"><code class="xref py py-exc docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">IOError</span></code></a>&nbsp;exception in opening the requested file is mapped to a&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">404</span></code>,&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'File</span>&nbsp;<span class="pre">not</span>&nbsp;<span class="pre">found'</span></code>&nbsp;error. Otherwise, the content type is guessed by calling the&nbsp;<code class="xref py py-meth docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">guess_type()</span></code>&nbsp;method, which in turn uses the&nbsp;<em>extensions_map</em>&nbsp;variable.</p> 
     <p style="line-height: 20.8px;">A&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'Content-type:'</span></code>&nbsp;header with the guessed content type is output, followed by a&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'Content-Length:'</span></code>&nbsp;header with the file’s size and a&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'Last-Modified:'</span></code>&nbsp;header with the file’s modification time.</p> 
     <p style="line-height: 20.8px;">Then follows a blank line signifying the end of the headers, and then the contents of the file are output. If the file’s MIME type starts with&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">text/</span></code>&nbsp;the file is opened in text mode; otherwise binary mode is used.</p> 
     <p style="line-height: 20.8px;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="test: Regression tests package containing the testing suite for Python." href="https://docs.python.org/2/library/test.html#module-test"><code class="xref py py-func docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">test()</span></code></a>&nbsp;function in the&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module is an example which creates a server using the&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer.SimpleHTTPRequestHandler" href="https://docs.python.org/2/library/simplehttpserver.html#SimpleHTTPServer.SimpleHTTPRequestHandler"><code class="xref py py-class docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPRequestHandler</span></code></a>&nbsp;as the Handler.</p> 
     <div class="versionadded"> 
      <p style="line-height: 20.8px;"><span class="versionmodified" style="font-style: italic;">New in version 2.5:&nbsp;</span>The&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">'Last-Modified'</span></code>&nbsp;header.</p> 
     </div> 
    </dd> 
   </dl> 
  </dd> 
 </dl> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module can be used in the following manner in order to set up a very basic web server serving files relative to the current directory.</p> 
 <div class="highlight-default notranslate" style="font-family: sans-serif; font-size: 16px;"> 
  <div class="highlight" style="background: #eeffcc;"> 
   <pre><span class="kn" style="color: #007020;">import</span> <span class="nn" style="color: #0e84b5;">SimpleHTTPServer</span>
<span class="kn" style="color: #007020;">import</span> <span class="nn" style="color: #0e84b5;">SocketServer</span>

<span class="n">PORT</span> <span class="o" style="color: #666666;">=</span> <span class="mi" style="color: #208050;">8000</span>

<span class="n">Handler</span> <span class="o" style="color: #666666;">=</span> <span class="n">SimpleHTTPServer</span><span class="o" style="color: #666666;">.</span><span class="n">SimpleHTTPRequestHandler</span>

<span class="n">httpd</span> <span class="o" style="color: #666666;">=</span> <span class="n">SocketServer</span><span class="o" style="color: #666666;">.</span><span class="n">TCPServer</span><span class="p">((</span><span class="s2" style="color: #4070a0;">""</span><span class="p">,</span> <span class="n">PORT</span><span class="p">),</span> <span class="n">Handler</span><span class="p">)</span>

<span class="nb" style="color: #007020;">print</span> <span class="s2" style="color: #4070a0;">"serving at port"</span><span class="p">,</span> <span class="n">PORT</span>
<span class="n">httpd</span><span class="o" style="color: #666666;">.</span><span class="n">serve_forever</span><span class="p">()</span>
</pre> 
  </div> 
 </div> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The&nbsp;<a class="reference internal" style="color: #355f7c;" title="SimpleHTTPServer: This module provides a basic request handler for HTTP servers." href="https://docs.python.org/2/library/simplehttpserver.html#module-SimpleHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">SimpleHTTPServer</span></code></a>&nbsp;module can also be invoked directly using the&nbsp;<a class="reference internal" style="color: #355f7c;" href="https://docs.python.org/2/using/cmdline.html#cmdoption-m"><code class="xref std std-option docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">-m</span></code></a>&nbsp;switch of the interpreter with a&nbsp;<code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">port</span>&nbsp;<span class="pre">number</span></code>&nbsp;argument. Similar to the previous example, this serves the files relative to the current directory.</p> 
 <div class="highlight-default notranslate" style="font-family: sans-serif; font-size: 16px;"> 
  <div class="highlight" style="background: #eeffcc;"> 
   <pre><span class="n">python</span> <span class="o" style="color: #666666;">-</span><span class="n">m</span> <span class="n">SimpleHTTPServer</span> <span class="mi" style="color: #208050;">8000</span>
</pre> 
  </div> 
 </div> 
 <div class="admonition seealso" style="margin-top: 10px; margin-bottom: 10px; padding: 7px; background-color: #ffffcc; border: 1px solid #ffff66; font-family: sans-serif; font-size: 16px;"> 
  <p class="first admonition-title" style="margin-right: 10px; margin-bottom: 5px; font-weight: bold; display: inline; text-align: justify; line-height: 20.8px;">See also</p> 
  <dl class="last docutils" style="margin-bottom: 0px;"> 
   <dt style="font-weight: bold;">
    Module&nbsp;
    <a class="reference internal" style="color: #355f7c;" title="BaseHTTPServer: Basic HTTP server (base class for SimpleHTTPServer and CGIHTTPServer)." href="https://docs.python.org/2/library/basehttpserver.html#module-BaseHTTPServer"><code class="xref py py-mod docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em;"><span class="pre">BaseHTTPServer</span></code></a> 
   </dt> 
   <dd style="margin-top: 3px; margin-bottom: 10px; text-align: justify; line-height: 20.8px;">
    Base class implementation for Web server and request handler.
   </dd> 
  </dl> 
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>