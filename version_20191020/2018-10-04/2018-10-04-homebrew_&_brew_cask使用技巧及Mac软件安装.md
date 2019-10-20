#homebrew & brew cask使用技巧及Mac软件安装
###发表时间：2018-10-04
###分类：mac,经验,brew
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431692" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431692</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div id="cnblogs_post_body" class="blogpost-body cnblogs-markdown" style="margin: 0px 0px 20px; padding: 0px; color: #393939; font-family: verdana, 'ms song', Arial, Helvetica, sans-serif; background-color: #faf7ef;"> 
  <h3 id="homebrew" style="margin-top: 10px; margin-bottom: 10px; font-size: 16px; line-height: 1.5;">homebrew</h3> 
  <h4 id="安装" style="margin-top: 10px; margin-bottom: 10px; font-size: 14px; color: #333333;">安装</h4> 
  <pre><code class="hljs sql" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span>/<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">master</span>/<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span>)<span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"
</span></code></pre> 
  <h4 id="命令" style="margin-top: 10px; margin-bottom: 10px; font-size: 14px; color: #333333;">命令</h4> 
  <pre><code class="hljs sql" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">安装软件：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> 软件名，例：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> wget
搜索软件：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">search</span> 软件名，例：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">search</span> wget
卸载软件：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">uninstall</span> 软件名，例：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">uninstall</span> wget
更新所有软件：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">update</span>
更新具体软件：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">upgrade</span> 软件名 ，例：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">upgrade</span> git
显示已安装软件：brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">list</span>
查看软件信息：brew info／home 软件名 ，例：brew info git ／ brew home git
显示包依赖：brew reps
显示安装的服务：brew services <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">list</span>
安装服务启动、停止、重启：brew services <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">start</span>/<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">stop</span>/restart serverName</code></pre> 
  <h3 id="homebrew-cask" style="margin-top: 10px; margin-bottom: 10px; font-size: 16px; line-height: 1.5;">homebrew cask</h3> 
  <h4 id="安装-1" style="margin-top: 10px; margin-bottom: 10px; font-size: 14px; color: #333333;">安装</h4> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew tap phinze/homebrew-cask
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> brew-cask</code></pre> 
  <h4 id="软件列表" style="margin-top: 10px; margin-bottom: 10px; font-size: 14px; color: #333333;">软件列表</h4> 
  <p style="margin: 10px auto;">可视化homebrew安装工具</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> cakebrew</code></pre> 
  <p style="margin: 10px auto;">图形化管理Homebrew安装的服务软件</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew tap jimbojsb/launchrocket
brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> launchrocket</code></pre> 
  <p style="margin: 10px auto;">全局搜索工具</p> 
  <pre><code class="hljs sql" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> alfred
//快捷键<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">option</span>+<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">space</span>
//command+回车打开文件所在文件夹
//把/usr/<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">local</span>/Caskroom增加到 alfred 的<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">search</span>目录中,偏好设置-&gt;Features-&gt;<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Default</span> Results-&gt;<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Search</span> <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Scope</span>

//百度搜索添加设置
<span class="hljs-number" style="margin: 0px; padding: 0px;">1.</span>Features-&gt;Web <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Search</span>-&gt;<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Add</span> Custom <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Search</span>
<span class="hljs-number" style="margin: 0px; padding: 0px;">2.</span><span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Search</span> <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Url</span>-&gt;https://www.baidu.com/s?wd={<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">query</span>}
Title-&gt;<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Search</span> Baidu <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">for</span> <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">'{query}'</span>
Keywords-&gt;baidu
<span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Validation</span>:alfredpp

//国人必备的<span class="hljs-number" style="margin: 0px; padding: 0px;">30</span>个Alfred Workflow
https://www.waerfa.com/alfred-workflow</code></pre> 
  <pre><code class="hljs awk" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask install google-chrome
<span class="hljs-regexp" style="margin: 0px; padding: 0px;">//</span>chrome:<span class="hljs-regexp" style="margin: 0px; padding: 0px;">//</span>components</code></pre> 
  <p style="margin: 10px auto;">终端工具</p> 
  <pre><code class="hljs awk" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask install iterm2
<span class="hljs-regexp" style="margin: 0px; padding: 0px;">//</span>配色https:<span class="hljs-regexp" style="margin: 0px; padding: 0px;">//gi</span>thub.com<span class="hljs-regexp" style="margin: 0px; padding: 0px;">/mbadolato/i</span>Term2-Color-Schemes</code></pre> 
  <p style="margin: 10px auto;">mac chm阅读工具</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> ichm</code></pre> 
  <p style="margin: 10px auto;">shadowsocks客户端</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> shadowsocksx-ng</code></pre> 
  <p style="margin: 10px auto;">redis客户端</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> rdm</code></pre> 
  <pre><code class="hljs sql" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> macvim <span class="hljs-comment" style="margin: 0px; padding: 0px; color: green;">--with-override-system-vim</span>
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> emacs <span class="hljs-comment" style="margin: 0px; padding: 0px; color: green;">--with-cocoa --with-gnutls</span>
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> adminer</code></pre> 
  <p style="margin: 10px auto;">mac环境工具</p> 
  <pre><code class="hljs sql" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> mysql
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> httpd24
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> php56 <span class="hljs-comment" style="margin: 0px; padding: 0px; color: green;">--with-httpd24</span>
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> redis
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> php56-redis
//redis可视化管理工具 redis-desktop-manager
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> php56-yaf
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> php56-swoole
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> mongodb
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> php56-mongodb
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> nginx
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> memcached
brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> php56-memcached
//mongodb可视化管理工具 robomongo</code></pre> 
  <p style="margin: 10px auto;">浏览器插件</p> 
  <pre><code class="hljs javascript" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">HTTP Status
IPvFoo
<span class="hljs-built_in" style="margin: 0px; padding: 0px; color: #0000ff;">Proxy</span> SwitchyOmega
WEB前端助手(FeHelper)
二维码生成器
译库网页翻译
购物比价助手</code></pre> 
  <p style="margin: 10px auto;">httpd22配置文件</p> 
  <pre><code class="hljs vhdl" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">&lt;IfModule alias_module&gt;
    <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Alias</span> /workspace <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/Users/redraiment/workspace/"</span>
    &lt;Directory <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/Users/redraiment/workspace/"</span>&gt;
        AllowOverride <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">All</span>
        Options Indexes MultiViews FollowSymLinks ExecCGI
        Order allow,deny
        Allow from <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">all</span>
        DirectoryIndex index.html index.php
    &lt;/Directory&gt;
&lt;/IfModule&gt;

//升级到<span class="hljs-number" style="margin: 0px; padding: 0px;">2.4</span>版本之后：Order allow,deny和Allow from <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">all</span>要改成Require <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">all</span> granted，如下所示：

&lt;IfModule alias_module&gt;
    <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">Alias</span> /workspace <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/Users/redraiment/workspace/"</span>
    &lt;Directory <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/Users/redraiment/workspace/"</span>&gt;
        AllowOverride <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">All</span>
        Options Indexes MultiViews FollowSymLinks ExecCGI
        Require <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">all</span> granted
        DirectoryIndex index.html index.php
    &lt;/Directory&gt;
&lt;/IfModule&gt;</code></pre> 
  <p style="margin: 10px auto;">虚拟目录</p> 
  <pre><code class="hljs apache" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;"><span class="hljs-section" style="margin: 0px; padding: 0px; color: #a31515;">&lt;VirtualHost *:80&gt;</span>
    <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">DocumentRoot</span> <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/www/test"</span>
    <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">ServerName</span> localhost
    <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">ErrorLog</span> <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/private/var/log/apache2/localhost-error_log"</span>
    <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">CustomLog</span> <span class="hljs-string" style="margin: 0px; padding: 0px; color: #a31515;">"/private/var/log/apache2/localhost-access_log"</span> common
    <span class="hljs-section" style="margin: 0px; padding: 0px; color: #a31515;">&lt;Directory "/www/test"&gt;</span>
        <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">Options</span> FollowSymLinks Multiviews
        <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">MultiviewsMatch</span> Any
        <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">AllowOverride</span> None
        <span class="hljs-attribute" style="margin: 0px; padding: 0px; color: #a31515;">Require</span> <span class="hljs-literal" style="margin: 0px; padding: 0px; color: #a31515;">all</span> granted
    <span class="hljs-section" style="margin: 0px; padding: 0px; color: #a31515;">&lt;/Directory&gt;</span>
<span class="hljs-section" style="margin: 0px; padding: 0px; color: #a31515;">&lt;/VirtualHost&gt;</span></code></pre> 
  <p style="margin: 10px auto;">虚拟机</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> virtualbox
brew cask <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> vagrant</code></pre> 
  <p style="margin: 10px auto;">前端工具</p> 
  <pre><code class="hljs cmake" style="margin: auto; vertical-align: middle; display: block; background: #ffffff; height: auto; padding: 5px !important; line-height: 1.5 !important; font-family: 'Courier New', sans-serif !important; font-size: 12px !important; border: 1px solid #cccccc !important; border-radius: 3px !important;">brew <span class="hljs-keyword" style="margin: 0px; padding: 0px; color: #0000ff;">install</span> node</code></pre> 
 </div> 
 <div id="blog_post_info_block" style="margin: 20px 0px 0px; padding: 0px; color: #393939; font-family: verdana, 'ms song', Arial, Helvetica, sans-serif; background-color: #faf7ef;">
  &nbsp;
 </div> 
 <div class="clear" style="">
  &nbsp;
 </div> 
 <div class="clear" style="">
  引用地址：&nbsp;
  <a href="https://www.cnblogs.com/51fx/p/7004429.html">https://www.cnblogs.com/51fx/p/7004429.html</a> 
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>