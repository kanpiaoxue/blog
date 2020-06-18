#birt session 过期问题，跨域问题
###发表时间：2011-11-14
###分类：birt
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1258590" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1258590</a>

---

<p>The viewing session is not available or has expired</p>
<p>&nbsp;</p>
<p>最近研究birt的使用，发现birt不支持集群。</p>
<p>所以我就另外搭建了一个tomcat，做专门的birt报表服务器。那么我就需要把它继承在现有的web程序中。用的是iframe。</p>
<p>发现，还是有问题，总是报错“The viewing session is not available or has expired”。</p>
<p>搞了半天，查了半天的资料。发现没有好的办法。老外也遇到这个问题，也在惆怅。</p>
<p>我试了IE的设置，找到一个勉强可以接受的方法来解决。</p>
<p>方法如下：</p>
<p>IE - Intetnet 选项 - 隐私 - 设置：这里有个拉动条，可以设置IE的cookie。将它调到“低”或者“最低”，可以达到解决问题的目的。</p>
<p>不过，这个方法我认为不好。你不能让每个用你的birt程序的人都去修改IE浏览器吧？！所以，也希望看见blog的朋友要是解决过这类的问题，说一下你们解决的方法。还有，谁尝试过birt的集群，也希望能给我一些帮助。谢谢</p>
<p>&nbsp;</p>
<p>------------------------------------ 2012-01-10 [解决如下] -------------</p>
<p>birt the viewing session is not avaliable or has expired</p>
<p>问题描述：</p>
<p>http://11.23.26.3:8084/biReport/frameset?__report=VIP_kefu.rptdesign&amp;__masterpage=true&amp;__format=html&amp;__parameterpage=true&amp;__toolbar=true&amp;__showtitle=false</p>
<p>我采用上面的url，在一个项目中访问另一个项目biReport中的birt报表，发生错误：</p>
<p> </p>
<p>birt the viewing session is not avaliable or has expired</p>
<p>&nbsp;</p>
<p>我在google的很多地方，都没有找到解决的方案。最终，在&nbsp;<a href="http://www.birt-exchange.org/org/forum/index.php/topic/17735-the-viewing-session-is-not-available-or-has-expired-again/page__s__e25ec58943536503b7b10f91ccd1e87e">http://www.birt-exchange.org/org/forum/index.php/topic/17735-the-viewing-session-is-not-available-or-has-expired-again/page__s__e25ec58943536503b7b10f91ccd1e87e</a>&nbsp;里面找到一个方案，解决了这个问题。原文描述如下：</p>
<p> </p>
<p class="posted_info" style="">Posted&nbsp;<abbr class="published" style="" title="2010-12-23T14:25:27+00:00">23 December 2010 - 06:25 AM</abbr></p>
<div class="post entry-content " style="margin-top: 3px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; background-color: #fafbfc; line-height: 19px; color: #1c2837; font-family: arial, verdana, tahoma, sans-serif; font-size: 13px; padding: 10px;">
 Hello,
 <br>
 <br>Today I encountered the same "The viewing session is not available or has expired." message again. Some months ago I managed to find a solution (see this&nbsp;
 <a class="bbc_url" style="color: #284b72; text-decoration: none;" title="External link" rel="nofollow" href="http://www.birt-exchange.org/org/forum/index.php/topic/15211-the-viewing-session-not-available/page__view__findpost__p__60445">post</a>).&nbsp;
 <br>
 <br>This time the issue was a bit different: it only happened when the reports were accessed from IE, but not from Firefox and only for some of them. Looking at the differences I saw that for some of the reports the URL included the hostname and for the others the IP address of the Tomcat server. The ones that were failing to be displayed were the ones accessed by IP.&nbsp;
 <br>
 <br>So you could check how you are accessing the reports and how the URL is specified. In my case using the hostname of the machine hosting the Tomcat did the trick.
 <br>
 <br>Regards,
 <br>Mudor&nbsp;
</div>
<div class="post entry-content " style="margin-top: 3px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; background-color: #fafbfc; line-height: 19px; color: #1c2837; font-family: arial, verdana, tahoma, sans-serif; font-size: 13px; padding: 10px;">
 所以，我修改了原有的IP地址访问，把IP地址修改为了hostname，就可以正常访问，不在报session过期的错误。
</div>
<div class="post entry-content " style="margin-top: 3px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; background-color: #fafbfc; line-height: 19px; color: #1c2837; font-family: arial, verdana, tahoma, sans-serif; font-size: 13px; padding: 10px;">
 如下：
</div>
<div class="post entry-content " style="margin-top: 3px; margin-right: 0px; margin-bottom: 0px; margin-left: 0px; background-color: #fafbfc; padding: 10px;">
 <span style="font-family: arial, verdana, tahoma, sans-serif; color: #1c2837; font-size: x-small;"><span style="line-height: 19px;">http://bi2.query.com:8084/biReport/frameset?__report=VIP_kefu.rptdesign&amp;__masterpage=true&amp;__format=html&amp;__parameterpage=true&amp;__toolbar=true&amp;__showtitle=false</span></span>
</div>
<p>&nbsp;</p>
<p>呵呵，困扰了很久的问题，终于得到解决。爽啊！（备注：这个问题已经被官网列为ＢＵＧ，但是一直没有修复，很奇怪。必须用域名，而不能用ＩＰ）</p>
<p>&nbsp;</p>
<p>&nbsp;</p>