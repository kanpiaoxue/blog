#MySQL Workbench: how do I set up “ON UPDATE” and CURRENT_TIMESTAMP?
###发表时间：2019-12-31
###分类：mysql,MySQL Workbench,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2511600" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2511600</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;<a href="https://stackoverflow.com/questions/8194157/mysql-workbench-how-do-i-set-up-on-update-and-current-timestamp">https://stackoverflow.com/questions/8194157/mysql-workbench-how-do-i-set-up-on-update-and-current-timestamp</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">I am using MySQL Workbench 5.2.35. Open create/alter table panel, switch to the columns tab, right click on the timestamp field; there you can see possible&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">default</code>&nbsp;and&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">on update</code>&nbsp;options.</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">Important note: You can use&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">CURRENT_TIMESTAMP</code>&nbsp;as default or updated value for only a single column in a table!</p> 
 <p>&nbsp;</p> 
</div>