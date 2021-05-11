#JavaScript 生成随机颜色
###发表时间：2013-12-20
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1993010" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1993010</a>

---

<div class="iteye-blog-content-contain"> 
 <pre name="code" class="js">/**
 * &lt;pre&gt;
 * @returns {String} 生成随机的颜色字符串
 * &lt;/pre&gt;
 */
function getRandomColorString(){
	return '#'+('00000'+(Math.random()*0x1000000&lt;&lt;0).toString(16)).slice(-6);
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>