#Linux挂载DVD/CD
###发表时间：2013-12-30
###分类：Linux
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1997434" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1997434</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">先确保你的机器（或虚拟机）有光驱，并将光盘放入其中。

[root@localhost cdrom]# cd /dev/
[root@localhost dev]# ll |grep dvd
lrwxrwxrwx. 1 root root           3 Dec 30 01:36 dvd -&gt; sr0
lrwxrwxrwx. 1 root root           3 Dec 30 01:19 dvd1 -&gt; sr1
lrwxrwxrwx. 1 root root           3 Dec 30 01:36 dvdrw -&gt; sr0
lrwxrwxrwx. 1 root root           3 Dec 30 01:19 dvdrw1 -&gt; sr1

[root@localhost dev]# mkdir /mnt/cdrom
[root@localhost dev]# mount dvd /mnt/cdrom 
[root@localhost dev]# cd /mnt/cdrom
[root@localhost cdrom]# ll</pre> 
 <p>&nbsp;</p> 
</div>