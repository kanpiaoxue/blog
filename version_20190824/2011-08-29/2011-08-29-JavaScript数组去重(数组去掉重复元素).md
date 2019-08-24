#JavaScript数组去重（数组去掉重复元素）
###发表时间：2011-08-29
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1160324" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1160324</a>

---

<p> </p>
<pre name="code" class="js">&lt;script&gt;
/**
 * 利用JavaScript内置的hash去重数组中的重复元素
 * @author kanpiaoxue
 * date 2011/08/29 13:29:01
 */
function uniqueArray(arr){
	if(null == arr || arr.length == 0 ){
		return arr;
	}else{
		var innerHashMap = {};
		for(var i = 0, j = arr.length; i&lt;j; i++){
			innerHashMap[arr[i]] = null;
		}
		var rs = [];
		for (obj in innerHashMap){
			rs.push(obj);
		}
		return rs;
	}
}

/*------------------------ test ---------------------------*/
var arr = [1,2,3,4,5,6,7,8,9,0,1,2,3,4,5,6,7,8,9,0];
var arr1 = [];
for(var i = 0 ; i &lt; 10; i++){
	arr1[i] = 'element' + (i%2);
}

//alert('source: ' + arr + '\n' + 'target: ' + uniqueArray(arr) + '\n' + 'source: ' +  arr1 + '\n' + 'target: ' +  uniqueArray(arr1))

var longArr = []
for(var i = 0; i &lt; 100000; i++){
	longArr[i] = i;
}

var start = (new Date()).getTime();
uniqueArray(longArr);
var end = (new Date()).getTime();
alert((end - start) + 'ms');

&lt;/script&gt;</pre>