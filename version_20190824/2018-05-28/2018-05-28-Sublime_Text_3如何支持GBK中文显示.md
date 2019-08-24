#Sublime Text 3如何支持GBK中文显示
###发表时间：2018-05-28
###分类：sublime,经验,mac
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2423692" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2423692</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <div class="quote_title">
  原文 写道
 </div> 
 <div class="quote_div">
  之前安装了Sublime Text 3之后，打开包含中文的文档发现中文乱码，刚开始不在乎，因为当时中文是注释。可是以后肯定会涉及到中文的文档，我不想因为此就放弃Sublime投向Notepad++的怀抱，倒不是因为Notepad++不好，而是因为它不夸平台。
  <br>
  <br> 在一番搜索之后，都说安装GBK Encoding Support，可是在安装了Package Control之后，选择Install Package发现根本没有GBK Support Encoding，但是官方网站的列表里是有这个支持的，未提供下载连接，很是郁闷，最终在一篇博客里看到了相关的介绍，给出了gbk4subl插件的链接，但是大家都知道github上只能下载压缩包，无法直接下载可用的Package。在下载了zip包无解后，盯着Package control看了一下，发现有add repository选项，相信有linux使用经验的人对此肯定很熟悉，这不就是添加源吗，灵光一现，赶紧试一下，把源添加上去，还真就行了。
  <br>
  <br> GBK4subl的github地址：https://github.com/jeewood/gbk4subl。安装好Package control后按control + ·（键盘左上角的那个和波浪线在一起的点），选择第二个add repository，添加上述gbk4subl地址，然后安装gbk4subl重启sublim就可以支持中文了。
 </div> 
 <p>&nbsp;引用地址：&nbsp;<a href="https://blog.csdn.net/xinwenfei/article/details/39312269">https://blog.csdn.net/xinwenfei/article/details/39312269</a></p> 
</div>