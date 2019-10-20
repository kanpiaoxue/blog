#javascript格式化日期Date
###发表时间：2015-07-09
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2225891" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2225891</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">function dateFormat(date,fmt) { // author: meizz
	var dateObject = null;
	if (date.constructor == Date){
		dateObject = date;
	}else if(date.constructor == Number){
		dateObject = new Date(date);
	}else if(date.constructor == String){
		dateObject = Date.parse(date);
	}else{
			alert('illegal argument type:'+date.constructor);
			return null;
	}

	//console.log(dateObject.getMonth());
	var month =  dateObject.getMonth() + 1;

	var o = {
		"M+" : month, // 月份
		"d+" : dateObject.getDate(), // 日
		"h+" : dateObject.getHours(), // 小时
		"m+" : dateObject.getMinutes(), // 分
		"s+" : dateObject.getSeconds(), // 秒
		"q+" : Math.floor((dateObject.getMonth() + 3) / 3), // 季度
		"S" : dateObject.getMilliseconds()
	// 毫秒
	};
	if (/(y+)/.test(fmt)){
		fmt = fmt.replace(RegExp.$1, (dateObject.getFullYear() + "")
				.substr(4 - RegExp.$1.length));
	}
	for ( var k in o){
		if (new RegExp("(" + k + ")").test(fmt)){
			fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k])
					: (("00" + o[k]).substr(("" + o[k]).length)));
				}
	}
	return fmt;
};</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">function createDataVersion(timeType, timeString, isStart) {

	timeType = Number(timeType);
	var date = Date.parse(timeString);

	var formatString = 'yyyyMMdd';

	switch (timeType) {
	case 1:// 分钟
	formatString = 'yyyyMMddhhmm';
		break;
	case 2:// 小时
		formatString = isStart ? 'yyyyMMddhh00':'yyyyMMddhh59';
		break;
	case 3:// 日
	case 4:// 周
	case 5:// 月
	case 6:// 季
		formatString = isStart ? 'yyyyMMdd0000':'yyyyMMdd2359';
		break;
	default:
		alert('can not find timeType:'+timeType);
		break;
	}
	var rs = dateFormat(date,formatString);
	return rs;
}

function show(d,timeType,isStart){

	var msg = null;
	switch (timeType) {
	case 1:// 分钟
		msg = 'minute';
		break;
	case 2:// 小时
		msg = 'hour';
		break;
	case 3:// 日
		msg = 'day';
		break;
	case 4:// 周
	msg = 'week';
	break;
	case 5:// 月
	msg = 'month';
	break;
	case 6:// 季
		msg = 'quarter';
		break
		break;
	default:
		alert('can not find timeType:'+timeType);
		break;
	}

	var s = isStart ? 'begin':'end';
	var val = createDataVersion(timeType, d, isStart);
	console.log(s+'\t--&gt;'+msg+':'+val);
}

var d1 = '2015-07-09 16:16:29';
var d2 = '2015-07-09 16:16';
var d3 = '2015-07-09';


for(var i = 1; i&lt;=6; i++){
	show(d1,i,true);
	show(d1,i,false);
	console.log('----------------');
}

&lt;/script&gt;</pre> 
 <p>&nbsp;</p> 
</div>