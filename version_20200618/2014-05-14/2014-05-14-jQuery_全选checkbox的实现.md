#jQuery 全选checkbox的实现
###发表时间：2014-05-14
###分类：html,javascript,jQuery
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2066236" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2066236</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我自己写了一个例子，用jQuery全选checkbox。</p> 
 <p>附件中有完整的代码。</p> 
 <pre name="code" class="js">&lt;html&gt;
&lt;head&gt;
&lt;style&gt;
table {
	border: 1px solid black;
}

.checkbox {
}
&lt;/style&gt;
&lt;script type="text/javascript" src='jquery-1.10.2.js'&gt;&lt;/script&gt;
&lt;script type="text/javascript"&gt;
	$(function() {
		//给全选的checkbox添加动作
		$('#checkboxAllId').click(function() {
			if ($(this).prop('checked')) {
				$('.checkbox').each(function(i, d) {
					$(this).prop('checked', true);
				});
			} else {
				$('.checkbox').each(function(i, d) {
					$(this).prop('checked', false);
				});
			}
		});

		//给每一个子checkbox添加动作
		var checkboxObj = $('.checkbox');
		checkboxObj.click(function(i, d) {
			var checkedArr = [];
			var checkboxArr = [];
			if ($(this).prop('checked')) {
				checkboxObj.each(function(i, d) {
					if ($(this).prop('checked')) {
						checkedArr.push(this);
					}
					checkboxArr.push(this);
				});
				$('#checkboxAllId').prop('checked',
						(checkedArr.length == checkboxArr.length));

			} else {
				$('#checkboxAllId').prop('checked', false);
			}
		});

	});
&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;table&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" id="checkboxAllId" value="-1" /&gt;全选&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="1" /&gt;1&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="2" /&gt;2&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="3" /&gt;3&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="4" /&gt;4&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="5" /&gt;5&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="6" /&gt;6&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="7" /&gt;7&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="8" /&gt;8&lt;/td&gt;
		&lt;/tr&gt;
		&lt;tr&gt;
			&lt;td&gt;&lt;input type="checkbox" class="checkbox" value="9" /&gt;9&lt;/td&gt;
		&lt;/tr&gt;
	&lt;/table&gt;
&lt;/body&gt;
&lt;/html&gt;</pre> 
 <p>&nbsp;</p> 
</div>