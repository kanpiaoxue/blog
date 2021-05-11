#python add utf-8 character set
###发表时间：2012-04-22
###分类：python
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1494096" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1494096</a>

---

<p>python 3.*以前的版本，打印汉字等亚洲字符，需要在.py文件的开头额外添加编码信息。这里我就是简单的写了一个添加utf-8编码的工具方法，方便自己使用。其实，在 pyDev IDE里面，可以给每个文件定义开头的。我的博客里面有。这里就给出一个可以遍历指定目录里面所有.py的文件，没有添加编码的，全部添加编码。</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<pre name="code" class="python">#-*-coding:utf-8-*-

'''
Created on 2012-4-22

@author: kanpiaoxue
'''
from string import strip
import os

class PythonUtil(object):
    UTF8_STRING = '#-*-coding:utf-8-*-'
    def __init__(self):
        pass
    def addAddUtf8(self, inputFile):
        needUtf8ListFiles = self.needUtf8(inputFile)
        count = len(needUtf8ListFiles)
        if count &gt; 0:
            for tmpFile in needUtf8ListFiles:
                print tmpFile, ' need to add ', self.UTF8_STRING
                readFile = None
                writeFile = None
                try:
                    readFile = open(tmpFile, 'r')
                    lines = readFile.readlines()
                    lines.insert(0, self.UTF8_STRING + '\n')
                    writeFile = open(tmpFile, 'w')
                    writeFile.writelines(lines)
                    print 'add ', self.UTF8_STRING, ' to ', tmpFile
                finally:
                    if readFile is not None:
                        readFile.close()
                    if writeFile is not None:
                        writeFile.flush()
                        writeFile.close()
        print '\n-------------- result report begin --------------'
        if count &gt; 0:
            print 'add ', self.UTF8_STRING, ' to ', count, ' files successfully.'
        else:
            print 'there are not any files needing to add ', self.UTF8_STRING
        print '--------------  result report end  --------------\n'
    
    def needUtf8(self, inputFile):
        needUtf8ListFiles = []
        if not os.path.isdir(inputFile):
            print '[', inputFile, '] is not a valid folder. Please check it.'
            return needUtf8ListFiles
        for root, dirs, files in os.walk(inputFile):
            for name in files:
                f = os.path.join(root, name)
                if f.endswith('.py') :
                    tmpFile = None
                    try:
                        tmpFile = open(f, 'r')
                        lines = tmpFile.readlines()
                        if len(lines) &gt; 0:
                            if strip(lines[0]) != self.UTF8_STRING:
                                needUtf8ListFiles.append(f)
                        else:
                            needUtf8ListFiles.append(f)
                    finally:
                        if tmpFile is not None:
                            tmpFile.close()
        return needUtf8ListFiles
                    

if __name__ == '__main__':
    f = r'E:\workspace_python'
    pythonUtil = PythonUtil()
    pythonUtil.addAddUtf8(f)

    
</pre>