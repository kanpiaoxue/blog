#jquery easyui添加、关闭、刷新Tab页
###发表时间：2017-11-01
###分类：easyui,经验,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2398318" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2398318</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>应用地址：<a href="http://chengyong.iteye.com/blog/1846455">http://chengyong.iteye.com/blog/1846455</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">define(function(require, exports, module) {  
    if (!window.cms)  
        window.cms = {};  
    cms = {  
        //添加新Tab页  
        addTab : function(data) {  
            var content = '&lt;iframe scrolling="auto" frameborder="0"  src="' + data.url + '" style="width:100%;height:100%;"&gt;&lt;/iframe&gt;';  
            if ($('#homePageTabs').tabs('exists', data.title)) {  
                // 选 中当前Tab  
                $('#homePageTabs').tabs('select', data.title);  
  
                // 重新加载已经存在的Tab内容  
                var currTab = $('#homePageTabs').tabs('getTab', data.title);  
                $('#homePageTabs').tabs('update', {tab: currTab, options: {content: content, closable: true}});  
            } else {  
                $('#homePageTabs').tabs('add', {  
                    title : data.title,  
                    content : content,  
                    closable : true  
                });  
            }  
        },  
        //关闭指定Tab  
        closeTab : function(title) {  
            if ($('#homePageTabs').tabs('exists', title)) {  
                $('#homePageTabs').tabs('close', title);  
            }  
        },  
        //刷新指定Tab的内容  
        refreshTab: function(title){  
            if ($('#homePageTabs').tabs('exists', title)){  
                var currTab = $('#homePageTabs').tabs('getTab', title),  
                    iframe = $(currTab.panel('options').content),  
                    content = '&lt;iframe scrolling="auto" frameborder="0"  src="' + iframe.attr('src') + '" style="width:100%;height:100%;"&gt;&lt;/iframe&gt;';  
                $('#homePageTabs').tabs('update', {tab: currTab, options: {content: content, closable: true}});  
            }  
        }  
    }  
  
});


cms.addTab({  
    id : 'homePageTabs',  
    title : '更新首页',  
    url : '/homePage/intoUpdate'  
});  </pre> 
 <p>&nbsp;</p> 
</div>