#python FAQ 问答题集锦（一）
###发表时间：2012-05-02
###分类：python,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1507574" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1507574</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>自己写了几个常用的python小函数，用于练习和日常使用：(Python版本：python2.7)</p> 
 <p>&nbsp;</p> 
 <p>0、文件的编码：</p> 
 <p>很多初学python的朋友，经常遇到文件编码问题。处理不当，会出现乱码，严重的，会因为在文件内写入不同格式的编码python代码，造成python无法编译。</p> 
 <p>这里给出解决的方法：推荐大家使用utf-8编码，它不仅包含了西欧的字符集，还包含了亚洲等地区的字符集。</p> 
 <p>在python的.py文件的第一行，写入：#-*-coding:utf-8-*-</p> 
 <p>或者为：&nbsp;#encoding=utf-8</p> 
 <p>如：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">#-*-coding:utf-8-*-


# some python code here</pre> 
 <p>&nbsp;</p> 
 <p>这样，就解决了问题。</p> 
 <p>&nbsp;</p> 
 <p>1、按照正则表达式，在指定的目录中查找匹配的文件列表</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">def seachFiles(folder, pattern):
    '''
    @param folder: 指定检索的目录
    @param pattern: 指定检索匹配的正则表达式
    '''
    if not os.path.isdir(folder):
        print 'Error:', folder, 'is not a valid folder.'
        return None
    else:
        rs = []
        prog = re.compile(pattern)
        for tmp in os.walk(folder):
            root = tmp[0]
            fileNames = tmp[2]
            for fileName in fileNames:
                path = os.path.join(root, fileName).strip()
                m = prog.match(path)
                if m :
                    rs.append(path)
        return rs</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>2、对指定的文件，统计文件内容的行数</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">def countFileRows(path): 
    '''
    @param path: 需要统计行数的文件名称
    '''
    if not os.path.isfile(path):
        print 'Error:', path, 'is not a valid path.'
        return None
    else:
        with open(path, 'r') as f:
            return len(f.readlines())</pre> 
 <p>&nbsp;</p> 
 <p>3、对指定文件列表，按照正则表达式对文件列表中的每个文件的每一行进行匹配，把匹配的结果作为列表返回</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">def matchLines(files, pattern):
    '''
    @param files: 需要扫描的文件的列表[r'c:\hello.txt',r'c:\world.txt']
    @param pattern: 需要匹配的正则表达式
    '''
    if files is None or 0 == len(files) or pattern is None:
        print 'Error: please check args'
    else:
        lst = []
        prog = re.compile(pattern)
        for tmpFile in files:
            if not os.path.isfile(tmpFile):
                print 'Error:', tmpFile, 'is not a valid tmpFile'
            else:
                with open(tmpFile) as f:
                    for tmpStr in f:
                        line = tmpStr.strip()
                        if line == '':
                            continue
                        else:
                            m = prog.match(line)
                            if m:
                                lst.append(line)
        return lst</pre> 
 <p>&nbsp; &nbsp;这里在给出一个精简版的代码，主要是利用python的列表解析功能：</p> 
 <pre name="code" class="python">def matchLinesListAnalysis(files, pattern):
    lst = []
    prog = re.compile(pattern)
    for tmpFile in files:
        lst += [line for line in open(tmpFile) if prog.match(line.strip())]
    return lst</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>4、得到指定范围(_range)，指定个数(count)的具有重复元素的列表</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">def createRandomNumber(_range, count):
    '''
    @note: 得到指定范围(_range)，指定个数(count)的具有重复元素的列表
    @param _range: 随机数的范围
    @param count: 随机数的个数
    '''
    return [int(math.floor(random.random() * _range)) for x in range(count)]</pre> 
 <p>&nbsp;</p> 
 <p>5、输入一个具有重复元素的列表，生成一个字典。 这个字典的key就是列表的元素，字典的value是该元素在列表中重复出现的次数</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">def countRepeat(lst):
    '''
    @note: 输入一个具有重复元素的列表，生成一个字典。 这个字典的key就是列表的元素，字典的value是该元素在列表中重复出现的次数
    @param lst: 具有重复元素的列表 
    '''
    if lst is None or 0 == len(lst):
        print 'Error: args is None or empty.'
        return None
    else:
        d = {}
        for key in lst:
            d[key] = d.get(key, 0) + 1
        return d</pre> 
 <p>&nbsp;</p> 
 <p>6、python实现定时任务，APScheduler定时框架的简单示例</p> 
 <p>APScheduler的内容请参考：&nbsp;<a href="http://packages.python.org/APScheduler/index.html">http://packages.python.org/APScheduler/index.html</a></p> 
 <p>示例：间隔 1 秒钟，打印一句话</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">class SchedulerTest(object):
    def __init__(self):
        self.sched = Scheduler(daemonic=False)
        print  self.sched
    def start(self):
        self.sched.add_cron_job(self.job, year='*', month='*', day='*', hour='*', minute='*', second='*/2', args=['hehe'])
        self.sched.start()
    def job(self, word):
        print 'say ', word</pre> 
 <p>&nbsp;</p> 
 <p>7、文件列求和函数</p> 
 <p>描述：给定一个文件，文件的第一列输入数字。用python编写一个函数，将该列的所有数字求和</p> 
 <p>目的：练习文件操作，列表解析的操作</p> 
 <p>文件的内容如下：C:\Users\test\Desktop\new &nbsp;2.txt</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">1
2
3

3.2 

-1000

1236.55 </pre> 
 <p>&nbsp;python的函数如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">def calculateColumn(f):
    return sum([float(x.strip()) for x in open(f) if x.strip() != ''])</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>8、数据查出记录，在该记录中进行数据筛选。（其实可以通过SQL的where子句中实现筛选）</p> 
 <p>[('tom', '12', 'm'), ('jack', '12', 'm'), ('lucy', '12', 'w'), ('mery', '13', 'w'), ('jack', '23', 'm')]</p> 
 <p>找出其中年纪12岁的，女性成员</p> 
 <p>代码如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">    f = [('tom', '12', 'm'), ('jack', '12', 'm'), ('lucy', '12', 'w'), ('mery', '13', 'w'), ('jack', '23', 'm')]
    print [x for x in f if x[1] == '12' and x[2] == 'w']</pre> 
 <p>&nbsp;</p> 
 <p>9、链接MySQL数据库</p> 
 <p>为了进行MySQL的数据库连接，插入数据，查询数据，需要进行一些前期的准备，主要是连接MySQL数据的lib的安装。</p> 
 <p>我使用的是&nbsp;MySQLdb。下载地址：</p> 
 <p><a href="http://sourceforge.net/projects/mysql-python/">http://sourceforge.net/projects/mysql-python/</a></p> 
 <p>或者：</p> 
 <p><a href="http://www.codegood.com/">http://www.codegood.com/</a></p> 
 <p>文档：</p> 
 <p><a href="http://mysql-python.sourceforge.net/MySQLdb.html">http://mysql-python.sourceforge.net/MySQLdb.html</a></p> 
 <p>我自己写了一个小例子</p> 
 <p>描述：创建一个数据库 testdb，创建一个表 user_info（建表语句见下例）.用MySQLdb插入数据，然后进行查询。</p> 
 <p>目的：配置文件的读取，MySQL数据的连接，数据的插入，数据的查询</p> 
 <p>表user_info的建表语句如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="sql">create database testdb;
    use testdb;
    create table user_info(
        id bigint(20) auto_increment,
        name varchar(30) not null,
        sex varchar(1) not null,
        email varchar(50),
        primary key (id)
    ) ENGINE=MyISAM AUTO_INCREMENT=1 DEFAULT CHARSET=gbk;</pre> 
 <p>&nbsp;python的代码如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">class User(object):    
    def __init__(self, id, name, sex, email):
        self.id = id
        self.name = name
        self.sex = sex
        self.email = email
        
class MySQLTest(object):
    '''
    create database testdb;
    use testdb;
    create table user_info(
        id bigint(20) auto_increment,
        name varchar(30) not null,
        sex varchar(1) not null,
        email varchar(50),
        primary key (id)
    ) ENGINE=MyISAM AUTO_INCREMENT=1 DEFAULT CHARSET=gbk;
    '''
    def __init__(self, configFile):
        self.config = ConfigParser.ConfigParser()
        self.config.read(configFile)
        self.section = 'mysql_connection_1'
        
    def getConnection(self):
        host = self.config.get(self.section, 'host')
        user = self.config.get(self.section, 'user')
        passwd = self.config.get(self.section, 'passwd')
        db = self.config.get(self.section, 'db')
        port = self.config.getint(self.section, 'port')# getint
        charset = self.config.get(self.section, 'charset')
        conn = MySQLdb.connect(host=host, user=user, passwd=passwd, db=db, port=port, charset=charset)
        return conn
    
    def createUsers(self, count):
        conn = None
        cursor = None
        try:
            conn = self.getConnection()
            cursor = conn.cursor()
            for i in range(count):
                name = 'test-' + str(i)
                sex = 'w' if i % 2 == 0 else 'm'
                email = name + '@' + '163.com'
                sql = "insert into user_info(name,sex,email) values('" + name + "','" + sex + "','" + email + "')"
                cursor.execute(sql)
        except Exception as e:
            print e
        finally:
            if cursor:
                cursor.close()
            if conn :
                conn.close()    
            
    def getUserList(self):
        lst = []
        conn = None
        cursor = None
        try:
            conn = self.getConnection()
            cursor = conn.cursor()
            cursor.execute('select * from user_info')
            for tmp in cursor.fetchall():
                row = dict(zip([d[0] for d in cursor.description], tmp))
                user = User(row.get('id'), row.get('name'), row.get('sex'), row.get('email'))
                lst.append(user)
            return lst
        except Exception as e:
            print e
            return None
        finally:
            if cursor :
                cursor.close()
            if conn:
                conn.close()</pre> 
 <p>配置文件如下：E:\python_workspace\learningPython\src\congfig.ini&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">[mysql_connection_1]
host=localhost
user=root
passwd=root
db=testdb
port=3306
charset=utf8</pre> 
 <p>&nbsp;运行如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">if __name__ == '__main__':
    mySQLTest = MySQLTest(r'E:\python_workspace\learningPython\src\congfig.ini')
    #mySQLTest.createUsers(100)
    userList = mySQLTest.getUserList()
    for user in userList:
        print user.id, user.name, user.sex, user.email</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>10、日期计算，是人们日常经常遇到的一个问题。人们生活中，到处可以看见日期的影子。比如，生日，“今天”，“昨天”，“明天”，“某日至某日，XXX计划干什么事情”... 等等。</p> 
 <p>所以这里给出了一个DateUtils的类，里面记述了一些使用的日期小函数。这里的DateUtils的默认日期格式： yyyy-MM-dd</p> 
 <p>python代码如下：</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">class DateUtils(object):
    '''
    Date的工具类
           备注：本工具类，日期格式全部使用日期短格式：%Y-%m-%d
           例如：2012-01-01
    '''
    DATE_SHORT_PATTERN = r'(\d{4})-(\d{2})-(\d{2})'
    DATE_SHORT_FORMAT = '%Y-%m-%d'
    
    def __init__(self):
        pass
    
    def getMondayAndSundayByDate(self, dateStr):      
        '''
    @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周一和周日的日期元组，如： ('2012-05-07', '2012-05-13')
        '''
        monday = self.getMondayByDate(dateStr)
        sunday = self.getSundayByDate(dateStr)
        return (monday, sunday)
        
    def getMondayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周一 结果：2012-05-07
        '''
        
        return self._getWeekdayByDate(dateStr, 0)
    def getTuesdayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周二 结果：2012-05-08
        '''
        return self._getWeekdayByDate(dateStr, 1)
    def getWednesdayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周三 结果：2012-05-09
        '''
        return self._getWeekdayByDate(dateStr, 2)
    def getThursdayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周四 结果：2012-05-10
        '''
        return self._getWeekdayByDate(dateStr, 3)
    def getFridayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周五 结果：2012-05-11
        '''
        return self._getWeekdayByDate(dateStr, 4)
    def getSaturdayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周六 结果：2012-05-12
        '''
        return self._getWeekdayByDate(dateStr, 5)
    def getSundayByDate(self, dateStr):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09
        备注：得到输入的日期所在的周日 结果：2012-05-13
        '''
        return self._getWeekdayByDate(dateStr, 6)
    
    
    def _getWeekdayByDate(self, dateStr, weekday):
        '''
        @param dateStr: 输入的任意的天的字符串，如：2012-05-09 
        @param weekday: 周几的数字，从 0 - 6，是周一至周日
        备注：得到输入日期所在的周几的日期 
        '''
        d = self.parseDate(dateStr)
        if d.weekday() &gt; weekday:
            while d.weekday() != weekday:
                d -= datetime.timedelta(days=1)
        elif d.weekday() &lt; weekday:
            while d.weekday() != weekday:
                d += datetime.timedelta(days=1)
        return self.formartDate(d)
        
    def getYestoday(self):
        '''
        得到昨天的日期
        '''
        return datetime.date.today() - datetime.timedelta(days=1)
    
    def getToday(self):
        '''
        得到今天的日期
        '''
        return datetime.date.today()
    
    def getTomorrow(self):
        '''
        得到明天的日期
        '''
        return datetime.date.today() + datetime.timedelta(days=1)
    
    def getDateStrList(self, beginDate, endDate):
        '''
        得到两个日期之间的日期字符串列表（包含起始日期和结束日期）
        '''
        return [self.formartDate(x) for x in self.getDateList(beginDate, endDate)]
    
    def getDateList(self, beginDate, endDate):
        '''
        得到两个日期之间的日期列表（包含起始日期和结束日期）
        '''
        begin = self.parseDate(beginDate)
        end = self.parseDate(endDate)
        if begin &gt; end:
            print 'Error: beginDate is after endDate'
            return None
        else:
            return [begin + datetime.timedelta(days=i) for i in range(self.getDays(beginDate, endDate) + 1)] # days +1 包括结束日期
        
    def getDays(self, beginDate, endDate):
        '''
        得到两个日期之间的天数（包含起始日期，不包含结束日期）
        '''
        begin = self.parseDate(beginDate)
        end = self.parseDate(endDate)
        if begin &gt; end:
            print 'Error: beginDate is after endDate'
            return None
        else:
            return  (end - begin).days
    
    def parseDate(self, dateStr):
        '''
        以日期的短格式，转换日期字符串为日期类型
        '''
        prog = re.compile(self.DATE_SHORT_PATTERN)
        m = prog.match(dateStr)
        if m:
            return datetime.date(int(m.group(1)), int(m.group(2)), int(m.group(3)))
        else:
            print 'Error: can not match ' + self.DATE_SHORT_PATTERN
            return None
        
    def formartDate(self, date):
        '''
        以日期的短格式，格式化日期类型为字符串类型
        '''
        return date.strftime(self.DATE_SHORT_FORMAT)</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>11、python连接oracle</p> 
 <p>人们日常接触的数据库最多的莫过于mysql和Oracle了。现在这里介绍python连接oracle的方法，采用cx_Oracle模块</p> 
 <p>下载地址：</p> 
 <p><a href="http://cx-oracle.sourceforge.net/">http://cx-oracle.sourceforge.net/</a></p> 
 <p>文档地址：</p> 
 <p><a href="http://cx-oracle.sourceforge.net/html/index.html">http://cx-oracle.sourceforge.net/html/index.html</a></p> 
 <p>我下载的源码包是：cx_Oracle-5.0.4.tar.gz</p> 
 <p>python setup.py build</p> 
 <p>python setup.py install</p> 
 <p>如果遇到问题，请参考本博客里面关于安装cx_Oracle报错问题的解决方案。</p> 
 <p>python连接Oracle，我这里创建了一个user_info的表，插入测试用数据</p> 
 <p>user_info的SQL：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="sql">    create table user_info(
        id number(11),
        user_key varchar2(30),
        user_mobile number(11),
        primary key(id)
    );</pre> 
 <p>&nbsp;python的脚本：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="python">#-*-coding:utf-8-*-
import cx_Oracle
import os
os.environ['NLS_LANG'] = 'SIMPLIFIED CHINESE_CHINA.UTF8'

class User(object):
    def __init__(self, id, user_key, user_mobile):
        self.id = id
        self.user_key = user_key
        self.user_mobile = user_mobile

class OracleTest(object):
    '''
    create table user_info(
        id number(11),
        user_key varchar2(30),
        user_mobile number(11),
        primary key(id)
    );
    '''
    def __init__(self, url):
        self.url = url
        
    def getConnection(self):
        return cx_Oracle.connect(self.url)
    
    def getUserList(self): 
        conn = None
        cursor = None
        try:
            conn = self.getConnection()
            cursor = conn.cursor()
            sql = '''
            select id,user_key,user_mobile from user_info
            '''
            cursor.execute(sql)
            cursor.rowfactory = User
            #print cursor.description
            return [user for user in cursor]
        except Exception as e:
            print 'Error', e
            return None
        finally:
            if cursor:
                cursor.close()
            if conn:
                conn.close()

if __name__ == '__main__':
    url1 = 'test/test@192.168.0.1:1521/test'
    oracleTest = OracleTest(url1)
    for user in oracleTest.getUserList():
        print user.id, user.user_key, user.user_mobile
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>12、&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>13、</p> 
 <p>14、</p> 
 <p>15、</p> 
 <p>&nbsp;</p> 
</div>