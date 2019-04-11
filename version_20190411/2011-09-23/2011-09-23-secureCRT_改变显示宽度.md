#secureCRT 改变显示宽度
###发表时间：2011-09-23
###分类：Linux
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1178913" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1178913</a>

---

<p><span style="font-family: Helvetica, Arial, sans-serif; line-height: 19px;"> </span></p>
<h2 style="margin-top: 0px; margin-right: 0px; margin-bottom: 0.5em; margin-left: 0px; font-size: 1.17em; line-height: normal; padding: 0px;">secureCRT 改变显示宽度</h2>
<div id="postmessage_920" class="t_msgfont" style="line-height: 1.6em; font-size: 14px;">
 每次用secureCRT登陆后sqlplus查询数据都是折行显示，即使set lines 1024参数后也没用，很不爽，今天终于搞定了。
 <br style="line-height: normal;">SecureCRT v5.5.1 (build 407)&nbsp;
 <br style="line-height: normal;">
 <br style="line-height: normal;">1、首先全局设置：Options - Global Options - Terminal - Appearance - Maximumcolumns 最大只能设置成1024（推荐256），设置越大越占用内存，并选上show horizontal scrollbar，然后重启SecureCRT；
 <br style="line-height: normal;">
 <br style="line-height: normal;">2、然后session设置：Options - Session Options(或者Global Options - General -Default Session - Edit Default Session，这样就可以设置所有的Session) - Terminal -Emulation - Logical Columns设置成255（推荐255，主要是因为Sqlplus里Dbms_output.put_line最多显示255字符限制，这里最大值只能设置成上面Maximum columns大小，并选上Retain size and font）、Logicalrows设置成42（刚好满屏）、Scrollbackbuffer设置成5000（这样纵向
 <span class="t_tag" style="line-height: normal; cursor: pointer; border-bottom-width: 1px; border-bottom-style: solid; border-bottom-color: #ff0000; white-space: nowrap;">滚动</span>屏就可以缓存更多内容，但占内存），另外Terminal - Appearance - Window -选上Show horizontal scroll bar，然后重新连接。
 <br style="line-height: normal;">
 <br style="line-height: normal;">附官方论坛开发人员的解释：
 <br style="line-height: normal;">
 <br style="line-height: normal;">There are also a couple of other settings which should allow you scroll to the right.
 <br style="line-height: normal;">Besides increasing the column amount as MikeStammer mentioned tosomething higher then 132 in the 'Emulation' sub-category under'Terminal' in the session options. Another option that needs to beenabled is 'Retain size and font' in that same category.
 <br style="line-height: normal;">If the columns are not increase, the remote will not even send theinformation after 132 characters. In this case, setting it to 200 or256 will ensure that no informaiton is left off from the editors.
 <br style="line-height: normal;">The 'Retain size and font' option will have SecureCRT leave the fontsize alone so that any extra text will just appear off the screenallowing you to scroll to it. You will also be able to manually resizeyour window without affecting the font size.
 <br style="line-height: normal;">The maximum number of columns in SecureCRT can be increased by changingthe 'Maximum columns' setting in the 'Appearance' sub-category under'Terminal' in the 'Global Options'.then restart SecureCRT, you willthen be able to change any of your session logical columns to 1024.
 <br style="line-height: normal;">The maximum number of columns that can be set is 1024.
 <br style="line-height: normal;">As the maximum number of columns allowed is increased, the memory usageof SecureCRT is also increases. The default of 132 columns was set toallow the least memory usage and yet still be compatible with mostapplications.
 <br style="line-height: normal;">
 <br style="line-height: normal;">--End--
</div>
<p>&nbsp;</p>