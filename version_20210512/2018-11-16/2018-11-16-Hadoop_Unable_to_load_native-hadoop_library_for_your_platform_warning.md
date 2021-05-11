#Hadoop “Unable to load native-hadoop library for your platform” warning
###发表时间：2018-11-16
###分类：hadoop
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2433924" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2433924</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>Hadoop “Unable to load native-hadoop library for your platform” warning</p> 
 <p>&nbsp;</p> 
 <p>Hadoop Installation on Mac OS X：</p> 
 <p><a href="https://isaacchanghau.github.io/post/install_hadoop_mac/">https://isaacchanghau.github.io/post/install_hadoop_mac/</a></p> 
 <p>&nbsp;</p> 
 <p>Compile Apache Hadoop on Linux (fix warning: Unable to load native-hadoop library)</p> 
 <p><a href="http://www.ercoppa.org/posts/how-to-compile-apache-hadoop-on-ubuntu-linux.html">http://www.ercoppa.org/posts/how-to-compile-apache-hadoop-on-ubuntu-linux.html</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>Question:</p> 
 <p>I'm currently configuring hadoop on a server running CentOs. When I run start-dfs.sh or stop-dfs.sh, I get the following error:</p> 
 <p>WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable</p> 
 <p>I'm running Hadoop 2.2.0.</p> 
 <p>&nbsp;</p> 
 <p>Answer:</p> 
 <p>I assume you're running Hadoop on 64bit CentOS. The reason you saw that warning is the native Hadoop library $HADOOP_HOME/lib/native/libhadoop.so.1.0.0 was actually compiled on 32 bit.</p> 
 <p>Anyway, it's just a warning, and won't impact Hadoop's functionalities.</p> 
 <p>Here is the way if you do want to eliminate this warning, download the source code of Hadoop and recompile libhadoop.so.1.0.0 on 64bit system, then replace the 32bit one.</p> 
 <p>Steps on how to recompile source code are included here for Ubuntu:</p> 
 <p><a href="http://www.ercoppa.org/Linux-Compile-Hadoop-220-fix-Unable-to-load-native-hadoop-library.htm">http://www.ercoppa.org/Linux-Compile-Hadoop-220-fix-Unable-to-load-native-hadoop-library.htm</a></p> 
 <p>Good luck.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <h1 style="margin-top: 20px; margin-bottom: 10px; font-size: 36px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 500; line-height: 1.1; color: #333333;">Compile Apache Hadoop on Linux (fix warning: Unable to load native-hadoop library)</h1> 
 <p style="margin-bottom: 10px; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;">This tutorial explains how to compile Apache Hadoop 2.4.0 under Ubuntu Linux 13.10 amd64. You may want to compile Hadoop in order to fix the issue:</p> 
 <pre><code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: inherit; padding: 0px; color: inherit; background-color: transparent; border-radius: 0px; white-space: pre-wrap;">WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable</code></pre> 
 <ul style="margin-bottom: 10px; color: #333333; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif;"> 
  <li style="">Install a JDK: Oracle JDK (suggested) or package&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">openjdk-7-jdk</code> </li> 
  <li style="">Install&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">maven</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">libssl-dev</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">build-essential</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">pkgconf</code>, and&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">cmake</code>.</li> 
  <li style=""> <p style="margin-bottom: 10px;">Install the library&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">protobuf</code>:</p> 
   <ul style="margin-bottom: 0px;"> 
    <li style=""> <p style="margin-bottom: 10px;">If you are running Ubuntu 13.10 or earlier then install locally&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">protobuf-2.5.0</code>&nbsp;and insert it in the PATH:</p> <pre><code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: inherit; padding: 0px; color: inherit; background-color: transparent; border-radius: 0px; white-space: pre-wrap;">cd protobuf-2.5.0/
./configure --prefix=`pwd`/inst/bin &amp;&amp; make &amp;&amp; make install
export PATH=`pwd`/inst/bin:$PATH</code></pre> </li> 
    <li style=""> <p style="margin-bottom: 10px;">Otherwise (Ubuntu 14.04 or newer):</p> <pre><code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: inherit; padding: 0px; color: inherit; background-color: transparent; border-radius: 0px; white-space: pre-wrap;">sudo apt-get install libprotobuf8 protobuf-compiler</code></pre> </li> 
   </ul> </li> 
  <li style="">Download Hadoop sources.</li> 
  <li style=""> <p style="margin-bottom: 10px;">Compile Apache Hadoop:</p> <pre><code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: inherit; padding: 0px; color: inherit; background-color: transparent; border-radius: 0px; white-space: pre-wrap;">tar xvf hadoop-2.4.0-src.tar.gz
cd hadoop-2.4.0-src
mvn package -Pdist,native -DskipTests -Dtar</code></pre> <p style="margin-bottom: 10px;">Check&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">hadoop-dist/target/hadoop-2.4.0.tar.gz</code>&nbsp;(e.g., use this as your hadoop binary) or&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">hadoop-dist/target/hadoop-2.4.0</code>. If you have already installed a 32bit Hadoop, then you need only to replace the native libs in&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">$HADOOP/lib/</code>&nbsp;with the new native libs (<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">hadoop-dist/target/hadoop-2.4.0/lib</code>) and remove (if applicable) from&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">$HADOOP/etc/hadoop-env.sh</code>:</p> <pre><code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: inherit; padding: 0px; color: inherit; background-color: transparent; border-radius: 0px; white-space: pre-wrap;">export HADOOP_COMMON_LIB_NATIVE_DIR="~/hadoop/lib/"
export HADOOP_OPTS="$HADOOP_OPTS -Djava.library.path=~/hadoop/lib/"</code></pre> </li> 
  <li style="">You can delete Hadoop (and Protobuf sources if Ubuntu 13.10 or earlier).</li> 
 </ul> 
</div>