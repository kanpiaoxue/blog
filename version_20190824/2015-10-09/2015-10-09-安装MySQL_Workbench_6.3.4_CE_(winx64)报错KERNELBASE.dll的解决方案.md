#安装MySQL Workbench 6.3.4 CE (winx64)报错KERNELBASE.dll的解决方案
###发表时间：2015-10-09
###分类：mysql,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2247763" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2247763</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>在 oracle 的官网下载了&nbsp;mysql-workbench-community-6.3.4-winx64-noinstall.zip 的压缩包，解压之后在 Windows 7 （64位） 机器上面运行，报错如下：</p> 
 <div class="quote_title">
  报错信息 写道
 </div> 
 <div class="quote_div">
  问题事件名称: APPCRASH
  <br> 应用程序名: MySQLWorkbench.exe
  <br> 应用程序版本: 6.3.4.0
  <br> 应用程序时间戳: 55758818
  <br> 故障模块名称: KERNELBASE.dll
  <br> 故障模块版本: 6.1.7601.17514
  <br> 故障模块时间戳: 4ce7c78c
  <br> 异常代码: e0434352
  <br> 异常偏移: 000000000000a49d
  <br> OS 版本: 6.1.7601.2.1.0.256.48
  <br> 区域设置 ID: 2052
  <br> 其他信息 1: 367e
  <br> 其他信息 2: 367e805d0e7c1ec3f63b05bb5ce5c416
  <br> 其他信息 3: 4d57
  <br> 其他信息 4: 4d57238a798bdf861a4d84c48ca0bf52
 </div> 
 <p>&nbsp;</p> 
 <p>在google上面找了一下，发现了官网给出的内容：</p> 
 <p>链接：　<a href="http://bugs.mysql.com/bug.php?id=61969">http://bugs.mysql.com/bug.php?id=61969</a></p> 
 <p>最有用的链接：　<a href="http://stackoverflow.com/questions/26864653/mysql-workbench-crash-on-start-on-windows">http://stackoverflow.com/questions/26864653/mysql-workbench-crash-on-start-on-windows</a></p> 
 <p>内容如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  got same error. found "_README_FOR_ZIP_PACKAGE.txt" file in "mysql-workbench-community-6.2.4-winx64-noinstall.zip." file says
  <br>------------------------------------------
  <br>MySQL Workbench needs the following prerequisites:
  <br>
  <br>Microsoft .NET Framework 4 Client Profile (http://www.microsoft.com/download/en/details.aspx?id=17113)
  <br>Visual C++ Redistributable for Visual Studio 2013 (http://www.microsoft.com/en-us/download/details.aspx?id=40784)
 </div> 
 <p>&nbsp;</p> 
 <p>我发现原来在&nbsp;<span style="line-height: 1.5;">&nbsp;mysql-workbench-community-6.3.4-winx64-noinstall.zip</span><span style="line-height: 1.5;">&nbsp; 解压之后的文件家里面就有解决方案的文件说明，文件如下：</span>_README_FOR_ZIP_PACKAGE.txt</p> 
 <p>内容如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  This readme describes the dependencies of MySQL Workbench when installed from the zip package on Windows.
  <br>
  <br>The normal setup using the msi package or an installation using the MySQL Installer both check if
  <br>any of the prerequisites MySQL Workbench needs are missing on the target system and warns the user
  <br>about this. Additionally, both allow to download the missing prerequisites.
  <br>
  <br>This doesn't happen when using the zip package and if any of the prerequisites is missing
  <br>MySQL Workbench will refuse to work without a good error message. So make sure you installed everything.
  <br>
  <br>MySQL Workbench needs the following prerequisites:
  <br>
  <br> Microsoft .NET Framework 4 Client Profile (http://www.microsoft.com/download/en/details.aspx?id=17113)
  <br> Visual C++ Redistributable for Visual Studio 2013 (http://www.microsoft.com/en-us/download/details.aspx?id=40784)
  <br>
  <br>Depending on which MySQL Workbench package you downloaded you either need the 32bit or 64bit version of the
  <br>Visual C++ runtime. It is essential that you pick the correct architecture.
 </div> 
 <p>&nbsp;</p> 
 <p>然后我就下载了上面提到的</p> 
 <p><span style="background-color: #fafafa;">Microsoft .NET Framework 4 Client Profile (http://www.microsoft.com/download/en/details.aspx?id=17113)</span><br><span style="background-color: #fafafa;">Visual C++ Redistributable for Visual Studio 2013 (http://www.microsoft.com/en-us/download/details.aspx?id=40784)</span></p> 
 <p><span style="background-color: #fafafa;">安装之后，</span><span style="line-height: 1.5;">mysql-workbench正常运行。</span></p> 
 <p><span style="line-height: 1.5;">【备注】大家注意一下，不同版本</span><span style="line-height: 1.5;">mysql-workbench的里面这个</span><span style="line-height: 1.5;">_README_FOR_ZIP_PACKAGE.txt文件的内容是不一样的，需要根据</span><span style="line-height: 1.5;">_README_FOR_ZIP_PACKAGE.txt里面的内容下载不同的补丁。</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>