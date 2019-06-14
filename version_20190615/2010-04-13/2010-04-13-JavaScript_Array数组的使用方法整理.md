#JavaScript Array数组的使用方法整理
###发表时间：2010-04-13
###分类：array,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/643005" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/643005</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">Array 的使用方法
1、声明Array的方法
   (1)	var arr = new Array(); 
   		//var arr = new Array(20); 
   		//通过构造函数指定数组的大小：缺点：如果数组不能填充满，浪费内存
   									优点：如果知道数组大小，能加快程序的运行速度，优化程序。
   		arr[0] = 'green';
   		arr[1] = 'red';
   		arr[2] = 'yellow';
   		alert(arr.length);//outputs : 3
   		arr[25] = 'blue';//直接没有被赋值的索引的地方都填充null
   		alert(arr.length);//outputs : 26 
   
   (2)	var arr = new Array('green','red','yellow');
   		alert(arr.length);//outputs : 3
   
   (3)	var arr = new Array;//没有用到构造函数的时候，可以省略后面的括号'()'
         arr.push('green');
         arr.push('red');
         arr.push('yellow');
         alert(arr.length);//outputs : 3
   
   (4)	var arr = [];//js声明Array的简写。
        	arr[0] = 'green';
   		arr[1] = 'red';
   		arr[2] = 'yellow';
   		alert(arr.length);//outputs : 3
   		//也可以 var arr = ['green','red','yellow'];
2、Array的常用方法
		(1)、join();数组生成字符串时候的链接，
			例如：	var arr = ['green','red','yellow'];
					alert(arr.join('-'));//outputs ：green-red-yellow
					alert(arr.join(''));//outputs ：greenredyellow
					alert(arr.join(']['));//outputs ：green][red][yellow
		(2)、toString();  //valueOf();  
				//valueOf()函数里面调用的是toString()方法。可以进行验证
				Array.prototype.toString = function(){
					return this.join('-');
				};
				//此时同时调用Array的toString()和valueOf()函数，发现它们结果相同，
             //证明了valueOf()也被重写了。
             Array.prototype.valueOf = function(){
					return this.join('-');
				};
				//这样重写了valueOf()之后，同时调用Array的toString()和valueOf()函数，
				//发现它们结果不相同。说明‘valueOf()函数里面调用的是toString()方法’。
		(3)、slice(arg1[,arg2]);//返回数组，和String的substring()方法的使用方法类似。
			var arr = [];
        	arr[0] = 'green';
	   		arr[1] = 'red';
	   		arr[2] = 'yellow';
	   		arr[3] = 'blue';
	   		arr[4] = 'black';
	   		var tempArray_1 = arr.slice(1);
	  		var tempArray_2 = arr.slice(0,3);
			alert(tempArray_1.toString());//outputs : red,yellow,blue,black
			alert(tempArray_2.toString());//outputs : green,red,yellow
		(4)、push()、pop(): 对[栈](后进先出结构，动作都在栈顶发生)的操作
			var arr = [];
			for(var i = 0 ; i &lt; 6; i++){
				//[注意] push()方法可以允许同时放入多个参数，构成数组
				arr.push('hello_' + i);//arr.push('hello_' + i,'world_' + i); 
			}
			alert(arr.toString());//outputs : hello_0,hello_1,hello_2,hello_3,hello_4,hello_5
			var removedItem = arr.pop();
			alert(removedItem);//outputs : hello_5
			alert(arr.toString());//outputs : hello_0,hello_1,hello_2,hello_3,hello_4
		(5)、shift()、unshift()：对[队列](后进后出结构，最近加入的元素最后删除。数据的插入发生在队列的尾部，数据的删除发生在队列的头部)
			shift()删除数组的第一项
			unshift()把一个项放在数组的第一个位置
				var arr = ['green','red','yellow'];
				var item = arr.shift();
				alert(item.toString());//outputs : green
				alert(arr.toString());//outputs : red,yellow
				arr.unshift('black');
				alert(arr.toString());//outputs : black,red,yellow
		(6)、排序：	reverse();颠倒数组里面元素的顺序
				sort();对于字母排序正常，按照字母的顺序排序。对于数字和汉字的排序，就会有问题，这个地方需要重构。
		(7)、splice()作用：把数据项插入数组的中部
				a、删除			：(2个参数)声明2个参数，分别是：要删除的第一个项的位置和要删除的项的个数
					例如： arr.splice(0,2);删除掉数组arr中的前两项
				b、替换而不删除	：(3个参数)声明3个参数，分别是：起始位置、0(要删除的数据项的个数)、和要插入的项。
					此外，还可以用更多的参数项指定其他要插入的项。
					arr.splice(2,0,'red','blue');将在第2个位置插入'red'和'blue'	
				c、替换并删除	：(3个参数)声明3个参数，分别是：起始位置、要删除的数据项的个数以及要插入的项。
					此外，还可以指定要插入的更多的项。要插入的项的个数不必等于删除的项的个数。
					例如：arr.splice(2,1,'red','green');将删除数组arr中位置2处的项，然后在位置2处插入'red'和'green'。
		(8)、字符串变成数组：split()
			var str = 'h,e,l,l,o';
			var arr = str.split(',');//变成数组
			alert(arr.toString());//outputs : h,e,l,l,o
			var s = arr.join('][');//逆操作，数组变成字符串
			alert(s);//outputs ： h][e][l][l][o
				
				
3、关于数组的优化：
	(1)、数组循环3种优劣势比较：推荐用for(var i = 0 ; arr[i] ; i++){//your code}
		var arr = [1,2,3,4,5,6,7,8,9];
		a、性能：最差
			for(var i = 0 ; i &lt; arr.length ; i++){
				alert(arr[i]);
			}
		b、性能：折中
			for(var i = 0 , j = arr.length ; i &lt; j ; i++){
				alert(arr[i]);
			}
		c、性能：最优
			for(var i = 0 ; arr[i] ; i++){
				alert(arr[i]);
			}
		当数据量为1500条，3种循环时间消耗相差无几；
		当数据量为15000条，(1)会当掉，(2)耗时比较长，(3)瞬间完成；
		当数据量为150000条，(1)、(2)都会当掉，(3)耗时2s左右完成；
		[注意]采用 c 方式（ for(var i = 0 ; arr[i] ; i++) ）的时候，
		      当数组元素arr[i]为 0 或者 '0' 时， 会停止运行，认为 arr[i]（值为0）是false
		      所以 c 方式适合于对象（Object）循环，不适用于数字循环。
	(2)、对数组赋值
		建议采用索引赋值，而不是采用push()赋值。速度会快很多。
 
</pre> 
 <p>&nbsp;</p> 
</div>