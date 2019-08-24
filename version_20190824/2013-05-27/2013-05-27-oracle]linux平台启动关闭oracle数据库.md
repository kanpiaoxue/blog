#oracle]linux平台启动关闭oracle数据库
###发表时间：2013-05-27
###分类：oracle
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1876743" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1876743</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p><a style="color: #1d58d1; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;" href="http://blog.csdn.net/blueilove2003/archive/2008/01/28/2070075.aspx"><span style="text-decoration: underline;"><span style="color: #800080;">oracle]linux平台启动关闭oracle数据库</span></span></a><span style="font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p id="fp" style="margin-bottom: 14px; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;">oracle数据库是重量级的，其管理非常复杂，将其在linux平台上的启动和关闭步骤整理一下。</p> 
 <p style="margin-bottom: 14px; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;">安装完毕oracle以后，需要创建oracle系统用户，并在/home/oracle下面的.bash_profile添加几个环境变量：ORACLE_SID,ORACLE_BASE,ORACLE_HOME。比如：</p> 
 <p style="margin-bottom: 14px; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;">export ORACLE_SID=test&nbsp; export ORACLE_BASE=oracle_install_dir export ORACLE_HOME=xxx</p> 
 <p style="margin-bottom: 14px; font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;">启动步骤：注意$代表shell命令提示符，这里的oracle是9.0以上版本。</p> 
 <ol style="font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19px;"> 
  <li>$ su - oracle</li> 
  <li>$ sqlplus / nolog</li> 
  <li>sql&gt; conn / as sysdba</li> 
  <li>sql&gt; startup (一般不需要加参数，只要设置好环境变量）</li> 
  <li>sql&gt; quit (退出sql模式)</li> 
  <li>$ lsnrctl start (启动监听器）<a id="more-15" style="color: #1d58d1;"></a>关闭oracle
   <ol> 
    <li>$ lsnrctl stop(关闭监听器，在这之前，应该先关闭应用程序）</li> 
    <li>$ sqlplus&nbsp; /nolog</li> 
    <li>sql&gt;shutdown 其参数 ：shutdown有四个参数，四个参数的含义如下：<br>Normal&nbsp;需要等待所有的用户断开连接<br>Immediate&nbsp;等待用户完成当前的语句<br>Transactional&nbsp;等待用户完成当前的事务<br>Abort&nbsp;不做任何等待，直接关闭数据库<br>normal需要在所有连接用户断开后才执行关闭数据库任务，所以有的时候看起来好象命令没有运行一样！在执行这个命令后不允许新的连接<br>immediate在用户执行完正在执行的语句后就断开用户连接，并不允许新用户连接。<br>transactional&nbsp;在拥护执行完当前事物后断开连接，并不允许新的用户连接数据库。<br>abort&nbsp;执行强行断开连接并直接关闭数据库。<br>前三种方式不回丢失用户数据。第四种在不的已的情况下，不建议采用！</li> 
   </ol> <p style="margin-bottom: 14px;">经常遇到的问题：</p> <p style="margin-bottom: 14px;">1）权限问题，解决方法，切换到oracle用户；</p> <p style="margin-bottom: 14px;">2）没有关闭监听器 ，解决方法：关闭监听器</p> <p style="margin-bottom: 14px;">3）有oracle实例没有关闭，解决办法：关闭oracle实例</p> <p style="margin-bottom: 14px;">4）环境变量设置不全，解决办法：修改环境变量</p> </li> 
 </ol> 
</div>