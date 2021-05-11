#python FAQ 问答题集锦（二）
###发表时间：2012-05-09
###分类：python,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1520584" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1520584</a>

---

<p>1、python 操作excel</p>
<p>excel是人们日常惯用的电子文档格式，所以python对excel的操作显得格外重要。</p>
<p>用到python的excel库 xlutils，</p>
<p>资源地址：http://www.python-excel.org/</p>
<p>例子：</p>
<p>公司对游戏内数据的销售物品的汇率进行上传操作，每次上传之前需要对数据的格式进行验证。上传的文件就是excel。</p>
<p>该excel共6个列，具体格式如下：</p>
<p>格式描述：游戏ID + 物品ID + 物品名称 &nbsp;+ 物品单价 &nbsp;+ 物品有效期 &nbsp;+ 物品类型</p>
<p>对格式的要求：</p>
<p>a、保证每一行，必须有6列数据</p>
<p>b、游戏ID + 物品ID 组成数据的主键，所以不允许 游戏ID + 物品ID 出现重复的情况</p>
<p>c、游戏ID ， 物品ID，必须是数字</p>
<p>d、物品单价，必须是合法的数字</p>
<p>代码如下：</p>
<p>&nbsp;</p>
<pre name="code" class="python">class OverseaRate(object):
        '''
        海外游戏，物品数据汇率上传excel文件格式检查
        '''
        '''
2002    24748    灿烂绚羽装护腕    0    -1    暂无
2002    561    条纹小礼服腕    0    -1    暂无
2002    3955    精灵裙鞋子    0    -1    暂无
2002    4259    晚礼服鞋    0    -1    暂无
2002    4261    绣花鞋    0    -1    暂无
2002    4273    蝴蝶裙鞋子    0    -1    暂无
        '''
    
    
        INIT_PATTERN = '^\d+$'
        PRICE_PATTERN = '^\d+(\.\d+)?$'
        VALID_LENGTH = 6
        
        def __init__(self, excelFile):
            self.excelFile = excelFile
            
        def checkOverseaRate(self):
            rs = self.getDatas()
            flag = self.checkPrimaryKey(rs)
            if flag:
                if self.checkFormat(rs):
                    print '检查完成，数据没有异常，可以上传'
                    
        def checkFormat(self, rs):
            initProg = re.compile(self.INIT_PATTERN)
            priceProg = re.compile(self.PRICE_PATTERN)
            rowNum = 0
            flag = True
            for row in rs:
                rowNum += 1
                gameId = self.dealFloatNum(row[0])
                itemId = self.dealFloatNum(row[1])
                price = self.dealFloatNum(row[3])
       
                gameIdMatch = initProg.match(gameId)
                itemIdMatch = initProg.match(itemId)
                priceMatch = priceProg.match(price)
                
                if not self.match(gameIdMatch):
                    self.getErrorMsg('游戏ID', rowNum, gameId)
                    flag = False
                if not self.match(itemIdMatch):
                    self.getErrorMsg('物品ID', rowNum, itemId)
                    flag = False
                if not self.match(priceMatch):
                    self.getErrorMsg('物品单价', rowNum, price)
                    flag = False
            return flag

        def getErrorMsg(self, msg, rowNum, row):
            print 'Error:' + msg + '，数据格式不正确！\t行数：', rowNum, ',错误数据内容：', row 
            
        def match(self, m):
            return True if m else False
        
        def dealFloatNum(self, row):
            return row[0:-2:] if row.endswith('.0') else row
        
        def checkPrimaryKey(self, rs):
            s = Set()
            rowNum = 0;
            flag = True
            for row in rs:
                rowNum += 1
                
                length = len(row)
                if self.VALID_LENGTH != length:
                    tmp = abs(self.VALID_LENGTH - length)
                    self.getErrorMsg('数据条目相差了' + str(tmp) + '列数据', rowNum, row)
                    flag = False
                    continue
                
                val = row[0], row[1]
                if val not in s:
                    s.add(val)
                else:
                    flag = False
                    print 'Error:数据重复！行数：', rowNum, '重复数据：', val
            return flag
        
        def getDatas(self):    
            wb = open_workbook(self.excelFile)
            s = wb.sheets()[0]
            rs = []
            for row in range(s.nrows):
                values = []
                for col in range(s.ncols):
                    val = s.cell(row, col).value
                    values.append(str(val))
                rs.append(values)
            return rs</pre>
<p>&nbsp;</p>
<p>2、远程文件MD5校验</p>
<p>描述：远程服务器上面有很多的 .zip 包，是一次性部署到远程服务器上面的。为了保证数据的完整性和一致性，需要对这些 .zip包进行 MD5 校验。如果有MD5不一致的，就需要进行再次部署新的文件，直到MD5一致。</p>
<p>给定一个ip列表的 .txt文件，对这个文件中的所以IP进行扫描，分别到这些服务器的固定目录下载 .zip文件到本地目录，然后对这些本地的文件进行MD5校验。</p>
<p>&nbsp;</p>
<p>patchIP.txt</p>
<p>&nbsp;</p>
<pre name="code" class="html">127.0.0.1
127.0.0.2
127.0.0.3
127.0.0.4
127.0.0.5
127.0.0.6
127.0.0.7</pre>
<p>&nbsp;python的代码如下：</p>
<p>&nbsp;</p>
<pre name="code" class="python">class CheckMd5(object):    
    def __init__(self, ipFile):
        self.ipFile = ipFile
        self.tmpUrl = r'D:\tmp'
        self.srcName = 'newupdateinfo.zip'
        
    def createTmpFolder(self, filePath):
        if not os.path.isdir(filePath):
            print 'start to create folder: ', filePath
            os.mkdir(filePath)
            
    def clearFolder(self, filePath):
        print 'start to clear ', filePath
        for root, dirs, fileNames in os.walk(filePath):
            for fileName in fileNames:
                tmpPath = os.path.join(root, fileName)
                os.remove(tmpPath)
                
    def downZips(self):
        self.createTmpFolder(self.tmpUrl)
        self.clearFolder(self.tmpUrl)
        count = 0
        for line in open(self.ipFile):
            line = line.strip()
            source = 'http://' + line + '/sgsj/' + self.srcName
            print 'start to wget [' + source + ']'
            cmd = r'"D:\Program Files (x86)\GnuWin32\bin\wget" --directory-prefix=' + self.tmpUrl + ' ' + source
            subprocess.Popen(cmd, shell=True).wait()
            self.changeZipName(line)
            count += 1
            print 'count: ', count, ',\tip:', line, 'is over'
            
    def changeZipName(self, line):
        print '-------- start to rename -------'
        old = os.path.join(self.tmpUrl, self.srcName)
        new = os.path.join(self.tmpUrl, line + '.zip')
        os.rename(old, new)
        print 'old', old
        print 'new', new
        print '-------- finished renaming -----'
    
    def createMd5List(self):
        md5Set = Set()
        for root, dirs, fileNames in os.walk(self.tmpUrl):
            for fileName in fileNames:
                filePath = os.path.join(root, fileName)
                md5Str = self.createFileMd5(filePath)
                
                print '%.500s\t:\t%s' % (filePath, md5Str if md5Str in md5Set else '\t--&gt;\t' + md5Str)
                md5Set.add(md5Str)
                
                
        print '*' * 10, ' md5 result start ', '*' * 10
        if 1 == len(md5Set):
            print 'check finished: all md5 is the same one. [Successfully!]'
        else:
            print 'Error: found different md5 in result. Please check it. [Failure!]'
        print '*' * 11, ' md5 result end ', '*' * 11
    
    def createFileMd5(self, filePath):
        '''
        文件生成MD5码，不行用二进制流的形式open(f,'rb')读出数据，对它进行操作。
        如果按照f.readlines()读取，那么文件无法保留原有的格式，造成MD5生成不一致。
        '''
        m = hashlib.md5()
        with open(filePath, 'rb') as f:#必须用二进制格式读取 'rb'
            b = f.read(1024)
            while b != b'':  
                m.update(b)  
                b = f.read(1024)
        #m.update(f.read()) # 可以采用这种形式，对于大于1024字节的文件效率不高，这里尝试每次读取 1024 字节
        return m.hexdigest().upper()
        
if __name__ == '__main__':
    checkMd5 = CheckMd5(r'E:\python_workspace\learningPython\src\sgcqip.txt')
    checkMd5.downZips()
    checkMd5.createMd5List()</pre>
<p>&nbsp;</p>
<p>上面下载文件到本地，用到了一个 wget的工具，该工具模仿Linux下面的 wget ，下载地址：&nbsp;<a href="http://gnuwin32.sourceforge.net/packages/wget.htm">http://gnuwin32.sourceforge.net/packages/wget.htm</a></p>
<p>3、</p>
<p>4、</p>
<p>5、</p>