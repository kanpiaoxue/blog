#JavaScript 构造器 constructor
###发表时间：2010-04-13
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/642969" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/642969</a>

---

<pre name="code" class="html">&lt;script&gt;
function Person(obj){
	this.name = obj.name;
	this.age = obj.age;
}

var one = new Person({
	name : "helloWorld",
	age : 22
});

alert(one.constructor == Person);

&lt;/script&gt;</pre>
<p>&nbsp;</p>