#如何解决类似 curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connec
###发表时间：2021-01-15
###分类：brew,mac,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2518738" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2518738</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料：<a href="https://github.com/hawtim/blog/issues/10">https://github.com/hawtim/blog/issues/10</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>今天发现安装 homeBrew 发现报错如下：</p> 
 <p>curl: (7) Failed to connect to raw.githubusercontent.com port 443: Connection refused</p> 
 <p>Failed to fetch Homebrew .gitignore!</p> 
 <p>&nbsp;</p> 
 <p style="">网上搜索了一下，发现是 github 的一些域名的 DNS 解析被污染，导致DNS 解析过程无法通过域名取得正确的IP地址。</p> 
 <p style=""><a style="" href="https://zhuanlan.zhihu.com/p/101908711" rel="nofollow">打开<span>&nbsp;</span></a><a style="" href="https://www.ipaddress.com/" rel="nofollow">https://www.ipaddress.com/</a><span>&nbsp;</span><span>输入访问不了的域名，得到IP地址，然后改一下本地host，把无法访问的域名代理一下，就可以了。</span></p> 
 <p style="">&nbsp;</p> 
</div>