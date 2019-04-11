#Javascript call和apply的区别
###发表时间：2014-05-03
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2059456" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2059456</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">&lt;script&gt;
	/**
	 * call: 它的第一个参数用作this的对象，其他的参数都直接传递给函数本身。
	 * apply:它有两个参数。第一个参数是用作this的对象，第二个参数是传递给函数的参数的数组。
	 * 
	 */
function Person(name,sex){
	this.name = name;
	this.sex = sex;
}
Person.prototype = {
	introduceSelf:function(){
		alert('My name is : ' + this.name + ', I\'m a ' + this.sex);	
	}
};
var person = new Person('Join','male');//output 'My name is : Join, I'm a male'
person.introduceSelf();
//给出一个继承的实现方式
function Student(name,sex,id){
	//Person.call(this,name,sex);// call 的用法
	Person.apply(this,arguments);// apply 的用法
	this.id = id;
}
Student.prototype = new Person();
Student.prototype.talkId = function(){
		alert('My student number is : ' + this.id);
};
var student = new Student('LiLei','male',101);
student.introduceSelf();//output 'My name is : LiLei, I'm a male'
student.talkId();//output 'My student number is : 101'
&lt;/script&gt;</pre> 
 <p>&nbsp;</p> 
</div>