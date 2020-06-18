#java -D arguments 参数
###发表时间：2011-12-16
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1313925" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1313925</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>-------------------- 对于如何给自己写的main传递参数，java用args[] 数组来解决。下面我给出自己的方法：</p> 
 <p>cmd 如下：</p> 
 <p>java -DmyParam1=hello,world com.test.Test</p> 
 <p>&nbsp;</p> 
 <p>class 类如下：</p> 
 <p>package com.test;</p> 
 <p>public class Test{</p> 
 <p>public static void main(String[] args){</p> 
 <p>System.out.println(System.getProperty("myParam1"));</p> 
 <p>// output: hello,world</p> 
 <p>}</p> 
 <p>}</p> 
 <p>&nbsp;</p> 
 <p>这样就省去了自己解析参数的部分。下面的说明，更详细的说明了这点。</p> 
 <p>&nbsp;</p> 
 <p>-------------------- 下面列出了 JAVA 自身运行需要的一些必要参数</p> 
 <p>-D set a system property(设置系统属性)&nbsp;<br style="padding: 0px; margin: 0px;">可通过语句System.getProperties().list(System.out);查看有哪些参数可以设置。&nbsp;<br style="padding: 0px; margin: 0px;">可设置的参数:&nbsp;<br style="padding: 0px; margin: 0px;">-- listing properties --&nbsp;<br style="padding: 0px; margin: 0px;">java.runtime.name=Java(TM) 2 Runtime Environment, Stand...&nbsp;<br style="padding: 0px; margin: 0px;">sun.boot.library.path=C:\Program Files\Java\jre1.5.0_08\bin&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.version=1.5.0_08-b03&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.vendor=Sun Microsystems Inc.&nbsp;<br style="padding: 0px; margin: 0px;">java.vendor.url=http://java.sun.com/&nbsp;<br style="padding: 0px; margin: 0px;">path.separator=;&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.name=Java HotSpot(TM) Client VM&nbsp;<br style="padding: 0px; margin: 0px;">file.encoding.pkg=sun.io&nbsp;<br style="padding: 0px; margin: 0px;">user.country=CN&nbsp;<br style="padding: 0px; margin: 0px;">sun.os.patch.level=Service Pack 2&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.specification.name=Java Virtual Machine Specification&nbsp;<br style="padding: 0px; margin: 0px;">user.dir=D:\wapSearchLogService&nbsp;<br style="padding: 0px; margin: 0px;">java.runtime.version=1.5.0_08-b03&nbsp;<br style="padding: 0px; margin: 0px;">java.awt.graphicsenv=sun.awt.Win32GraphicsEnvironment&nbsp;<br style="padding: 0px; margin: 0px;">java.endorsed.dirs=C:\Program Files\Java\jre1.5.0_08\lib...&nbsp;<br style="padding: 0px; margin: 0px;">os.arch=x86&nbsp;<br style="padding: 0px; margin: 0px;">java.io.tmpdir=C:\DOCUME~1\ADMINI~1\LOCALS~1\Temp\&nbsp;<br style="padding: 0px; margin: 0px;">line.separator=&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.specification.vendor=Sun Microsystems Inc.&nbsp;<br style="padding: 0px; margin: 0px;">user.variant=&nbsp;<br style="padding: 0px; margin: 0px;">os.name=Windows XP&nbsp;<br style="padding: 0px; margin: 0px;">sun.jnu.encoding=GBK&nbsp;<br style="padding: 0px; margin: 0px;">java.library.path=C:\Program Files\Java\jre1.5.0_08\bin...&nbsp;<br style="padding: 0px; margin: 0px;">java.specification.name=Java Platform API Specification&nbsp;<br style="padding: 0px; margin: 0px;">java.class.version=49.0&nbsp;<br style="padding: 0px; margin: 0px;">sun.management.compiler=HotSpot Client Compiler&nbsp;<br style="padding: 0px; margin: 0px;">os.version=5.1&nbsp;<br style="padding: 0px; margin: 0px;">user.home=C:\Documents and Settings\Administrator&nbsp;<br style="padding: 0px; margin: 0px;">user.timezone=Asia/Shanghai&nbsp;<br style="padding: 0px; margin: 0px;">java.awt.printerjob=sun.awt.windows.WPrinterJob&nbsp;<br style="padding: 0px; margin: 0px;">file.encoding=GBK&nbsp;<br style="padding: 0px; margin: 0px;">java.specification.version=1.5&nbsp;<br style="padding: 0px; margin: 0px;">user.name=Administrator&nbsp;<br style="padding: 0px; margin: 0px;">java.class.path=D:\wapSearchLogService\bin;D:\wapSear...&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.specification.version=1.0&nbsp;<br style="padding: 0px; margin: 0px;">sun.arch.data.model=32&nbsp;<br style="padding: 0px; margin: 0px;">java.home=C:\Program Files\Java\jre1.5.0_08&nbsp;<br style="padding: 0px; margin: 0px;">java.specification.vendor=Sun Microsystems Inc.&nbsp;<br style="padding: 0px; margin: 0px;">user.language=zh&nbsp;<br style="padding: 0px; margin: 0px;">awt.toolkit=sun.awt.windows.WToolkit&nbsp;<br style="padding: 0px; margin: 0px;">java.vm.info=mixed mode, sharing&nbsp;<br style="padding: 0px; margin: 0px;">java.version=1.5.0_08&nbsp;<br style="padding: 0px; margin: 0px;">java.ext.dirs=C:\Program Files\Java\jre1.5.0_08\lib...&nbsp;<br style="padding: 0px; margin: 0px;">sun.boot.class.path=C:\Program Files\Java\jre1.5.0_08\lib...&nbsp;<br style="padding: 0px; margin: 0px;">java.vendor=Sun Microsystems Inc.&nbsp;<br style="padding: 0px; margin: 0px;">file.separator=\&nbsp;<br style="padding: 0px; margin: 0px;">java.vendor.url.bug=http://java.sun.com/cgi-bin/bugreport...&nbsp;<br style="padding: 0px; margin: 0px;">sun.cpu.endian=little&nbsp;<br style="padding: 0px; margin: 0px;">sun.io.unicode.encoding=UnicodeLittle&nbsp;<br style="padding: 0px; margin: 0px;">sun.desktop=windows&nbsp;<br style="padding: 0px; margin: 0px;">sun.cpu.isalist=amd64<br style="padding: 0px; margin: 0px;">这样就可以在java中通过System.getProperty(“propertyName”) 获得环境变量设置的值</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><span style="background-color: #888888; color: #ff0000;">---------------------------------- 参考 ------------------</span></p> 
 <p>其他的java的运行参数：</p> 
 <h3 style="font-size: 16px; padding-top: 10px;"><a style="color: #108ac6; text-decoration: underline;" href="http://xinklabi.iteye.com/blog/837435">Java命令行运行参数说明大全</a></h3> 
 <p>地址：<a href="http://xinklabi.iteye.com/blog/837435">http://xinklabi.iteye.com/blog/837435</a></p> 
</div>