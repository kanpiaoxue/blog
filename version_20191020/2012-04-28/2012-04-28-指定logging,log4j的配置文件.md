#指定logging,log4j的配置文件
###发表时间：2012-04-28
###分类：java,log4j
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1503744" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1503744</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>工作开发中，时长会用到可运行的jar包。记录程序的运行情况，就是通过java.util.logging来实现log，或者通过log4j.jar来实现log。这样会有一个问题，log4j.properties或者log4j.xml会被包含到jar里面，如果要修改这个文件，就需要重新打成jar包。解决这个问题的还有一个办法，把log4j.xml从jar挪出来，放到和jar一个目录中（log4j会搜索classpath），就可以修改这个配置文件了。但是，这样还是不够友好。所以提供下面2种方法解决：</p> 
 <p>1、针对java.util.logging</p> 
 <p>运行如下：</p> 
 <p>java -D<span style="color: #ff0000;">java.util.logging.config.file=</span>c:/log.properties -jar hello.jar</p> 
 <p>参考：&nbsp;<a href="http://docs.oracle.com/javase/1.4.2/docs/api/java/util/logging/LogManager.html">http://docs.oracle.com/javase/1.4.2/docs/api/java/util/logging/LogManager.html</a></p> 
 <p>2、针对log4j</p> 
 <p>运行如下：</p> 
 <p>java&nbsp;<span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; line-height: 18px; text-align: left; background-color: #fafafa;">-D<span style="color: #ff0000;">log4j.configuration=file:</span>c:/log4j.xml -jar hello.jar</span></p> 
 <p>&nbsp;</p> 
</div>