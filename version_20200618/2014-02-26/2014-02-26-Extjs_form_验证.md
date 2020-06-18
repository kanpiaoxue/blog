#Extjs form 验证
###发表时间：2014-02-26
###分类：javascript,Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2022673" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2022673</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="js">var form = Ext.getCmp('createTempTableFormId');
if(!form.form.isValid()){
confirmWarning('请输入必要的内容');
return;
}</pre> 
 <p>&nbsp;</p> 
</div>