#Ext Treepanel 得到选中的节点
###发表时间：2013-12-25
###分类：javascript,Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1995127" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1995127</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">var tree = Ext.getCmp('getSharedFromOthersTree');
var sm = tree.getSelectionModel();

var node = sm.getSelectedNode() ;
alert(node.attributes.text);
sm.clearSelections() ;//清空选择区，并返回选择区中的节点
//参考 Ext.tree.DefaultSelectionModel </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>