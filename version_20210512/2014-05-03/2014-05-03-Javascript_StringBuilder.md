#Javascript StringBuilder
###发表时间：2014-05-03
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2059464" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2059464</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">&lt;script&gt;
/**
 * @author: kanpiaoxue
 * Description: 模拟Java的StringBuilder
 */
function StringBuilder(str){
	this.arr = [];
	if(str){
		this.arr.push(str);
	}
}
StringBuilder.prototype = {
	append:function(str){
			this.arr.push(str);
			return this;
	},
	toString:function(){
		return this.arr.join('');
	}
};

var builder = new StringBuilder('kanpiaoxue');
var count = 5;
for(var i = 0; i &lt; count; i++){
	builder.append('hello'+ i);
}
alert(builder.toString());
//output 'kanpiaoxuehello0hello1hello2hello3hello4'
&lt;/script&gt;</pre> 
 <p>&nbsp;</p> 
</div>