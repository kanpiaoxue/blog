#Python的包管理工具pip的安装与使用
###发表时间：2017-08-21
###分类：python,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2390483" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2390483</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>转载地址：&nbsp;<a href="http://blog.csdn.net/liuchunming033/article/details/39578019">http://blog.csdn.net/liuchunming033/article/details/39578019</a></p> 
 <p>&nbsp;</p> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"><span style="font-size: 18px;">【Preface】</span></h1> 
 <p style="font-family: Arial;"><a class="replace_word" style="color: #df3434; font-weight: bold;" title="Python知识库" href="http://lib.csdn.net/base/python" target="_blank">Python</a>有两个著名的包管理工具easy_install.py和pip。在Python2.7的安装包中，easy_install.py是默认安装的，而pip需要我们手动安装。</p> 
 <p style="font-family: Arial;">pip可以运行在Unix/<a class="replace_word" style="color: #df3434; font-weight: bold;" title="Linux知识库" href="http://lib.csdn.net/base/linux" target="_blank">Linux</a>, OS X, and Windows平台上，支持CPython versions 2.6, 2.7, 3.1, 3.2, 3.3, 3.4 and also pypy.</p> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"> <a style="color: #ff9900;" name="t1" target="_blank"></a><span style="font-size: 18px;">【Download】</span> </h1> 
 <p style="font-family: Arial;">下载pip的安装包<a class="reference external" style="color: #ff9900;" href="https://bootstrap.pypa.io/get-pip.py" target="_blank">get-pip.py</a>，下载地址：<a style="color: #ff9900;" href="https://pip.pypa.io/en/latest/installing.html#id7" target="_blank">https://pip.pypa.io/en/latest/installing.html#id7</a></p> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"> <a style="color: #ff9900;" name="t2" target="_blank"></a><span style="font-size: 18px;">【Install pip on Windows】</span> </h1> 
 <p style="font-family: Arial;">从pip v1.5.1开始，安装变得很简单，直接以管理员身份，在get-pip.py所在的目录下运行</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">python&nbsp;get-pip.py&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">执行完成后，在<a class="replace_word" style="color: #df3434; font-weight: bold;" title="Python知识库" href="http://lib.csdn.net/base/python" target="_blank">python</a>的安装目录下的Scripts子目录下，可以看到pip.exe、pip2.7.exe、pip2.exe等，这就表示pip安装成功了。</p> 
 <p style="font-family: Arial;">注意：要想能在命令行上直接运行pip程序，需要scripts这个目录加入到环境变量PATH中。</p> 
 <p style="font-family: Arial;">pip安装的时候还可以使用安装选项进行安装，比如指定get-pip.py所在的位置：</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">python&nbsp;get-pip.py&nbsp;--no-index&nbsp;--find-links=c:\downloads&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"> <a style="color: #ff9900;" name="t3" target="_blank"></a><span style="font-size: 18px;">【Install pip on Linux】</span> </h1> 
 <p style="font-family: Arial;">在<a class="replace_word" style="color: #df3434; font-weight: bold;" title="Linux知识库" href="http://lib.csdn.net/base/linux" target="_blank">linux</a>，使用对应Linux发行版上的包管理工具，可以很方便的进行安装。例如：</p> 
 <p style="font-family: Arial;">On Debian and Ubuntu:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">sudo&nbsp;apt-get&nbsp;install&nbsp;python-pip&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">On Fedora:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">sudo&nbsp;yum&nbsp;install&nbsp;python-pip&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"> <a style="color: #ff9900;" name="t4" target="_blank"></a><span style="font-size: 18px;">【Upgrade pip】</span> </h1> 
 <p style="font-family: Arial;">On Linux or OS X:&nbsp;</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;install&nbsp;-U&nbsp;pip&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">&nbsp;On Windows&nbsp;<a id="id6" class="footnote-reference" style="color: #ff9900;" href="https://pip.pypa.io/en/latest/installing.html#id11" target="_blank"></a>：</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">python&nbsp;-m&nbsp;pip&nbsp;install&nbsp;-U&nbsp;pip&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"> <a style="color: #ff9900;" name="t5" target="_blank"></a><span style="font-size: 18px;">&nbsp;【Usage】</span> </h1> 
 <p style="font-family: Arial;">Install a package from&nbsp;<a class="reference external" style="color: #ff9900;" href="http://pypi.python.org/pypi/" target="_blank">PyPI</a>:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;install&nbsp;SomePackage&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">安装特定版本的package，通过使用==, &gt;=, &lt;=, &gt;, &lt;来指定一个版本号。<br>pip install 'Markdown&lt;2.0'<br>pip install 'Markdown&gt;2.0,&lt;2.0.3</p> 
 <p style="font-family: Arial;">如果有requirement的话，直接pip install -r requirements.txt就可以安装所有的了。</p> 
 <p style="font-family: Arial;">Uninstall a package:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;uninstall&nbsp;SomePackage&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">Upgrade a package:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;install&nbsp;--upgrade&nbsp;SomePackage&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">Show what files were installed:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;show&nbsp;--files&nbsp;SomePackage&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">List what packages are outdated:</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;list&nbsp;--outdated&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <h1 style="margin-bottom: 0px; font-family: Arial;"> <a style="color: #ff9900;" name="t6" target="_blank"></a><span style="font-size: 18px;">【Practice】</span> </h1> 
 <p style="font-family: Arial;">install selenium on windows 7：</p> 
 <p style="font-family: Arial;"><img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20140926143238734?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1Y2h1bm1pbmcwMzM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""></p> 
 <p style="font-family: Arial;">验证，打开始--所有程序--Python 2.7 ---IDLE (Python GUI)，输入以下代码，并执行如果不报错，就表示selenium安装成功了。</p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: #006699; background-color: inherit; font-weight: bold;">from</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;selenium&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: #006699; background-color: inherit; font-weight: bold;">import</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;webdriver&nbsp;&nbsp;</span></span></li> 
   <li style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; background-color: #f8f8f8; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: #006699; background-color: inherit; font-weight: bold;">from</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;selenium.common.exceptions&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: #006699; background-color: inherit; font-weight: bold;">import</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;TimeoutException&nbsp;&nbsp;</span></span></li> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: #006699; background-color: inherit; font-weight: bold;">from</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;selenium.webdriver.support.ui&nbsp;</span><span class="keyword" style="margin: 0px; padding: 0px; border: none; color: #006699; background-color: inherit; font-weight: bold;">import</span><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">&nbsp;WebDriverWait&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;"><span style="font-size: 12px;">还有一种方法，就是执行</span></p> 
 <div class="dp-highlighter bg_python" style="font-family: Consolas, 'Courier New', Courier, mono, serif; font-size: 12px; background-color: #e7e5dc; width: 936.531px; padding-top: 1px; margin: 18px 0px !important;"> 
  <div class="bar" style="padding-left: 45px;"> 
   <div class="tools" style="padding: 3px 8px 10px 10px; font-size: 9px; line-height: normal; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; color: silver; background-color: #f8f8f8; border-left: 3px solid #6ce26c; border-right: 1px solid #e7e5dc;"> 
    <strong>[python]</strong>&nbsp;
    <a class="ViewSource" style="" title="view plain" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">view plain</a>
    <span><span>&nbsp;<a class="CopyToClipboard" style="" title="copy" href="http://blog.csdn.net/liuchunming033/article/details/39578019" target="_blank">copy</a></span></span> 
    <div style="width: 18px; height: 18px;">
     &nbsp;
    </div> 
   </div> 
  </div> 
  <ol class="dp-py" style="border-top: none; border-right: 1px solid #e7e5dc; border-bottom: none; border-left: none; background-color: #ffffff; color: #5c5c5c; margin-bottom: 1px !important; margin-left: 45px !important;" start="1"> 
   <li class="alt" style="border-top: none; border-right: none; border-bottom: none; border-left: 3px solid #6ce26c; color: inherit; line-height: 18px; margin-bottom: 0px !important; margin-left: 0px !important; padding-right: 3px !important; padding-left: 10px !important;"><span style="margin: 0px; padding: 0px; border: none; color: black; background-color: inherit;"><span style="margin: 0px; padding: 0px; border: none; background-color: inherit;">pip&nbsp;show&nbsp;--files&nbsp;selenim&nbsp;&nbsp;</span></span></li> 
  </ol> 
 </div> 
 <p style="font-family: Arial;">执行结果是列出selunium包的所有文件。</p> 
 <p style="font-family: Arial;"><br><img style="border-style: none; max-width: 100%;" src="http://img.blog.csdn.net/20141031111448453?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1Y2h1bm1pbmcwMzM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt=""></p> 
 <p style="font-family: Arial;"><span style="font-size: 18px;">【References】</span></p> 
 <p style="font-family: Arial;"><a style="color: #ff9900;" href="https://pypi.python.org/pypi/pip" target="_blank">https://pypi.python.org/pypi/pip</a></p> 
 <p>&nbsp;</p> 
</div>