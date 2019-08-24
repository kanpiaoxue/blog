#mac crontab的使用
###发表时间：2018-06-29
###分类：mac,非技术,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2425852" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2425852</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>启用Mac的crontab，需要添加文件：</p> 
 <pre name="code" class="java">$sudo touch /etc/crontab</pre> 
 <p>&nbsp;</p> 
 <p id="crontab的文件格式" style="margin: 10px auto; font-family: 'Helvetica Neue', Helvetica, Verdana, Arial, sans-serif;"><strong style="margin: 0px; padding: 0px;">crontab的文件格式</strong></p> 
 <pre><code style="margin: 0px; padding: 0px;">    * 第1列分钟0～59
    * 第2列小时0～23（0表示子夜）
    * 第3列日1～31
    * 第4列月1～12
    * 第5列星期0～7（0和7表示星期天）
    * 第6列要运行的命令</code></pre> 
</div>