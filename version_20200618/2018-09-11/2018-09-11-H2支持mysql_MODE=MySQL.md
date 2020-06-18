#H2支持mysql：MODE=MySQL
###发表时间：2018-09-11
###分类：h2,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2430433" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2430433</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <h3 style="margin-top: 10px; margin-bottom: 10px; font-size: 16px; line-height: 1.5; color: #444444; font-family: tahoma, arial, sans-serif;"><span style="margin: 0px; padding: 0px;" lang="zh-CN">连接字符串参数</span></h3> 
 <ul style="margin-bottom: 0px; margin-left: 30px; color: #444444; font-family: tahoma, arial, sans-serif; font-size: 12px;" type="disc"> 
  <li style="margin-bottom: 1em; margin-left: 0px;"><span style="margin: 0px; padding: 0px;">DB_CLOSE_DELAY：要求最后一个正在连接的连接断开后，不要关闭数据库</span></li> 
  <li style="margin-bottom: 1em; margin-left: 0px;"> <span style="margin: 0px; padding: 0px;" lang="zh-CN">MODE=MySQL：兼容模式，</span><span style="margin: 0px; padding: 0px;" lang="en-US">H2</span><span style="margin: 0px; padding: 0px;" lang="zh-CN">兼容多种数据库，该值可以为：DB2、Derby、HSQLDB、MSSQLServer、MySQL、Oracle、PostgreSQL</span> </li> 
  <li style="margin-bottom: 1em; margin-left: 0px;"><span style="margin: 0px; padding: 0px;">AUTO_RECONNECT=TRUE：连接丢失后自动重新连接</span></li> 
  <li style="margin-bottom: 1em; margin-left: 0px;"><span style="margin: 0px; padding: 0px;">AUTO_SERVER=TRUE：启动自动混合模式，允许开启多个连接，该参数不支持在内存中运行模式</span></li> 
  <li style="margin-bottom: 1em; margin-left: 0px;"> <span style="margin: 0px; padding: 0px;" lang="zh-CN">TRACE_LEVEL_SYSTEM_OUT、TRACE_LEVEL_FILE：输出跟踪日志到控制台或文件， 取值</span><span style="margin: 0px; padding: 0px;" lang="en-US">0</span><span style="margin: 0px; padding: 0px;" lang="zh-CN">为OFF，1为ERROR（默认值），2为INFO，3为DEBUG</span> </li> 
  <li style="margin-bottom: 1em; margin-left: 0px;"> <span style="margin: 0px; padding: 0px;" lang="zh-CN">SET TRACE_MAX_FILE_SIZE mb：设置跟踪日志文件的大小，默认为</span><span style="margin: 0px; padding: 0px;" lang="en-US">16M</span> </li> 
 </ul> 
 <p><span style="margin: 0px; padding: 0px;" lang="en-US">JDBC URL：&nbsp;jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1;DB_CLOSE_ON_EXIT=FALSE;MODE=MYSQL</span></p> 
</div>