#为EasyUI 的Tab 标签添加右键菜单
###发表时间：2015-05-20
###分类：easyui,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2212929" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2212929</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="html"> &lt;div id="mm" class="easyui-menu" style="width:150px;"&gt;
         &lt;div id="mm-tabclose" name="1"&gt;关闭标签页&lt;/div&gt;
        &lt;div id="mm-tabcloseall" name="2"&gt;关闭全部标签页&lt;/div&gt;
        &lt;div id="mm-tabcloseother" name="3"&gt;关闭其它标签页&lt;/div&gt;
        &lt;div class="menu-sep"&gt;&lt;/div&gt;
        &lt;div id="mm-tabcloseright" name="4"&gt;关闭右侧标签页&lt;/div&gt;
        &lt;div id="mm-tabcloseleft" name="5"&gt;关闭左侧标签页&lt;/div&gt;
    &lt;/div&gt;</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">	// 监听右键事件，创建右键菜单
		$('#tt').tabs({
			onContextMenu : function(e, title, index) {
				e.preventDefault();
				//if (index &gt; 0) {
					$('#mm').menu('show', {
						left : e.pageX,
						top : e.pageY
					}).data("tabTitle", title);
				//}
			}
		});
		// 右键菜单click
		$("#mm").menu({
			onClick : function(item) {
				closeTab(this, item.name);
			}
		});</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">// 删除Tabs
function closeTab(menu, type) {
	var obj = $('#tt');
	;
	var allTabs = obj.tabs('tabs');
	var allTabtitle = [];
	$.each(allTabs, function(i, n) {
		var opt = $(n).panel('options');
		if (opt.closable) {
			allTabtitle.push(opt.title);
		}
	});
	var curTabTitle = $(menu).data('tabTitle');

//	console.log('curTabTitle:' + curTabTitle)

	var curTabIndex = obj.tabs('getTabIndex', obj.tabs('getTab', curTabTitle));
	/**
	 * &lt;pre&gt;
	 * 	    1:关闭标签页
	 * 	    2:关闭全部标签页
	 * 	    3:关闭其它标签页
	 * 	    4:关闭右侧标签页
	 * 	    5:关闭左侧标签页
	 * &lt;/pre&gt;
	 */
	switch (type) {
	case '1':
		obj.tabs('close', curTabTitle);
		break;
	case '2':
		for (var i = 0, j = allTabtitle.length; i &lt; j; i++) {
			obj.tabs('close', allTabtitle[i]);
		}
		break;
	case '3':
		for (var i = 0, j = allTabtitle.length; i &lt; j; i++) {
			if (curTabTitle != allTabtitle[i]) {
				obj.tabs('close', allTabtitle[i]);
			}
		}
		obj.tabs('select', curTabTitle);
		break;
	case '4':
		for (var i = curTabIndex + 1 ,j = allTabtitle.length; i&lt;j; i++) {
			obj.tabs('close', allTabtitle[i]);
		}
		obj.tabs('select', curTabTitle);
		break;
	case '5':
		for (var i = 0; i &lt; curTabIndex; i++) {
			obj.tabs('close', allTabtitle[i]);
		}
		obj.tabs('select', curTabTitle);
		break;
	}

}</pre> 
 <p>&nbsp;</p> 
</div>