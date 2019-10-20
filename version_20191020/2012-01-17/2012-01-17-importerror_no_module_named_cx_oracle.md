#importerror no module named cx_oracle
###发表时间：2012-01-17
###分类：python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1354242" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1354242</a>

---

<p>我在Linux上面安装cx_oracle打包好的 rpm文件，总是报错&nbsp;importerror no module named cx_oracle。没有办法，我只好去cx_Oracle的官网&nbsp;<a href="http://cx-oracle.sourceforge.net/">http://cx-oracle.sourceforge.net/</a>&nbsp;下载了源程序，找到对应版本的“Source Code only”。自己进行编译。</p>
<p>python setup.py build</p>
<p>python setup.py install</p>
<p>&nbsp;</p>
<p>在运行程序，就OK了。</p>