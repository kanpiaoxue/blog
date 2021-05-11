#Tomcat JVM 启动参数配置
###发表时间：2011-07-11
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1121530" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1121530</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>自己配置了一个nginx + tomcat (1 * 3) + memcached 的J2EE集群。</p> 
 <p>发现tomcat经常发现堆栈溢出，尤其是 Pern Gen。</p> 
 <p>看了网上不少资料，发现没一个能用的。所以根据自己配置 java [-jvm args] -jar test.jar ，配置了tomcat的JVM启动参数，解决了堆栈溢出的问题。</p> 
 <p>步骤如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/*------------- linux start ----------------*/
$cd /usr/local/apache-tomcat-6.0.18/bin //进入你tomcat的bin目录
$vim catalina.sh //编辑你的 catalina.sh 文件
找到里面的 

# Set juli LogManager if it is present
if [ -r "$CATALINA_BASE"/conf/logging.properties ]; then
  JAVA_OPTS="$JAVA_OPTS -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager"
  LOGGING_CONFIG="-Djava.util.logging.config.file=$CATALINA_BASE/conf/logging.properties"
fi

把 JAVA_OPTS="$JAVA_OPTS -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager"
修改为 JAVA_OPTS="$JAVA_OPTS -Xms5120m -Xmx5120m -Xmn2048m -XX:PermSize=512m -XX:MaxPermSize=512m -XX:+UseConcMarkSweepGC -XX:+UseCMSCompactAtFullCollection -XX:CMSMaxAbortablePrecleanTime=500 -XX:+CMSClassUnloadingEnabled -XX:+CMSClassUnloadingEnabled -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager"

/*------------- linux end ----------------*/
</pre> 
 <p>&nbsp;</p> 
 <p>因为我用的Linux服务器是32G内存，所以我对JVM的参数设置的比较大。在JVM堆栈后面的参数，是对JVM垃圾回收器优化的参数。</p> 
 <p>&nbsp;</p> 
 <p>如果大家依然发现堆栈溢出，请检查你的代码。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>---------&nbsp;</p> 
 <h3 style="font-size: 16px; padding-top: 10px;"><a style="color: #108ac6; text-decoration: underline;" href="http://zxmsdyz.iteye.com/blog/1768567">tomcat7 内存配置修改方法</a></h3> 
 <p><a href="http://zxmsdyz.iteye.com/blog/1768567">http://zxmsdyz.iteye.com/blog/1768567</a></p> 
</div>