#JavaScript 拥有的属性 Obj.hasOwnProperty(obj.属性)
###发表时间：2010-04-13
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/642972" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/642972</a>

---

<pre name="code" class="js">&lt;script&gt;
function Person(obj){
	this.name = obj.name;
	this.age = obj.age;
}

var one = new Person({
	name : "hello",
	age : 22
});

alert("hasOwnProperty: " + one.hasOwnProperty("name"));

&lt;/script&gt;</pre>
<p>&nbsp;</p>