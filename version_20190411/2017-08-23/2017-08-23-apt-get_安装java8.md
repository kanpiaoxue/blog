#apt-get 安装java8
###发表时间：2017-08-23
###分类：Linux,ubuntu,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2390918" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2390918</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p># echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list</p> 
 <p><span style="line-height: 1.5;">#</span><span style="line-height: 1.5;">&nbsp;</span>echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list</p> 
 <p><span style="line-height: 1.5;">#</span><span style="line-height: 1.5;">&nbsp;</span>apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886</p> 
 <p><span style="line-height: 1.5;">#</span><span style="line-height: 1.5;">&nbsp;</span>apt-get update</p> 
 <p><span style="line-height: 1.5;">#</span><span style="line-height: 1.5;">&nbsp;</span>apt-get install oracle-java8-installer</p> 
</div>