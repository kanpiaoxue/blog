#spring-boot的日志添加行号
###发表时间：2018-09-20
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431021" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431021</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">spring-boot-2.0.5.RELEASE的日志默认是不带行号的，对于开发人员来说比较鸡肋。开发人员更喜欢日志中带有代码的行号，方便定位问题。</p> 
 <p style="font-size: 14px;">所以我们来修改一下spring-boot-2.0.5.RELEASE的logback的默认配置。</p> 
 <p style="font-size: 14px;">找到他的默认配置文件，如下：</p> 
 <div class="quote_title" style="font-size: 14px;">
  spring-boot-2.0.5.RELEASE的默认logback的配置文件：需要使用 vim直接查看
 </div> 
 <div class="quote_div" style="font-size: 14px;">
  /org/springframework/boot/spring-boot/2.0.5.RELEASE/spring-boot-2.0.5.RELEASE.jar::org/springframework/boot/logging/logback/defaults.xml
 </div> 
 <p style="font-size: 14px;">&nbsp;文件内容：</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;!--
Default logback configuration provided for import, equivalent to the programmatic
initialization performed by Boot
--&gt;

&lt;included&gt;
    &lt;conversionRule conversionWord="clr" converterClass="org.springframework.boot.logging.logback.ColorConverter" /&gt;
    &lt;conversionRule conversionWord="wex" converterClass="org.springframework.boot.logging.logback.WhitespaceThrowableProxyConverter" /&gt;
    &lt;conversionRule conversionWord="wEx" converterClass="org.springframework.boot.logging.logback.ExtendedWhitespaceThrowableProxyConverter" /&gt;
    &lt;property name="CONSOLE_LOG_PATTERN" value="${CONSOLE_LOG_PATTERN:-%clr(%d{${LOG_DATEFORMAT_PATTERN:-yyyy-MM-dd HH:mm:ss.SSS}}){faint} %clr(${LOG_LEVEL_PATTERN:-%5p}) %clr(${PID:- }){magenta} %clr(---){faint} %clr([%15.15t]){faint} %clr(%-40.40logger{39}){cyan} %clr(:){faint} %m%n${LOG_EXCEPTION_CONVERSION_WORD:-%wEx}}"/&gt;
    &lt;property name="FILE_LOG_PATTERN" value="${FILE_LOG_PATTERN:-%d{${LOG_DATEFORMAT_PATTERN:-yyyy-MM-dd HH:mm:ss.SSS}} ${LOG_LEVEL_PATTERN:-%5p} ${PID:- } --- [%t] %-40.40logger{39} : %m%n${LOG_EXCEPTION_CONVERSION_WORD:-%wEx}}"/&gt;

    &lt;logger name="org.apache.catalina.startup.DigesterFactory" level="ERROR"/&gt;
    &lt;logger name="org.apache.catalina.util.LifecycleBase" level="ERROR"/&gt;
    &lt;logger name="org.apache.coyote.http11.Http11NioProtocol" level="WARN"/&gt;
    &lt;logger name="org.apache.sshd.common.util.SecurityUtils" level="WARN"/&gt;
    &lt;logger name="org.apache.tomcat.util.net.NioSelectorPool" level="WARN"/&gt;
    &lt;logger name="org.eclipse.jetty.util.component.AbstractLifeCycle" level="ERROR"/&gt;
    &lt;logger name="org.hibernate.validator.internal.util.Version" level="WARN"/&gt;
&lt;/included&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;查看 logback 的文档可知它打印日志的时候pattern中的变量 %line 表示行号。我们配置application.yum文件。</p> 
 <pre name="code" class="java"># logging start
logging.file: "logs/hello.log"
logging:
  file:
    max-size: 10MB
    max-history: 20    
  level:
    root: INFO
    org.springframework: ERROR
  pattern:
    console: "%clr(%d{yyyy-MM-dd HH:mm:ss.SSS}){faint} %clr(${LOG_LEVEL_PATTERN:-%5p}) %clr(${PID:- }){magenta} %clr(---){faint} %clr([%t]){faint} %clr(%-40.40logger{39}){cyan}[lineno:%line]    %clr(:){faint} %m%n${LOG_EXCEPTION_CONVERSION_WORD:%wEx}"
    file: "%d{yyyy-MM-dd HH:mm:ss.SSS} ${LOG_LEVEL_PATTERN:-%5p} ${PID:- } --- [%t] %-40.40logger{39}[lineno:%line]: %m%n${LOG_EXCEPTION_CONVERSION_WORD:%wEx}"</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; background-color: #ffffff; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline; color: #000000;"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline;">仔细观察上面的配置可以看见里面比spring-boot自己的日志文件多了 %line 的内容，这就是行号。</span></span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; background-color: #ffffff; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline; color: #000000;"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline;">参考：</span></span></a></p> 
 <p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; background-color: #ffffff; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline; color: #000000;"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline;">https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html</span></span></a></p> 
 <p><a href="https://stackoverflow.com/questions/23123934/logback-show-logs-with-line-number"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; background-color: #ffffff; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline; color: #000000;"><span class="pln" style="font-family: inherit; font-size: 14px; font-style: inherit; font-variant: inherit; white-space: inherit; margin: 0px; padding: 0px; border: 0px; line-height: inherit; vertical-align: baseline;">https://stackoverflow.com/questions/23123934/logback-show-logs-with-line-number</span></span></a></p> 
</div>