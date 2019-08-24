#How to hide or show textbox and combobox
###发表时间：2018-04-08
###分类：javascript,经验,easyui
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2415942" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2415942</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>目前的easyui不支持 extbox 和 combobox 直接的隐藏，需要进行扩展。</p> 
 <p>代码如下:</p> 
 <pre name="code" class="js">$.extend($.fn.textbox.methods, {
    show: function(jq){
        return jq.each(function(){
            $(this).next().show();
        })
    },
    hide: function(jq){
        return jq.each(function(){
            $(this).next().hide();
        })
    }
});</pre> 
 <p>&nbsp;使用举例如下：</p> 
 <pre name="code" class="js">$('#t1').textbox('hide');  // hide the textbox
$('#c1').combobox('hide');  // hide the combobox

$('#t1').textbox('show');  // show the textbox
$('#c1').combobox('show');  // show the combobox</pre> 
 <p>&nbsp;</p> 
</div>