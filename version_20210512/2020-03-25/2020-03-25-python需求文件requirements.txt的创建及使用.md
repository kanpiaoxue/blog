#python需求文件requirements.txt的创建及使用
###发表时间：2020-03-25
###分类：python,shell,经验,pip
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2513214" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2513214</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>迁移python环境是很麻烦的事情，需要精准的安装一堆的pip的package。有个简易的办法，使用需求文件requirements.txt来简化这个过程。</p> 
 <p>&nbsp;</p> 
 <p>源头机器上面，生成需求文件：</p> 
 <p><span class="hljs-variable" style="margin: 0px; padding: 0px; font-family: 'Microsoft YaHei', 'SF Pro Display', Roboto, Noto, Arial, 'PingFang SC', sans-serif; color: #4f4f4f; white-space: pre;">$ </span><span style="color: #4f4f4f; font-family: 'Source Code Pro', 'DejaVu Sans Mono', 'Ubuntu Mono', 'Anonymous Pro', 'Droid Sans Mono', Menlo, Monaco, Consolas, Inconsolata, Courier, monospace, 'PingFang SC', 'Microsoft YaHei', sans-serif; white-space: pre; background-color: #f6f8fa;">pip freeze &gt;requirements.txt</span></p> 
 <p><span style="color: #4f4f4f; font-family: 'Source Code Pro', 'DejaVu Sans Mono', 'Ubuntu Mono', 'Anonymous Pro', 'Droid Sans Mono', Menlo, Monaco, Consolas, Inconsolata, Courier, monospace, 'PingFang SC', 'Microsoft YaHei', sans-serif; white-space: pre; background-color: #f6f8fa;">目标机器，安装需求文件：</span></p> 
 <p><span class="hljs-variable" style="margin: 0px; padding: 0px; font-family: 'Microsoft YaHei', 'SF Pro Display', Roboto, Noto, Arial, 'PingFang SC', sans-serif; color: #4f4f4f; white-space: pre;">$ </span><span style="color: #4f4f4f; font-family: 'Source Code Pro', 'DejaVu Sans Mono', 'Ubuntu Mono', 'Anonymous Pro', 'Droid Sans Mono', Menlo, Monaco, Consolas, Inconsolata, Courier, monospace, 'PingFang SC', 'Microsoft YaHei', sans-serif; white-space: pre; background-color: #f6f8fa;">pip install -r requirements.txt</span></p> 
 <p>&nbsp;</p> 
 <p>参考资料：<a href="https://blog.csdn.net/loyachen/article/details/52028825">https://blog.csdn.net/loyachen/article/details/52028825</a></p> 
</div>