#决eclipse中tomcat启动后，tomcat控制台显示红色字体
###发表时间：2012-10-30
###分类：eclipse
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1708727" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1708727</a>

---

<p> </p>
<p style="padding: 0px; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.200000762939453px; text-align: left;">1、使用eclipse-jee-juno中tomcat启动后，它的tomcat控制台显示红色字体，和自己项目的log4j的字体颜色（黑色）不一致，感觉很奇怪。</p>
<p style="padding: 0px; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.200000762939453px;">&nbsp;2、在网上查找到了以下解决办法。</p>
<p style="padding: 0px; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.200000762939453px;">&nbsp; a、tomcat没启动时，双击eclipse下方的servers里面的服务器。</p>
<p style="padding: 0px; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.200000762939453px;">&nbsp; b、双击后会弹出一个配置窗体，如："Tomcat&nbsp;v6.0 Server at localhost"。在配置窗体的server option 的选择中，把Publish module contexts to separate XML files 选择。保存。</p>
<p style="padding: 0px; font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25.200000762939453px;">&nbsp; 问题解决。</p>