#ext check tree
###发表时间：2013-07-22
###分类：Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1911342" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1911342</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;来源：&nbsp;<a style="font-size: 12px; line-height: 1.5;" href="http://2008shucheng.iteye.com/blog/645260">http://2008shucheng.iteye.com/blog/645260</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">var Tree = Ext.tree;          
    var tree = new Tree.TreePanel({          
        el:'tree-div',          
        useArrows:true,          
        autoScroll:true,          
        animate:true,          
        enableDD:true,          
        containerScroll: true,           
        loader: new Tree.TreeLoader({          
        dataUrl:'treecheckjson.jsp'         
        })          
    });          
     
     tree.on('checkchange', function(node, checked) {             
        node.expand();             
        node.attributes.checked = checked;             
        node.eachChild(function(child) {             
            child.ui.toggleCheck(checked);             
            child.attributes.checked = checked;             
            child.fireEvent('checkchange', child, checked);             
        });             
    }, tree);          
          
    var root = new Tree.AsyncTreeNode({          
        text: 'Ext JS',          
        draggable:false,       
        checked:false,      
        id:'0'         
    });          
    tree.setRootNode(root);         
          
    tree.render();          
    root.expand();        
 //带复选框(checkbox)的树         
//改编自ExtJs 自带的tree例子，选中父节点后，所有子节点会自动选上。      
//该例子点击父节点如果速度过快，有时候不会自动选中子节点！     
var checkedNodes = tree.getChecked();//tree必须事先创建好.      
var s = [];      
for(var i=0;i&lt;checkedNodes.length;i++){      
s.push(checkedNodes[i].id)      
}   //得到里面选中的node id 值数组  </pre> 
 <p>&nbsp;</p> 
</div>