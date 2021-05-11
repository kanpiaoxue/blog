#Missing library: xdoclet-1.2.1.jar. Select the home directory for XDoclet. 1.2.1
###发表时间：2018-02-28
###分类：eclipse,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2411821" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2411821</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p><span style="font-size: 14px;">eclipse开发web项目的失败，总是发现Project的文件夹上面有错误。</span></p> 
 <p><span style="font-size: 14px;">点开项目的Properties之后发现里面的XDocklet报错如下:</span></p> 
 <div class="quote_div">
  <span style="font-size: 14px;">Missing library: xdoclet-1.2.1.jar. Select the home directory for XDoclet. 1.2.1</span>
 </div> 
 <p><span style="font-size: 14px;">&nbsp;在网上找到的解决办法：</span></p> 
 <p><span style="font-size: 14px;"><a href="http://blog.csdn.net/uestcong/article/details/7162095">http://blog.csdn.net/uestcong/article/details/7162095</a></span></p> 
 <p><span style="font-size: 14px;">具体方法如下：</span></p> 
 <p><span style="font-size: 14px;"><span style="margin: 0px; padding: 0px; color: #4f4f4f; font-family: 'PingFang SC', 'Microsoft YaHei', SimHei, Arial, SimSun; text-align: justify; white-space: pre;">Go to http://sourceforge.net/projects/xdoclet/files/xdoclet/1.2.1/ </span><span style="color: #4f4f4f; font-family: 'PingFang SC', 'Microsoft YaHei', SimHei, Arial, SimSun; text-align: justify;">&nbsp;</span><span style="margin: 0px; padding: 0px; color: #4f4f4f; font-family: 'PingFang SC', 'Microsoft YaHei', SimHei, Arial, SimSun; text-align: justify; white-space: pre;">and download the zip <span style="white-space: normal;">xdoclet-bin-1.2.1.zip</span>. Unzip it somewhere on your pc and in eclipse point the XDoclet。</span></span></p> 
 <p><span style="margin: 0px; padding: 0px; color: #4f4f4f; font-family: 'PingFang SC', 'Microsoft YaHei', SimHei, Arial, SimSun; text-align: justify; white-space: pre;"><span style="color: #4f4f4f; font-family: 'PingFang SC', 'Microsoft YaHei', SimHei, Arial, SimSun;">把XDoclet Home设置为C:\openxds\xdoclet-1.2.1\lib，就成功啦！</span></span></p> 
</div>