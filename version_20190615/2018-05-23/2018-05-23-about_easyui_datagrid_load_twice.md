#about easyui datagrid load twice
###发表时间：2018-05-23
###分类：javascript,经验,easyui
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2423409" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2423409</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;<strong style="margin: 0px; padding: 0px; border: 0px; font-size: 12.5px; vertical-align: baseline; color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, sans-serif;"><a class="nav" style="margin: 0px; padding: 0px; border: 0px; vertical-align: baseline; background: transparent; color: #333333;" href="https://www.jeasyui.com/forum/index.php?PHPSESSID=7de4q619rld13tpiih3k7i99a2&amp;topic=3720.0">about easyui datagrid in 1.4v load twice</a></strong></p> 
 <p>&nbsp;</p> 
 <p><strong style="margin: 0px; padding: 0px; border: 0px; font-size: 12.5px; vertical-align: baseline; color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, sans-serif;">easyui datagrid 加载数据的时候总是加载2次，这是它的一个BUG。</strong></p> 
 <p><strong style="margin: 0px; padding: 0px; border: 0px; font-size: 12.5px; vertical-align: baseline; color: #333333; font-family: 'Helvetica Neue', Helvetica, Tahoma, sans-serif;">解决方案如下：</strong></p> 
 <p><a href="http://www.jeasyui.com/forum/index.php?topic=3720.0"><strong>http://www.jeasyui.com/forum/index.php?topic=3720.0</strong></a></p> 
 <div class="quote_title">
  原文 写道
 </div> 
 <div class="quote_div">
  Quote from: stworthy on September 03, 2014, 02:05:18 AM
  <br>Make sure you are using the newest patch. Please try to download it from http://www.jeasyui.com/download/downloads/jquery-easyui-1.4-patch.zip.
  <br>
  <br>ok, using jquery-easyui-1.4-patch.js version 20140903 .it's fixed . thanks for your help stworthy and thank you 【aswzen】。
 </div> 
 <p>&nbsp;我在本文的附件中也放了这个补丁的js。</p> 
 <p>我使用的方式是：</p> 
 <pre name="code" class="html">&lt;script type="text/javascript" src="static/js/libs/jquery-easyui/jquery.min.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="static/js/libs/jquery-easyui/jquery.easyui.min.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="static/js/libs/jquery-easyui/jquery.easyui.patch.js"&gt;&lt;/script&gt;
&lt;script type="text/javascript" src="static/js/libs/jquery-easyui/locale/easyui-lang-zh_CN.js"&gt;&lt;/script&gt;</pre> 
 <p>&nbsp;这样就解决了该问题。</p> 
 <p>&nbsp;</p> 
 <p>另外参考地址：&nbsp;<a href="https://www.jeasyui.com/forum/index.php?topic=6803.0">https://www.jeasyui.com/forum/index.php?topic=6803.0</a></p> 
 <p>Latest patch is always using same file name.<br style="font-family: verdana, sans-serif; font-size: 13px;">For example, current patch (for version 1.5.2) is here:<br style="font-family: verdana, sans-serif; font-size: 13px;"><a style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: baseline; color: #0e2d5f; font-family: verdana, sans-serif;" href="http://www.jeasyui.com/download/downloads/jquery-easyui-1.5.2-patch.zip" target="_blank">http://www.jeasyui.com/download/downloads/jquery-easyui-1.5.2-patch.zip</a><br style="font-family: verdana, sans-serif; font-size: 13px;">For 1.3, it will be here:<br style="font-family: verdana, sans-serif; font-size: 13px;"><a style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: baseline; color: #0e2d5f; font-family: verdana, sans-serif;" href="http://www.jeasyui.com/download/downloads/jquery-easyui-1.3-patch.zip" target="_blank">http://www.jeasyui.com/download/downloads/jquery-easyui-1.3-patch.zip</a><br style="font-family: verdana, sans-serif; font-size: 13px;">for 1.3.8, here:<br style="font-family: verdana, sans-serif; font-size: 13px;"><a style="margin: 0px; padding: 0px; border: 0px; font-size: 13px; vertical-align: baseline; color: #0e2d5f; font-family: verdana, sans-serif;" href="http://www.jeasyui.com/download/downloads/jquery-easyui-1.3.8-patch.zip" target="_blank">http://www.jeasyui.com/download/downloads/jquery-easyui-1.3.8-patch.zip</a><br style="font-family: verdana, sans-serif; font-size: 13px;">it is not so hard&nbsp;&nbsp;<img style="margin: 0px; padding: 0px; font-size: 13px; vertical-align: top; max-width: 100%; height: auto; font-family: verdana, sans-serif;" src="http://jeasyui.com/forum/Smileys/default/grin.gif" alt="Grin" border="0"></p> 
 <p>&nbsp;</p> 
 <p>附件中也附录了 1.5.3的补丁文件。【注意】我试了1.5.3的补丁js文件，发现DataGrid的数据还是会load twice。不知道为啥？但是1.4的补丁文件是好用的。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>