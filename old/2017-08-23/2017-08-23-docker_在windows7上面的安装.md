#docker 在windows7上面的安装
###发表时间：2017-08-23
###分类：docker
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2390905" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2390905</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>我想在windows7安装docker，之前在Mac上面安装docker非常容易。我也去docker的官网：<a href="https://www.docker.com/">https://www.docker.com/</a>&nbsp;下载了windows的安装程序InstallDocker.msi来安装，发现不行，报错，提示让我使用docker-toolbox来安装。所以我跑到docker的官网（<a href="https://www.docker.com/products/docker-toolbox">https://www.docker.com/products/docker-toolbox</a>）下载 docker-toolbox，安装（注意选择安装git，很有用），然后会有3个应用被安装，分别是：</p> 
 <ol> 
  <li>Docker Quickstart Terminal</li> 
  <li>Kitematic (Alpha)</li> 
  <li>Oracle VM VirtualBox</li> 
  <li>Git Bash</li> 
 </ol> 
 <p>双击Docker Quickstart Terminal开始运行这个程序，他会下载Boot2Docker的应用（下载因网速不同可能不同）下来并启动docker。</p> 
 <p>其实在windows7上面运行的docker是运行在Oracle VM VirtualBox的虚拟机里面的，它会为docker分配一个IP地址，一般是：192.168.99.100 。我们要使用docker该如何做呢？</p> 
 <p>步骤一：启动Docker Quickstart Terminal，也就是启动了虚拟机和docker应用</p> 
 <p>步骤二：运行Git Bash，通过ssh链接虚拟机：$ ssh docker@192.168.99.100 密码默认是：tcuser</p> 
 <p>步骤三：验证docker。在连通虚拟机之后可以输入 $ docker --version 查看docker的版本。</p> 
 <p>&nbsp;</p> 
 <p>有用的参考资料：</p> 
 <ol> 
  <li><span style="line-height: 1.5;">用Boot2Docker来使用Docker（toolbox在Windows下安装Docker）</span></li> 
 </ol> 
 <p>地址：<a style="line-height: 1.5;" href="http://www.iganlei.cn/environment-configuration/798.html">http://www.iganlei.cn/environment-configuration/798.html</a></p> 
</div>