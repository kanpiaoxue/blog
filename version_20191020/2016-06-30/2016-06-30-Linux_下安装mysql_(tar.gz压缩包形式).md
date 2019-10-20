#Linux 下安装mysql （tar.gz压缩包形式）
###发表时间：2016-06-30
###分类：mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2308302" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2308302</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>自己简单的安装一个mysql。目的：能够运行mysql即可。</p> 
 <p>缺点：没有任何配置上面的优化。</p> 
 <p>步骤：</p> 
 <p>1、在 oracle.com 上面下载社区版本的mysql</p> 
 <p>2、上传到Linux机器的目录</p> 
 <p>3、根据mysql官网给出的安装 "2.2 Installing MySQL on Unix/Linux Using Generic Binaries"的步骤进行安装。</p> 
 <p>如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  shell&gt; groupadd mysql
  <br>shell&gt; useradd -r -g mysql -s /bin/false mysql
  <br>shell&gt; cd /usr/local
  <br>shell&gt; tar zxvf /path/to/mysql-VERSION-OS.tar.gz
  <br>shell&gt; ln -s full-path-to-mysql-VERSION-OS mysql
  <br>shell&gt; cd mysql
  <br>shell&gt; chown -R mysql .
  <br>shell&gt; chgrp -R mysql .
  <br>shell&gt; scripts/mysql_install_db --user=mysql
  <br>shell&gt; chown -R root .
  <br>shell&gt; chown -R mysql data
  <br>shell&gt; bin/mysqld_safe --user=mysql &amp;
  <br># Next command is optional
  <br>shell&gt; cp support-files/mysql.server /etc/init.d/mysql.server
 </div> 
 <p>&nbsp;并且这里假设用户使用的是root用户。</p> 
 <p>原文：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  Note
  <br>This procedure assumes that you have root (administrator) access to your
  <br>system. Alternatively, you can prefix each command using the sudo (Linux) or
  <br>pfexec (OpenSolaris) command.
 </div> 
 <p>&nbsp;</p> 
 <p>运行命令：scripts/mysql_install_db --user=mysql 之后会给出很多的文字描述，这个很有用。具体如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  [root@cp01-kanpiaoxue-org mysql]# scripts/mysql_install_db --user=mysql
  <br>Installing MySQL system tables...2016-06-30 15:24:47 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
  <br>2016-06-30 15:24:47 0 [Note] ./bin/mysqld (mysqld 5.6.31) starting as process 482 ...
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Using atomics to ref count buffer pool pages
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: The InnoDB memory heap is disabled
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Memory barrier is not used
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Compressed tables use zlib 1.2.3
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Using Linux native AIO
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Using CPU crc32 instructions
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Initializing buffer pool, size = 128.0M
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Completed initialization of buffer pool
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: The first specified data file ./ibdata1 did not exist: a new database to be created!
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Setting file ./ibdata1 size to 12 MB
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Database physically writes the file full: wait...
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Setting log file ./ib_logfile101 size to 48 MB
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Setting log file ./ib_logfile1 size to 48 MB
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Renaming log file ./ib_logfile101 to ./ib_logfile0
  <br>2016-06-30 15:24:47 482 [Warning] InnoDB: New log files created, LSN=45781
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Doublewrite buffer not found: creating new
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Doublewrite buffer created
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: 128 rollback segment(s) are active.
  <br>2016-06-30 15:24:47 482 [Warning] InnoDB: Creating foreign key constraint system tables.
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Foreign key constraint system tables created
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Creating tablespace and datafile system tables.
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Tablespace and datafile system tables created.
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Waiting for purge to start
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: 5.6.31 started; log sequence number 0
  <br>2016-06-30 15:24:47 482 [Note] Binlog end
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: FTS optimize thread exiting.
  <br>2016-06-30 15:24:47 482 [Note] InnoDB: Starting shutdown...
  <br>2016-06-30 15:24:49 482 [Note] InnoDB: Shutdown completed; log sequence number 1625977
  <br>OK
  <br>
  <br>Filling help tables...2016-06-30 15:24:49 0 [Warning] TIMESTAMP with implicit DEFAULT value is deprecated. Please use --explicit_defaults_for_timestamp server option (see documentation for more details).
  <br>2016-06-30 15:24:49 0 [Note] ./bin/mysqld (mysqld 5.6.31) starting as process 539 ...
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Using atomics to ref count buffer pool pages
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: The InnoDB memory heap is disabled
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Mutexes and rw_locks use GCC atomic builtins
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Memory barrier is not used
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Compressed tables use zlib 1.2.3
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Using Linux native AIO
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Using CPU crc32 instructions
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Initializing buffer pool, size = 128.0M
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Completed initialization of buffer pool
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Highest supported file format is Barracuda.
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: 128 rollback segment(s) are active.
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Waiting for purge to start
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: 5.6.31 started; log sequence number 1625977
  <br>2016-06-30 15:24:49 539 [Note] Binlog end
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: FTS optimize thread exiting.
  <br>2016-06-30 15:24:49 539 [Note] InnoDB: Starting shutdown...
  <br>2016-06-30 15:24:51 539 [Note] InnoDB: Shutdown completed; log sequence number 1625987
  <br>OK
  <br>
  <br>To start mysqld at boot time you have to copy
  <br>support-files/mysql.server to the right place for your system
  <br>
  <br>PLEASE REMEMBER TO SET A PASSWORD FOR THE MySQL root USER !
  <br>To do so, start the server, then issue the following commands:
  <br>
  <br> ./bin/mysqladmin -u root password 'new-password'
  <br> ./bin/mysqladmin -u root -h cp01-kanpiaoxue-org.epc.com password 'new-password'
  <br>
  <br>Alternatively you can run:
  <br>
  <br> ./bin/mysql_secure_installation
  <br>
  <br>which will also give you the option of removing the test
  <br>databases and anonymous user created by default. This is
  <br>strongly recommended for production servers.
  <br>
  <br>See the manual for more instructions.
  <br>
  <br>You can start the MySQL daemon with:
  <br>
  <br> cd . ; ./bin/mysqld_safe &amp;
  <br>
  <br>You can test the MySQL daemon with mysql-test-run.pl
  <br>
  <br> cd mysql-test ; perl mysql-test-run.pl
  <br>
  <br>Please report any problems at http://bugs.mysql.com/
  <br>
  <br>The latest information about MySQL is available on the web at
  <br>
  <br> http://www.mysql.com
  <br>
  <br>Support MySQL by buying support/licenses at http://shop.mysql.com
  <br>
  <br>New default config file was created as ./my.cnf and
  <br>will be used by default by the server when you start it.
  <br>You may edit this file to change server settings
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>使用上面文字中提到的：./bin/mysqladmin -u root -h cp01-kanpiaoxue-org.epc.com password 'new-password' 修改密码。</p> 
 <p>使用 ./bin/mysql -u root -h cp01-kanpiaoxue-org.epc.com -p 可以进行登录mysql。</p> 
 <p>如果使用localhost登录，如：&nbsp;<span style="line-height: 1.5;">.</span><span style="line-height: 1.5;">/bin/mysql -u root -p 登录，会报错如下：</span></p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  Access denied for user 'root'@'localhost' (using password: YES)
 </div> 
 <p><span style="line-height: 1.5;">&nbsp;怎么解决呢？很简单。使用&nbsp;</span><span style="line-height: 1.5;">.</span><span style="line-height: 1.5;">/bin/mysql -u root -h cp01-kanpiaoxue-org.epc.com -p 登录mysql，修改localhost以及密码即可。</span></p> 
 <p><span style="line-height: 1.5;"><span style="line-height: 1.5;">mysql&gt;&nbsp;</span>use mysql;</span></p> 
 <p><span style="line-height: 1.5;"><span style="line-height: 1.5;">mysql&gt;&nbsp;update user&nbsp;set&nbsp;password=PASSWORD('这里改成你的密码')&nbsp;where&nbsp;User='root';</span><br style="color: #333333; line-height: 24px; background-color: #f5f5f5;"><span style="line-height: 1.5;">mysql&gt;&nbsp;flush&nbsp;privileges;</span><br style="color: #333333; line-height: 24px; background-color: #f5f5f5;"><span style="line-height: 1.5;">mysql&gt;&nbsp;quit</span></span></p> 
 <p>&nbsp;</p> 
 <p>======== 小结</p> 
 <p>安装mysql的最好办法就是参考mysql官方文档的安装文档部分。没有比他更加权威的了。</p> 
 <p>&nbsp;</p> 
</div>