#mac brew安装mysql8.0
###发表时间：2018-10-19
###分类：mac,经验,brew,mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2432454" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2432454</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>随着mysql的版本升级，每个版本安装mysql的方法居然都不一样。这里谈一下mac如何通过brew安装mysql8.0.</p> 
 <p>还没有安装 brew 的可以去官网：&nbsp;<a href="https://brew.sh/">https://brew.sh/</a>&nbsp;安装。</p> 
 <p>安装mysql8.0如下：</p> 
 <p>1、先看看mysql安装需要什么？命令如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">$brew info mysql</pre> 
 <p>&nbsp;该命令会打印出安装需要的依赖和冲突的软件信息。</p> 
 <p>&nbsp;</p> 
 <p>2、进行安装：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">$brew install mysql</pre> 
 <p>&nbsp;安装完成之后提示信息如下（这个很重要，靠它安装的剩下的步骤）</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">We've installed your MySQL database without a root password. To secure it run:
    mysql_secure_installation

MySQL is configured to only allow connections from localhost by default

To connect run:
    mysql -uroot

To have launchd start mysql now and restart at login:
  brew services start mysql
Or, if you don't want/need a background service you can just run:
  mysql.server start
==&gt; Summary</pre>
</div>