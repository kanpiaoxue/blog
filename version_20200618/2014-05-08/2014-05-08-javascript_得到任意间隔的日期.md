#javascript 得到任意间隔的日期
###发表时间：2014-05-08
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2064027" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2064027</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">//得到今天为起点的任意一天地日期
function getDateByCount(addDayCount) {
    var dd = new Date();
    dd.setDate(dd.getDate()+addDayCount);//获取addDayCount天后的日期
    var y = dd.getFullYear();
    var m = dd.getMonth()+1;
    var d = dd.getDate();
    return y+"-"+m+"-"+d;
}

//得到以 otherDate 为起点的任意一天的日期
function getDateByCountWithOtherDate(otherDate,addDayCount) {
		if(!otherDate || otherDate.constructor != Date){
			alert('otherDate 不是日期类型，请检查！');
			return;
		}
		var dd = new Date(otherDate.getTime());
		dd.setDate(dd.getDate()+addDayCount);//获取addDayCount天后的日期
		return dd;
}

document.write("&lt;br /&gt;昨天："+getDateByCount(-1));
document.write("&lt;br /&gt;今天："+getDateByCount(0));
document.write("&lt;br /&gt;明天："+getDateByCount(1));
document.write("&lt;br /&gt;后天："+getDateByCount(2));</pre> 
 <p>&nbsp;</p> 
</div>