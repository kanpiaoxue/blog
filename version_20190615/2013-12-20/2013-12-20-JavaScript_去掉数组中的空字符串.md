#JavaScript 去掉数组中的空字符串
###发表时间：2013-12-20
###分类：javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1993018" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1993018</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">/**
 * &lt;pre&gt;
 * @param str
 * @returns {Array} 用逗号,将string进行分割，形成一个数组
 * &lt;/pre&gt;
 */
function splitToArrayWithoutBlank(str){
	var arr = str.split(',');
	return skipEmptyElementForArray(arr);
}

/**
 * &lt;pre&gt;
 * @param arr
 * @returns {Array} 如果arr中的元素存在空字符串''，则去掉该空字符串
 * &lt;/pre&gt;
 */
function skipEmptyElementForArray(arr){
	var a = [];
	$.each(arr,function(i,v){
		var data = $.trim(v);//$.trim()函数来自jQuery
		if('' != data){
			a.push(data);
		}
	});
	return a;
}</pre> 
 <p>&nbsp;</p> 
</div>