#按照brew失败：Failed to connect to raw.githubusercontent.com port 44
###发表时间：2021-01-14
###分类：brew,mac,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2518700" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2518700</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料：<a href="https://stackoverflow.com/questions/29910217/homebrew-installation-on-mac-os-x-failed-to-connect-to-raw-githubusercontent-com">https://stackoverflow.com/questions/29910217/homebrew-installation-on-mac-os-x-failed-to-connect-to-raw-githubusercontent-com</a></p> 
 <p>&nbsp;</p> 
 <p style="">The accepted Answer is outdated now. But based on the answer I solved the problem by:</p> 
 <ol style="margin-bottom: 0px; margin-left: 30px; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; color: #242729;"> 
  <li style="">open the home page of brew&nbsp;<a style="" href="https://brew.sh/" rel="nofollow noreferrer">https://brew.sh/</a> </li> 
  <li style="">copy the URL from the install cmd and open it on your browser&nbsp;<a style="" href="https://raw.githubusercontent.com/Homebrew/install/master/install.sh" rel="nofollow noreferrer">https://raw.githubusercontent.com/Homebrew/install/master/install.sh</a> </li> 
  <li style="">right-click and save it to your computer</li> 
  <li style="margin-bottom: 0px; margin-left: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: inherit; font-size: 15px; vertical-align: baseline;">open a terminal and run it with: /bin/bash path-to/install.sh</li> 
 </ol> 
 <p>&nbsp;</p> 
</div>