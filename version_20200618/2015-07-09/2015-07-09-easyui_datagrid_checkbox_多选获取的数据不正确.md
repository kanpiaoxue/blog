#easyui datagrid checkbox 多选获取的数据不正确
###发表时间：2015-07-09
###分类：easyui,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2225927" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2225927</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>问题描述：easyui datagrid checkbox进行多选的时候，获取的数据与选择的数据不一致，有的时候一条数据，有的时候多条数据。</p> 
 <p>根源：easyui datagrid 设置了&nbsp;idField 列造成的。</p> 
 <p>解决：使用好&nbsp;idField 列，或者去掉这个配置。</p> 
 <p>如下：</p> 
 <pre name="code" class="js">	$('#dg_taskgrid')
			.datagrid(
					{
						remoteSort : true,
						/*toolbar : [ {
							text : '批量修复',
							iconCls : 'icon-batch-repair',
							handler : function() {
								batchRepairAction();
							}
						} ],*/
						
						toolbar : '#tb_ops',
						singleSelect: false,
                        checkOnSelect : false,
                        selectOnCheck : false,
						title : '任务列表',
						fitColumns : true, // 设置列宽度自适应屏幕
						iconCls : 'icon-task-list',
						striped : true,
						url : basePath + 'web/op/queryTaskLog',
						method : 'get',
						width: $(window).width()*0.9,
						pageNumber : 1,
						pageSize : baseNum, // 设置默认分页大小
						pageList : pageList, // 设置分页大小
						idField : 'versionId',
						columns : [ [
                                {
                                    checkbox : true
                                },
										 
								{
									field : 'taskId',
									title : '任务ID',
									width : 40,
									align : 'center',
									sortable : true
								},
								{
									field : 'taskName',
									title : '任务名称',
									width : 80,
									align : 'center',
									sortable : false,
									formatter : function(val, row, rowIndex) {
										var taskName = val;
										var taskId = row.taskId;
										var length = 40;
										var showTaskName = suitableLengthText(
												taskName, length);
										var arr = [];
										arr
												.push('&lt;a href="javascript:void(0);" title="');
										arr.push(taskName);
										arr.push('" class="'
												+ SHOW_FIRST_TOOLTIP_CLASS
												+ '" onclick="openTaskDeatil(');
										arr.push(taskId);
                                        arr.push(',2)"&gt;');
										arr.push(showTaskName);
										arr.push('&lt;/a&gt;');
										return arr.join('');

									}
								}, 
								
								{
				                    field : 'versionNo',
				                    title : '数据版本',
				                    width : 30,
				                    align : 'center',
				                    sortable : true
				                },
				                {
									field : 'state',
									title : '版本状态',
									width : 30,
									align : 'center',
									sortable : true,
									formatter : versionStateFormat
								}, 
				                {
				                    field : 'startTime',
				                    title : '运行开始时间',
				                    width : 40,
				                    align : 'center',
				                    sortable : true,
				                    formatter : function(val, row, rowIndex) {
				                        if (null == val) {
				                            return '-';
				                        } else {
				                            return val;
				                        }
				                    }
				                },
				                {
				                    field : 'endTime',
				                    title : '运行结束时间',
				                    width : 40,
				                    align : 'center',
				                    sortable : true,
				                    formatter : function(val, row, rowIndex) {
				                        if (null == val) {
				                            return '-';
				                        } else {
				                            return val;
				                        }
				                    }
				                },
				                {
									field : 'elapsedLabel',
									title : '运行耗时',
									width : 20,
									align : 'center',
									sortable : false
								}, 
				                {
				                    field : 'message',
				                    title : '信息',
				                    width : 80,
				                    align : 'left',
				                    sortable : false,
				                    formatter : function(val, row, rowIndex) {
				                        var length = 30;
				                        var showVal = suitableLengthText(val,
				                            length);
				                        var arr = [];
				                        arr.push('&lt;span class="'
				                            + SHOW_FIRST_TOOLTIP_CLASS
				                            + '" title="');
				                        arr.push(val);
				                        arr.push('"&gt;');
				                        arr.push(showVal);
				                        arr.push('&lt;/span&gt;');
				                        return arr.join('');
				                    }
				                },{
									field : 'teamName',
									title : '团队名称',
									width : 30,
									align : 'center'
								},  {
									field : 'op',
									title : '操作',
									//width : 40,
									align : 'center',
									formatter : formatOp,
									sortable : false
								} ] ],
						pagination : true,
						queryParams : {
							filters : params
						},
						onLoadSuccess : function(data) {
							addToolTips(SHOW_FIRST_TOOLTIP_CLASS);
						}
					});

};</pre> 
 <p>&nbsp;</p> 
 <p>附加 checkbox的多选函数：</p> 
 <pre name="code" class="java">function batchKillTaskAction(){
    // FIXME 20150709
    var checkedItems = $('#dg_taskgrid').datagrid('getChecked');
    var arr = [];
    $.each(checkedItems, function(index, item){
        var str = item.taskId + ':' + item.versionNo;
        arr.push(str);
    });
    console.log('arr:'+arr.length+' --&gt; '+arr.join(','))
}</pre> 
 <p>&nbsp;</p> 
</div>