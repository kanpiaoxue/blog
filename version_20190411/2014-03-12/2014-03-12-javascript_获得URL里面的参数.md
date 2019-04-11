#javascript 获得URL里面的参数
###发表时间：2014-03-12
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2030079" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2030079</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="html">&lt;script&gt;
function getConditionFromUrl(url,key){
	var position = url.indexOf('?');
	if(position &gt; 0){
		var tempUrl = url.substring(position + 1);
		var arr = tempUrl.split('&amp;');
		for(var i = 0, j = arr.length; i &lt; j; i++){
			var tempArr = arr[i].split('=');
			if(key === tempArr[0]){
				return tempArr[1];
			}
		}
	}
	return '';	
}

var url = 'http://www.baidu.com/seach?name=qudanna&amp;age=28&amp;sex=1&amp;address=Beijing';
alert(getConditionFromUrl(url,'name'));
alert(getConditionFromUrl(url,'age'));
alert(getConditionFromUrl(url,'sex'));
alert(getConditionFromUrl(url,'address'));
alert(getConditionFromUrl(url,'haha'));

&lt;/script&gt;</pre> 
 <p>&nbsp;</p> 
</div>