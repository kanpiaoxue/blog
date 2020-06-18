#指定logging、log4j、log4j2的配置文件
###发表时间：2012-04-28
###分类：java,log4j
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1503744" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1503744</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">工作开发中，时长会用到可运行的jar包。记录程序的运行情况，就是通过java.util.logging来实现log，或者通过log4j.jar来实现log。这样会有一个问题，log4j.properties或者log4j.xml会被包含到jar里面，如果要修改这个文件，就需要重新打成jar包。解决这个问题的还有一个办法，把log4j.xml从jar挪出来，放到和jar一个目录中（log4j会搜索classpath），就可以修改这个配置文件了。但是，这样还是不够友好。所以提供下面2种方法解决：</p> 
 <p style="font-size: 14px;">1、针对java.util.logging</p> 
 <p style="font-size: 14px;">运行如下：</p> 
 <p style="font-size: 14px;">java -D<span style="color: #ff0000;">java.util.logging.config.file=</span>c:/log.properties -jar hello.jar</p> 
 <p style="font-size: 14px;">参考：&nbsp;<a href="http://docs.oracle.com/javase/1.4.2/docs/api/java/util/logging/LogManager.html">http://docs.oracle.com/javase/1.4.2/docs/api/java/util/logging/LogManager.html</a></p> 
 <p style="font-size: 14px;">2、针对log4j</p> 
 <p style="font-size: 14px;">运行如下：</p> 
 <p style="font-size: 14px;">java&nbsp;<span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; line-height: 18px; text-align: left; background-color: #fafafa;">-D<span style="color: #ff0000;">log4j.configuration=file:</span>c:/log4j.xml -jar hello.jar</span></p> 
 <p style="font-size: 14px;"><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; line-height: 18px; text-align: left; background-color: #fafafa;">3、</span>针对log4j2</p> 
 <p>运行如下：</p> 
 <p><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; line-height: 18px; text-align: left; background-color: #fafafa;"><span style="background-color: white;">java&nbsp;</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace;">-Dlog4j.configurationFile=/tmp/log4j2.console.xml&nbsp;</span></span><span style="background-color: #fafafa; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace;">-jar hello.jar</span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>