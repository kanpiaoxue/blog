#Ext multiselect多选框
###发表时间：2013-12-20
###分类：javascript,Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1992700" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1992700</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在Ext里面经常会用到多选的组件：&nbsp;multiselect</p> 
 <p>我这里给出的是Ext 3.1.1的例子。里面有些地方需要注意，我会在下面进行说明</p> 
 <p>下面是HTML</p> 
 <pre name="code" class="html">&lt;html&gt;
&lt;head&gt;
    &lt;meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" /&gt;
    &lt;title&gt;MultiSelect &amp;amp; ItemSelector&lt;/title&gt;
    &lt;link rel="stylesheet" type="text/css" href="../../resources/css/ext-all.css" /&gt;
    &lt;link rel="stylesheet" type="text/css" href="../ux/css/MultiSelect.css"/&gt;
    &lt;link rel="stylesheet" type="text/css" href="../shared/examples.css" /&gt;
    
    &lt;script type="text/javascript" src="../../adapter/ext/ext-base.js"&gt; &lt;/script&gt;
    &lt;script type="text/javascript" src="../../ext-all.js"&gt; &lt;/script&gt;

    &lt;script type="text/javascript" src="../ux/MultiSelect.js"&gt;&lt;/script&gt;
    &lt;script type="text/javascript" src="../ux/ItemSelector.js"&gt;&lt;/script&gt;
    
    &lt;script type="text/javascript" src="multiselect-demo.js"&gt;&lt;/script&gt;
    &lt;script type="text/javascript" src="../shared/examples.js"&gt;&lt;/script&gt;

&lt;/head&gt;
&lt;body&gt;
    &lt;h1&gt;MultiSelect &amp;amp; ItemSelector&lt;/h1&gt;
    &lt;p&gt;The js is not minified so it is readable. See &lt;a href="multiselect-demo.js"&gt;multiselect-demo.js&lt;/a&gt;.&lt;/p&gt;
    
    &lt;b&gt;MultiSelect&lt;/b&gt;&lt;br /&gt;

    &lt;p&gt;Press Save with no items selected to see an example of validation applied.&lt;/p&gt;
    &lt;div id="multiselect" class="demo-ct" style="margin-bottom:15px;"&gt;&lt;/div&gt;
    
    &lt;b&gt;ItemSelector&lt;/b&gt;&lt;br /&gt;
    &lt;p&gt;Supports drag and drop, double-click, button move/reorder, etc.
    &lt;div id="itemselector" class="demo-ct"&gt;&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</pre> 
 <p>&nbsp;</p> 
 <p>下面是JS</p> 
 <pre name="code" class="js">/*!
 * Ext JS Library 3.1.1
 * Copyright(c) 2006-2010 Ext JS, LLC
 * licensing@extjs.com
 * http://www.extjs.com/license
 */
Ext.onReady(function(){

    Ext.QuickTips.init();
    Ext.form.Field.prototype.msgTarget = 'side';

    /*
     * Ext.ux.form.MultiSelect Example Code
     */
    var msForm = new Ext.form.FormPanel({
        title: 'MultiSelect Test',
        width: 700,
        bodyStyle: 'padding:10px;',
        renderTo: 'multiselect',
        items:[{
            xtype: 'multiselect',
            fieldLabel: 'Multiselect&lt;br /&gt;(Required)',
            name: 'multiselect',
            width: 250,
            height: 200,
            allowBlank:false,
            store: [[123,'One Hundred Twenty Three'],
                    ['1', 'One'], ['2', 'Two'], ['3', 'Three'], ['4', 'Four'], ['5', 'Five'],
                    ['6', 'Six'], ['7', 'Seven'], ['8', 'Eight'], ['9', 'Nine']],
            tbar:[{
                text: 'clear',
                handler: function(){
	                msForm.getForm().findField('multiselect').reset();
	            }
            }],
            ddReorder: true
        }],
        tbar:[{
            text: 'Options',
            menu: [{
	            text: 'Set Value (2,3)',
	            handler: function(){
	                msForm.getForm().findField('multiselect').setValue('2,3');
	            }
	        },{
	            text: 'Toggle Enabled',
	            handler: function(){
	                var m = msForm.getForm().findField('multiselect');
	                if (!m.disabled) {
	                    m.disable();
	                } else {
	                    m.enable();
	                }
	            }
            }]
        }],

        buttons: [{
            text: 'Save',
            handler: function(){
                if(msForm.getForm().isValid()){
	                Ext.Msg.alert('Submitted Values', 'The following will be sent to the server: &lt;br /&gt;'+
	                    msForm.getForm().getValues(true));
                }
            }
        }]
    });


    var ds = new Ext.data.ArrayStore({
        data: [[123,'One Hundred Twenty Three'],
            ['1', 'One'], ['2', 'Two'], ['3', 'Three'], ['4', 'Four'], ['5', 'Five'],
            ['6', 'Six'], ['7', 'Seven'], ['8', 'Eight'], ['9', 'Nine']],
        fields: ['value','text'],
        sortInfo: {
            field: 'value',
            direction: 'ASC'
        }
    });

    /*
     * Ext.ux.form.ItemSelector Example Code
     */
    var isForm = new Ext.form.FormPanel({
        title: 'ItemSelector Test',
        width:700,
        bodyStyle: 'padding:10px;',
        renderTo: 'itemselector',
        items:[{
            xtype: 'itemselector',
            name: 'itemselector',
            fieldLabel: 'ItemSelector',
	        imagePath: '../ux/images/',
            multiselects: [{
                width: 250,
                height: 200,
                store: ds,
                displayField: 'text',
                valueField: 'value'
            },{
                width: 250,
                height: 200,
                store: [['10','Ten']],
                tbar:[{
                    text: 'clear',
                    handler:function(){
	                    isForm.getForm().findField('itemselector').reset();
	                }
                }]
            }]
        }],

        buttons: [{
            text: 'Save',
            handler: function(){
                if(isForm.getForm().isValid()){
                    Ext.Msg.alert('Submitted Values', 'The following will be sent to the server: &lt;br /&gt;'+
                        isForm.getForm().getValues(true));
                }
            }
        }]
    });

});
</pre> 
 <p>&nbsp;【注意：】这里要说明的是，如何取得多选框中的数值的问题。</p> 
 <p>在Ext给出的例子中，&nbsp;msForm.getForm().getValues(true) 取值之后，</p> 
 <p>打印出来是：&nbsp;<span style="background-color: #ccd9e8; font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">multiselect=1%2C2%2C3%2C4</span></p> 
 <p><span style="background-color: #ccd9e8; font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">这个结果是被decode之后的，可以顺利的放在url里面传给后台。</span></p> 
 <p><span style="background-color: #ccd9e8; font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">但是：如果我们需要在前台处理我们的选项，或者我们不想用上面给出的decode之后的结果传递给后台，该如何处理呢？</span></p> 
 <p><span style="background-color: #ccd9e8; font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">其实很简单，需要注意2个地方。</span></p> 
 <p><span style="background-color: #ccd9e8; font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">1、在</span><span style="font-family: tahoma, arial, helvetica, sans-serif;"><span style="background-color: #ccd9e8; font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">&nbsp;xtype: 'multiselect', 下面有表单的name的配置：</span><span style="font-size: 12px; line-height: normal;">name: 'multiselect',</span></span></p> 
 <p><span style="font-family: tahoma, arial, helvetica, sans-serif;"><span style="font-size: 12px; line-height: normal;">&nbsp; &nbsp; &nbsp;这里的name，就是你取得数据的关键。</span></span></p> 
 <p><span style="font-family: tahoma, arial, helvetica, sans-serif;"><span style="font-size: 12px; line-height: normal;">2、例子中取出数据的是这条语句：</span></span></p> 
 <p><span style="font-family: tahoma, arial, helvetica, sans-serif;"><span style="font-size: 12px; line-height: normal;">&nbsp; &nbsp; &nbsp; msForm.getForm().getValues(true)</span></span></p> 
 <p><span style="font-family: tahoma, arial, helvetica, sans-serif;"><span style="font-size: 12px; line-height: normal;">&nbsp; &nbsp; &nbsp;我们也需要对它进行改造。如下：</span></span></p> 
 <p><span style="font-family: tahoma, arial, helvetica, sans-serif;"><span style="font-size: 12px; line-height: normal;">&nbsp; &nbsp; &nbsp; var selectItems =</span></span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">&nbsp;</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">msForm.getForm().getValues().</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">multiselect;</span></p> 
 <p><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">&nbsp; &nbsp; &nbsp; 这个&nbsp;</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">selectItems</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">&nbsp; 就是我们要的数值。通过 alert(</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">selectItems.constructor); 我们可以知道，</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">selectItems</span><span style="font-family: tahoma, arial, helvetica, sans-serif; font-size: 12px; line-height: normal;">&nbsp;是一个字符串，里面的数值用逗号,进行了串联。我们来处理这个逗号,分割的字符串就可以得到一个数组。就是我们要的数值</span></p> 
</div>