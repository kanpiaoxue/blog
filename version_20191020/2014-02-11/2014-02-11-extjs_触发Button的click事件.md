#extjs 触发Button的click事件
###发表时间：2014-02-11
###分类：javascript,Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2015081" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2015081</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">首先有一个按钮，并且有监听click的事件
var button_1 = new Ext.Button({
	text : "button",
	listeners :{
		click : function(){
	  	alert("111");
	 	}
	}
});


var button_2 = new Ext.Button({
	text : "button",
	handler:function(){
		//在这里触发那个按钮的点击事件就可以了
		button_1.fireEvent('click');
	}
});</pre> 
 <p>&nbsp;</p> 
</div>