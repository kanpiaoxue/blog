#cx_Oracle找不到libclntsh.so.11.1错误
###发表时间：2012-02-07
###分类：python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1396649" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1396649</a>

---

<p><span style="font-size: x-small;">装完cx_Oracle之后，运行import cx_Oracle，报如下错误：</span></p>
<p><span style="font-size: x-small;">&gt;&gt;&gt;import cx_Oracle</span></p>
<p><span style="font-size: x-small;">Traceback (most recent call last):</span></p>
<p><span style="font-size: x-small;">&nbsp;File "&lt;stdin&gt;",line 1, in &lt;module&gt;</span></p>
<p><span style="font-size: x-small;">&nbsp;ImportError: libclntsh.so.11.1: cannot open shared object file: No such file or directory</span></p>
<p><span style="font-size: x-small;"><br></span></p>
<p><span style="font-size: x-small;">解决方案如下：</span></p>
<p> </p>
<p style="font-family: Helvetica, Tahoma, Arial, sans-serif; line-height: 25px; text-align: left; padding: 0px;"><span style="font-size: x-small;">在/etc/profile中添加</span></p>
<p style="font-family: Helvetica, Tahoma, Arial, sans-serif; line-height: 25px; text-align: left; padding: 0px;"> </p>
<p style="padding: 0px;"><span style="font-size: x-small;">LD_LIBRARY_PATH=$ORACLE_HOME/lib:/usr/lib:/usr/local/lib;<br>export LD_LIBRARY_PATH<br>然后可以用source /etc/profile 生效一下</span></p>