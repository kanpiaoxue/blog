#springboot的Hikari的数据源报错Failed to validate connection
###发表时间：2020-01-19
###分类：Spring,java,DataSource,jdbc,springboot,hikari
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2512141" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2512141</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>使用springboot的默认数据源&nbsp;Hikari 的DataSource的时候，日志里面时常出现以下的异常日志：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">HikariPool-1 - Failed to validate connection com.mysql.jdbc.JDBC4Connection@16521373 (No operations allowed after connection closed</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>修改springboot的数据源配置如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">spring: 
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://127.0.0.1:3306/xxxx
    username: root
    password: xxxxx
    hikari:    
      #timeout 5 minutes: 5 * 60 seconds. Here unit is ms.
      max-lifetime: 300000</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>新增如下的配置</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    hikari:    
      #timeout 5 minutes: 5 * 60 seconds. Here unit is ms.
      max-lifetime: 300000</pre> 
 <p>&nbsp;问题解决。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>观察springboot的启动日志可以发现如下的区别：</p> 
 <p>未添加spring.hikari.max-lifetime: 300000 之前启动日志：</p> 
 <pre name="code" class="java">FrameworkServlet 'dispatcherServlet': initialization started
FrameworkServlet 'dispatcherServlet': initialization completed in 35 ms
HikariPool-1 - Starting...
HikariPool-1 - Start completed.</pre> 
 <p>&nbsp;添加spring.hikari.max-lifetime: 300000 之后启动日志：</p> 
 <pre name="code" class="java">FrameworkServlet 'dispatcherServlet': initialization started
FrameworkServlet 'dispatcherServlet': initialization completed in 44 ms
HikariPool-1 - idleTimeout is close to or more than maxLifetime, disabling it.
HikariPool-1 - Starting...
HikariPool-1 - Start completed.</pre> 
 <p>&nbsp;发现多了一行：</p> 
 <pre name="code" class="java">HikariPool-1 - idleTimeout is close to or more than maxLifetime, disabling it.</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考地址：</p> 
 <p><a href="https://www.cnblogs.com/l-tianyi/p/8143103.html">https://www.cnblogs.com/l-tianyi/p/8143103.html</a></p> 
</div>