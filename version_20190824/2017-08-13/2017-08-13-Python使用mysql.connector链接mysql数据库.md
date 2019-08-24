#Python使用mysql.connector链接mysql数据库
###发表时间：2017-08-13
###分类：python,mysql
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2389497" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2389497</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>之前一直使用pythond mysqldb链接数据库，随着mysql被oracle收购之后，我发现mysqldb就不怎么更新了。</p> 
 <p>现在开始使用oracle提供的mysql.connector来操作mysql。</p> 
 <p>下载mysql.connector地址：&nbsp;<a href="https://dev.mysql.com/downloads/connector/python/">https://dev.mysql.com/downloads/connector/python/</a></p> 
 <p>《MySQL Connector/Python Developer Guide》的地址：&nbsp;</p> 
 <p><a href="https://dev.mysql.com/doc/connector-python/en/">https://dev.mysql.com/doc/connector-python/en/</a></p> 
 <p>安装地址：&nbsp;<a href="https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html">https://dev.mysql.com/doc/connector-python/en/connector-python-installation.html</a></p> 
 <p>mysql 的社区版下载地址：&nbsp;<a href="https://dev.mysql.com/downloads/mysql/">https://dev.mysql.com/downloads/mysql/</a></p> 
 <p>安装 mysql 的文档地址：</p> 
 <ul> 
  <li>Windows：<a href="https://dev.mysql.com/doc/refman/5.7/en/mysql-installer-setup.html">https://dev.mysql.com/doc/refman/5.7/en/mysql-installer-setup.html</a> </li> 
  <li>Linux：<a href="https://dev.mysql.com/doc/refman/5.7/en/linux-installation.html">https://dev.mysql.com/doc/refman/5.7/en/linux-installation.html</a> </li> 
  <li>Mac：<a href="https://dev.mysql.com/doc/refman/5.7/en/osx-installation.html">https://dev.mysql.com/doc/refman/5.7/en/osx-installation.html</a> </li> 
 </ul> 
 <p>好用的 MySQL 的 SQL 开发工具（建模、执行 SQL、分析 SQL）：MySQL Workbench</p> 
 <p>下载地址： &nbsp;<a href="https://dev.mysql.com/downloads/workbench/">https://dev.mysql.com/downloads/workbench/</a></p> 
 <p>&nbsp;</p> 
 <p>举例：</p> 
 <pre name="code" class="python">#encoding=utf-8
'''
Created on 2017-8-12

@author: kanpiaoxue
'''


import mysql.connector


if __name__ == '__main__':
    
    config={'host':'127.0.0.1',#默认127.0.0.1
        'user':'root',
        'password':'hao123',
        'port':3306 ,#默认即为3306
        'database':'learn',
        'charset':'utf8'#默认即为utf8
        }
    conn=mysql.connector.connect(**config) #连接数据库
    cursor=conn.cursor()
    cursor.execute('select * from person') #表查询
    for (id,name,birthday) in cursor:
        print id,name,birthday
    cursor.close()
    conn.close()</pre> 
 <p>&nbsp;</p> 
 <p>这里仅仅是抛砖引玉，居然使用方法请参考官网的文档。</p> 
</div>