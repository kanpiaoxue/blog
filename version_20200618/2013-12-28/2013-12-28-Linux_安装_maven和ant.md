#Linux 安装 maven和ant
###发表时间：2013-12-28
###分类：Linux,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1996855" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1996855</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在Linux上面安装maven。</p> 
 <p>到apache的官网下载最新版本的maven：<a style="font-size: 12px; line-height: 1.5;" href="http://maven.apache.org/download.cgi">http://maven.apache.org/download.cgi</a></p> 
 <p>把maven程序放在&nbsp;/usr/local/program_for_java/ 文件夹下面，进行解压：</p> 
 <pre name="code" class="java">tar xzvf apache-maven-3.1.1-bin.tar.gz </pre> 
 <p>&nbsp;然后进入解压之后的目录：</p> 
 <pre name="code" class="java">cd apache-maven-3.1.1/</pre> 
 <p>&nbsp;<span style="font-family: Arial; font-size: 12px; line-height: 1.5;">配置环境变量，编辑/etc/profile文件，添加如下代码</span></p> 
 <pre name="code" class="java">MAVEN_HOME=/usr/local/program_for_java/apache-maven-3.1.1
export MAVEN_HOME
export PATH=${PATH}:${MAVEN_HOME}/bin</pre> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">&nbsp;</span><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">保存文件，并运行如下命令使环境变量生效</span></p> 
 <pre name="code" class="java">source /etc/profile</pre> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">&nbsp;测试maven是否安装成功，执行下面的命令查看maven的版本信息：</span></p> 
 <pre name="code" class="java">mvn -v</pre> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">&nbsp;显示如下：</span></p> 
 <pre name="code" class="java">Apache Maven 3.1.1 (0728685237757ffbf44136acec0402957f723d9a; 2013-09-17 08:22:22-0700)
Maven home: /usr/local/program_for_java/apache-maven-3.1.1
Java version: 1.6.0_45, vendor: Sun Microsystems Inc.
Java home: /usr/local/jdk1.6.0_45/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "2.6.32-131.0.15.el6.x86_64", arch: "amd64", family: "unix"</pre> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">&nbsp;说明maven已经安装成功</span></p> 
 <p>&nbsp;</p> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">安装ant和mavn相似。</span></p> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">下面仅给出ant的配置项：</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">ANT_HOME=/usr/local/program_for_java/apache-ant-1.9.3
export ANT_HOME
export PATH=${PATH}:${ANT_HOME}/bin</pre> 
 <p><span style="font-family: Arial; font-size: 12px; line-height: 1.5;">&nbsp;</span></p> 
</div>