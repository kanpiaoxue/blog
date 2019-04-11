#springboot常用application.yml
###发表时间：2018-09-20
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2431035" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2431035</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>application.yml</p> 
 <pre name="code" class="java">spring:
  profiles:
    active:
    - dev
  main:
    banner-mode: log
  boot:
    admin:
      client:
        instance:
          prefer-ip: true
  mvc:
    view:
      prefix: /pages/
      suffix: .html

management:
  endpoints:
    web:
      exposure:
        include: "*"
  endpoint:
    health:
      show-details: always
    jolokia:
      enabled: true
    shutdown:
      enabled: true
         
info:
  app:
    cnName: 测试系统
    enName: test-system


mybatis:
  mapper-locations:
  - mapper/*DAO.xml 
  type-aliases-package: org.kanpiaoxue.dao.*

</pre> 
 <pre name="code" class="java"># logging start

logging:

  pattern:

    console: "%clr(%d{yyyy-MM-dd HH:mm:ss.SSS}){faint} %clr(${LOG_LEVEL_PATTERN:-%5p}) %clr(${PID:- }){magenta} %clr(---){faint} %clr([%t]){faint} %clr(%-40.40logger{39}){cyan}[lineno:%line]    %clr(:){faint} %m%n${LOG_EXCEPTION_CONVERSION_WORD:%wEx}"

    file: "%d{yyyy-MM-dd HH:mm:ss.SSS} ${LOG_LEVEL_PATTERN:-%5p} ${PID:- } --- [%t] %-40.40logger{39}[lineno:%line]: %m%n${LOG_EXCEPTION_CONVERSION_WORD:%wEx}"</pre> 
 <p class="p1" style="font-family: Helvetica, Tahoma, Arial, sans-serif; white-space: normal; background-color: #ffffff;">&nbsp;</p> 
 <p class="p1">&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  application-dev.yml 写
 </div> 
 <div class="quote_title"> 
  <pre name="code" class="java">spring:
  application:
    name: hello-开发环境
  boot:
    admin:
      client:
        url: "http://localhost:9080"
# database start
  datasource:
    url: "jdbc:mysql://127.0.0.1:3306/hello"
    username: "root"
    password: "root"

server:
  port: 8081

# logging start
logging.file: "${HOME}/logs/hello/hello.log"
logging:
  file:
    max-size: 1MB
    max-history: 20
  level:
    root: INFO
    org.springframework: INFO
    org.kanpiaoxue.hello: DEBUG</pre> &nbsp;
 </div> 
 <p>&nbsp;</p> 
</div>