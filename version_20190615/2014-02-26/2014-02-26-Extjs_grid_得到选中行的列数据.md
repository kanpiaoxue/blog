#Extjs grid 得到选中行的列数据
###发表时间：2014-02-26
###分类：Ext,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2022674" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2022674</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">function getSelectedTableName() {
	var grid = Ext.getCmp('tempTableGridId');
	var rowSelectionModel = grid.getSelectionModel();
	if (rowSelectionModel.hasSelection()) {
		var record = rowSelectionModel.getSelected();
		var tableName = record.get('tableName');
		return tableName;
	} else {
		return '';
	}
}</pre> 
 <p>&nbsp;</p> 
</div>