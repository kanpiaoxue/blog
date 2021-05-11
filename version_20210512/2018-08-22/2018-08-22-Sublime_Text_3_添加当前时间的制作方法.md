#Sublime Text 3 添加当前时间的制作方法
###发表时间：2018-08-22
###分类：sublime,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2429089" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2429089</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">参考地址：&nbsp;</p> 
 <p style="font-size: 14px;"><a href="https://blog.csdn.net/BTUJACK/article/details/80711764">https://blog.csdn.net/BTUJACK/article/details/80711764</a></p> 
 <p><a href="https://blog.csdn.net/sshfl_csdn/article/details/46415551">https://blog.csdn.net/sshfl_csdn/article/details/46415551</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p>第一步:制作插件：</p> 
 <p>&nbsp;</p> 
 <p>插件放入位置：</p> 
 <p>(Windows)C:\Users\Z003TESJ.AD005\AppData\Roaming\Sublime Text 3\Packages\User</p> 
 <p>(Mac)&nbsp;~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User</p> 
 <p>&nbsp;</p> 
 <p>插件内容：</p> 
 <p>&nbsp;</p> 
 <ol class="hljs-ln" style="margin-bottom: 0px; border-collapse: collapse; overflow: hidden; width: 967px;"> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;"> 
     <span class="hljs-keyword" style="color: #c678dd;">import</span> datetime
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;"> 
     <span class="hljs-keyword" style="color: #c678dd;">import</span> sublime_plugin
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     <span class="hljs-class"><span class="hljs-keyword" style="color: #c678dd;">class</span> <span class="hljs-title" style="color: #e6c07b;">AddCurrentTimeCommand</span><span class="hljs-params">(sublime_plugin.TextCommand)</span>:</span>
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     <span class="hljs-function"><span class="hljs-keyword" style="color: #c678dd;">def</span> <span class="hljs-title" style="color: #61aeee;">run</span><span class="hljs-params">(self, edit)</span>:</span>
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     self.view.run_command(
     <span class="hljs-string" style="color: #98c379;">"insert_snippet"</span>,
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     {
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;"> 
     <span class="hljs-string" style="color: #98c379;">"contents"</span>: 
     <span class="hljs-string" style="color: #98c379;">"%s"</span> % datetime.datetime.now().strftime(
     <span class="hljs-string" style="color: #98c379;">"#%Y-%m-%d %X %B %A the %W week, the %j day SZ"</span>)
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     }
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     )
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;">
    &nbsp;
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     <span class="hljs-comment" style="color: #5c6370; font-style: italic;">#%X 等价于%H:%M:%S</span>
    </div> 
   </div> </li> 
 </ol> 
 <p>&nbsp;</p> 
 <p>第二步：制作快捷键</p> 
 <p>&nbsp;</p> 
 <p>sublime Text-&gt;<span style="font-family: 'Courier New';">Preference → Key Bindings - User:</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>删除所有的东西，然后添加代码：</p> 
 <p>&nbsp;</p> 
 <ol class="hljs-ln" style="margin-bottom: 0px; border-collapse: collapse; overflow: hidden;"> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     [
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     { 
     <span class="hljs-string" style="color: #98c379;">"keys"</span>: [
     <span class="hljs-string" style="color: #98c379;">"ctrl+shift+;"</span>], 
     <span class="hljs-string" style="color: #98c379;">"command"</span>: 
     <span class="hljs-string" style="color: #98c379;">"add_current_time"</span> }
    </div> 
   </div> </li> 
  <li style="margin-bottom: 0px; margin-left: 0px; height: 22px;"> 
   <div class="hljs-ln-numbers" style="padding: 0px; margin: 0px; float: left; height: 22px; width: 24px; border-right: 1px solid #c5c5c5;">
    &nbsp;
   </div> 
   <div class="hljs-ln-code" style="padding: 0px; margin: 0px 0px 0px 8px; float: left; height: 22px;"> 
    <div class="hljs-ln-line" style="padding: 0px; margin: 0px;">
     ]
    </div> 
   </div> </li> 
 </ol> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>最后保存，重启软件，建立一个文档，同时按下：ctrl, shift, ;三个键，就会出现如下效果：</p> 
 <p>&nbsp;</p> 
 <p>#2018-06-16 10:46:08 08 June Saturday the 24 week, the 167 day SZ</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>如果你想创新，打造自己的模式，参考这里进行修改.</p> 
 <p>&nbsp;</p> 
 <p>python中时间日期格式化符号：</p> 
 <ul> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%y 两位数的年份表示（00-99）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%Y 四位数的年份表示（000-9999）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%m 月份（01-12）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%d 月内中的一天（0-31）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%H 24小时制小时数（0-23）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%I 12小时制小时数（01-12）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%M 分钟数（00=59）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%S 秒（00-59）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%a 本地简化星期名称</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%A 本地完整星期名称</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%b 本地简化的月份名称</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%B 本地完整的月份名称</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%c 本地相应的日期表示和时间表示</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%j 年内的一天（001-366）</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%p 本地A.M.或P.M.的等价符</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%U 一年中的星期数（00-53）星期天为星期的开始</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%w 星期（0-6），星期天为星期的开始</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%W 一年中的星期数（00-53）星期一为星期的开始</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%x 本地相应的日期表示</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%X 本地相应的时间表示</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%Z 当前时区的名称</li> 
  <li style="margin-top: 8px; margin-bottom: 0px; margin-left: 32px;">%% %号本身</li> 
 </ul> 
</div>