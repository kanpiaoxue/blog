#Struts2 的 Action 被 无故 执行2次 或 执行多次
###发表时间：2010-09-09
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/759451" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/759451</a>

---

<p>Struts2 的 Action 被 无故 执行2次 或 执行多次</p>
<p>你请求了一次，日志却出现了2次，而且是2次相同的...</p>
<p>一个Action被执行了2次！（甚至有多次的情况）</p>
<p>出现这种情况的人&nbsp; 都是用&nbsp; SSS!SSSS.action 来执行的</p>
<p>也就是说一个 Action类中，有N个方法被当成Action来用...</p>
<p>具体就是 你的方法名 用了&nbsp; getXXX 为方法名</p>
<p>也就是说，如果你的Action是一个方法，而且以叹号的方式请求，方法还以get开头</p>
<p>如：getUserById() 、getACL() 等...</p>
<p>那么...你就会出现上面的错误...</p>
<p>&nbsp;</p>
<p>解决方法很简单，帮你的方法换个名字</p>
<p>如：loadUserById()...</p>