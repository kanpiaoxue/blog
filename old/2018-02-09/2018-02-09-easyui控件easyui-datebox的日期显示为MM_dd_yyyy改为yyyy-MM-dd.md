#easyui控件easyui-datebox的日期显示为MM/dd/yyyy改为yyyy-MM-dd
###发表时间：2018-02-09
###分类：easyui,经验,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2410646" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2410646</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>今天使用&nbsp;easyui-datebox 控件，发现它的默认格式是：02/07/2018 ，可是中国人习惯的格式应该是：2018-02-09。 怎么处理呢？在写一个format的函数来处理？</p> 
 <p>后来我发现在js的引用的时候，加入本地化的js即可。加入：</p> 
 <pre name="code" class="html">&lt;script type="text/javascript" src="jquery-easyui/locale/easyui-lang-zh_CN.js"&gt;&lt;/script&gt;</pre> 
 <p>easyui-datebox 控件的显示格式便由MM/dd/yyyy改为yyyy-MM-dd。同时控件英文的地方改为了中文，更加符合国人的习惯。</p> 
 <p>&nbsp;</p> 
</div>