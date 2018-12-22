#python 操作 mysql
###发表时间：2015-10-27
###分类：mysql,python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2252522" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2252522</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：<a href="http://www.cnblogs.com/rollenholt/archive/2012/05/29/2524327.html">http://www.cnblogs.com/rollenholt/archive/2012/05/29/2524327.html</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">import MySQLdb
 
try:
    conn=MySQLdb.connect(host='localhost',user='root',passwd='root',db='test',port=3306)
    cur=conn.cursor()
    cur.execute('select * from user')
    cur.close()
    conn.close()
except MySQLdb.Error,e:
     print "Mysql Error %d: %s" % (e.args[0], e.args[1])
     
     
import MySQLdb
 
try:
    conn=MySQLdb.connect(host='localhost',user='root',passwd='root',port=3306)
    cur=conn.cursor()
     
    cur.execute('create database if not exists python')
    conn.select_db('python')
    cur.execute('create table test(id int,info varchar(20))')
     
    value=[1,'hi rollen']
    cur.execute('insert into test values(%s,%s)',value)
     
    values=[]
    for i in range(20):
        values.append((i,'hi rollen'+str(i)))
         
    cur.executemany('insert into test values(%s,%s)',values)
 
    cur.execute('update test set info="I am rollen" where id=3')
 
    conn.commit()
    cur.close()
    conn.close()
 
except MySQLdb.Error,e:
     print "Mysql Error %d: %s" % (e.args[0], e.args[1])
     
     
import MySQLdb
 
try:
    conn=MySQLdb.connect(host='localhost',user='root',passwd='root',port=3306)
    cur=conn.cursor()
     
    conn.select_db('python')
 
    count=cur.execute('select * from test')
    print 'there has %s rows record' % count
 
    result=cur.fetchone()
    print result
    print 'ID: %s info %s' % result
 
    results=cur.fetchmany(5)
    for r in results:
        print r
 
    print '=='*10
    cur.scroll(0,mode='absolute')
 
    results=cur.fetchall()
    for r in results:
        print r[1]
     
 
    conn.commit()
    cur.close()
    conn.close()
 
except MySQLdb.Error,e:
     print "Mysql Error %d: %s" % (e.args[0], e.args[1])          </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>