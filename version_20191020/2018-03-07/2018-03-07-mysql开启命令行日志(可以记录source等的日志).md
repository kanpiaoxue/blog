#mysql开启命令行日志（可以记录source等的日志）
###发表时间：2018-03-07
###分类：mysql,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2412386" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2412386</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我们有的时候使用mysql的client登录命令行执行一些sql，在操作的过程中希望记录这些内容，该如何操作呢？比如我们使用source一个sql文件的时候，我想看看source过程中是否出现问题。如果sql文件很庞大，那么错误日志很快就从屏幕消失了，来不及查看。怎么操作呢？</p> 
 <p>这个时候我们可以使用mysql命令行中的tee命令打开一个log的文件，后续所有的同一个session操作都会记录到这个文件中。</p> 
 <p>如：</p> 
 <p>mysql&gt; tee hello.log</p> 
 <p>mysql&gt;select now() ;</p> 
 <p>mysql&gt;exit;&nbsp; //退出mysql 客户端</p> 
 <p>查看 hello.log 文件内容如下：</p> 
 <div class="quote_div">
  mysql&gt; select now();
  <br>+---------------------+
  <br>| now() |
  <br>+---------------------+
  <br>| 2018-03-07 10:55:58 |
  <br>+---------------------+
  <br>1 row in set (0.00 sec)
  <br>
  <br>mysql&gt; exit
 </div> 
 <p>&nbsp;可以为 tee 的日志文件指定目录，如：</p> 
 <p>mysql&gt; tee ~/hello.log</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考链接：&nbsp;<a href="https://techglimpse.com/redirect-output-of-mysql-source-command-to-log-file/">https://techglimpse.com/redirect-output-of-mysql-source-command-to-log-file/</a></p> 
 <p>&nbsp;</p> 
 <p><span style="color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">So if you want to redirect output of MySQL&nbsp;</span><code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px; color: #595959; white-space: normal;">source</code><span style="color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">&nbsp;command into a log file, then you need to use ‘</span><code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px; color: #595959; white-space: normal;">tee</code><span style="color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">‘. Here’s how it works.</span></p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">Step 1:</span>&nbsp;Login to MySQL</p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">Step 2:</span>&nbsp;In the MySQL command prompt, type the below command.</p> 
 <pre>mysql&gt; tee log.out
Logging to file 'log.out'
mysql&gt;</pre> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">You should see a message “Logging to file” displayed on the screen.</p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">Step 3:</span>&nbsp;Now, source the SQL file</p> 
 <pre>mysql&gt; source sample.sql</pre> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">Step 4:</span>&nbsp;The output of&nbsp;<code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px;">source</code>&nbsp;command would have been logged into a file&nbsp;<code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px;">log.out</code>.</p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">Step 5:</span>&nbsp;View the&nbsp;<code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px;">log.out</code></p> 
 <pre>$ more log.out</pre> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">That’s it!</p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">Why would you (or Mr. Waseem) wants to log the output of source SQL? For example, the SQL file that you would like to import might come with long list of tables &amp; records and while sourcing it, there are chances few of the records might not get imported. Now what if you want to know which of those records failed during import? The log file will help you to find that.</p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">Note</span>:&nbsp;<code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px;">'tee'</code>&nbsp;command can be used before executing any MySQL statement. The output of any query after logging the session will be stored in the specified file.</p> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;"><span style="font-weight: bolder;">For example:</span></p> 
 <pre>mysql&gt; tee showdboutput.out
Logging to file 'showdboutput.out'
mysql&gt; show databases;</pre> 
 <p style="margin-bottom: 22px; color: #595959; font-family: Roboto, Helvetica, Arial, sans-serif; font-size: 17px;">The output of the above query will be stored in&nbsp;<code style="font-family: Consolas, 'Liberation Mono', Courier, monospace; font-size: 16.15px; border-radius: 3px; background-color: #f7f7f7; padding: 2px 4px;">showdboutput.out</code>&nbsp;file.</p> 
 <p>&nbsp;</p> 
</div>