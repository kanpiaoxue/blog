#springboot项目maven多module
###发表时间：2018-11-29
###分类：Spring,springboot,java,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434522" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434522</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">在创建springboot项目的时候，我们希望一个主题的多个子模块可以共享彼此的逻辑。springboot强调为服务，各自为战。但是我还是希望可以将同一个主题的多个springboot程序放在一起，它们可以共享通用的javabean、DAO和业务逻辑代码。</p> 
 <p style="font-size: 14px;">下面是helloWorld的项目结构：</p> 
 <pre name="code" class="java">helloWorld
├── helloWorld-commons //通用的javabean和工具类
│&nbsp;&nbsp; ├── pom.xml
│&nbsp;&nbsp; ├── src
│&nbsp;&nbsp; └── target
├── helloWorld-dao // jdbc的 DAO
│&nbsp;&nbsp; ├── pom.xml
│&nbsp;&nbsp; ├── src
│&nbsp;&nbsp; └── target
├── helloWorld-service // 业务逻辑服务类
│&nbsp;&nbsp; ├── pom.xml
│&nbsp;&nbsp; ├── src
│&nbsp;&nbsp; └── target
├── helloWorld-web // web程序
│&nbsp;&nbsp; ├── pom.xml
│&nbsp;&nbsp; ├── src
│&nbsp;&nbsp; └── target
└── pom.xml
</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">下面是根pom.xml</p> 
 <pre name="code" class="java">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
    &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
    &lt;artifactId&gt;helloWorld&lt;/artifactId&gt;
    &lt;version&gt;0.0.1&lt;/version&gt;
    &lt;packaging&gt;pom&lt;/packaging&gt;

    &lt;parent&gt;
        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
        &lt;artifactId&gt;spring-boot-starter-parent&lt;/artifactId&gt;
        &lt;version&gt;2.0.6.RELEASE&lt;/version&gt;
        &lt;relativePath /&gt; &lt;!-- lookup parent from repository --&gt;
    &lt;/parent&gt;
    &lt;modules&gt;
        &lt;module&gt;helloWorld-commons&lt;/module&gt;
        &lt;module&gt;helloWorld-dao&lt;/module&gt;
        &lt;module&gt;helloWorld-service&lt;/module&gt;
        &lt;module&gt;helloWorld-web&lt;/module&gt;
    &lt;/modules&gt;

    &lt;properties&gt;
            &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
            &lt;java.source.version&gt;1.8&lt;/java.source.version&gt;
            &lt;java.target.version&gt;1.8&lt;/java.target.version&gt;
    &lt;/properties&gt;

    &lt;dependencyManagement&gt;
            &lt;dependencies&gt;
                    &lt;!-- 这里配置各个模块需要的通用依赖，但是不配置 springboot 的各个依赖。 springboot的各个依赖配置在各个module中 --&gt;
                    ...
            &lt;/dependencies&gt;
    &lt;/dependencyManagement&gt;

    &lt;build&gt;
        &lt;pluginManagement&gt;
            &lt;plugins&gt;
                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
                    &lt;version&gt;3.3&lt;/version&gt;
                    &lt;configuration&gt;
                        &lt;source&gt;${java.source.version}&lt;/source&gt;
                        &lt;target&gt;${java.target.version}&lt;/target&gt;
                        &lt;encoding&gt;utf8&lt;/encoding&gt;
                    &lt;/configuration&gt;
                &lt;/plugin&gt;
                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-resources-plugin&lt;/artifactId&gt;
                    &lt;version&gt;2.4.3&lt;/version&gt;
                    &lt;configuration&gt;
                        &lt;encoding&gt;UTF-8&lt;/encoding&gt;
                    &lt;/configuration&gt;
                &lt;/plugin&gt;
                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-assembly-plugin&lt;/artifactId&gt;
                    &lt;version&gt;3.1.0&lt;/version&gt;
                    &lt;configuration&gt;
                        &lt;encoding&gt;UTF-8&lt;/encoding&gt;
                    &lt;/configuration&gt;
                &lt;/plugin&gt;
                &lt;plugin&gt;
                    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
                    &lt;artifactId&gt;maven-surefire-plugin&lt;/artifactId&gt;
                    &lt;version&gt;2.20.1&lt;/version&gt;
                    &lt;configuration&gt;
                        &lt;skipTests&gt;false&lt;/skipTests&gt;
                    &lt;/configuration&gt;
                &lt;/plugin&gt;
            &lt;/plugins&gt;
        &lt;/pluginManagement&gt;
    &lt;/build&gt;

&lt;/project&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">helloWorld-commons 模块的pom.xml: 注意它使用到了log日志，注意它是如何在pom里面引用log的。</p> 
 <pre name="code" class="java">&lt;?xml version="1.0"?&gt;
&lt;project
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
    &lt;parent&gt;
        &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
        &lt;artifactId&gt;helloWorld&lt;/artifactId&gt;
        &lt;version&gt;0.0.1&lt;/version&gt;
    &lt;/parent&gt;
    &lt;artifactId&gt;helloWorld-commons&lt;/artifactId&gt;
    &lt;name&gt;helloWorld-commons&lt;/name&gt;
    &lt;url&gt;http://maven.apache.org&lt;/url&gt;
    &lt;properties&gt;
        &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
    &lt;/properties&gt;
    &lt;dependencies&gt;



        &lt;!-- log start --&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-logging&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;!-- log end --&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
            &lt;artifactId&gt;guava&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;com.google.code.gson&lt;/groupId&gt;
            &lt;artifactId&gt;gson&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;!-- start apache --&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;commons-collections&lt;/groupId&gt;
            &lt;artifactId&gt;commons-collections&lt;/artifactId&gt;
        &lt;/dependency&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
            &lt;artifactId&gt;commons-lang3&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;commons-io&lt;/groupId&gt;
            &lt;artifactId&gt;commons-io&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;!-- end apache --&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;joda-time&lt;/groupId&gt;
            &lt;artifactId&gt;joda-time&lt;/artifactId&gt;
        &lt;/dependency&gt;


        &lt;!-- test start --&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;junit&lt;/groupId&gt;
            &lt;artifactId&gt;junit&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-module-junit4-rule-agent&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock.tests&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-tests-utils&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-core&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-module-junit4&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.mockito&lt;/groupId&gt;
            &lt;artifactId&gt;mockito-all&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-api-mockito&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-classloading-xstream&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;!-- test end --&gt;

    &lt;/dependencies&gt;
&lt;/project&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">其他模块的pom.xml 就不一一罗列了，这里最关键是helloWorld-web的pom.xml 因为只有它才是真正的springboot的可执行程序。它的pom.xml如下：</p> 
 <pre name="code" class="java">&lt;?xml version="1.0"?&gt;
&lt;project
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"
    xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
    &lt;parent&gt;
        &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
        &lt;artifactId&gt;hello&lt;/artifactId&gt;
        &lt;version&gt;0.0.1&lt;/version&gt;
    &lt;/parent&gt;

    &lt;artifactId&gt;hello-web&lt;/artifactId&gt;
    &lt;name&gt;hello-web&lt;/name&gt;
    &lt;packaging&gt;jar&lt;/packaging&gt;
    &lt;url&gt;http://maven.apache.org&lt;/url&gt;

    &lt;properties&gt;
        &lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
        &lt;helloWorld.version&gt;0.0.1&lt;/helloWorld.version&gt;
    &lt;/properties&gt;
    &lt;dependencies&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
            &lt;artifactId&gt;helloWorld-commons&lt;/artifactId&gt;
            &lt;version&gt;${helloWorld.version}&lt;/version&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
            &lt;artifactId&gt;helloWorld-dao&lt;/artifactId&gt;
            &lt;version&gt;${helloWorld.version}&lt;/version&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
            &lt;artifactId&gt;helloWorld-service&lt;/artifactId&gt;
            &lt;version&gt;${helloWorld.version}&lt;/version&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;org.quartz-scheduler&lt;/groupId&gt;
            &lt;artifactId&gt;quartz&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.apache.poi&lt;/groupId&gt;
            &lt;artifactId&gt;poi&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;org.apache.poi&lt;/groupId&gt;
            &lt;artifactId&gt;poi-ooxml&lt;/artifactId&gt;
        &lt;/dependency&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
            &lt;artifactId&gt;guava&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;com.google.code.gson&lt;/groupId&gt;
            &lt;artifactId&gt;gson&lt;/artifactId&gt;
        &lt;/dependency&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;net.sf.ehcache&lt;/groupId&gt;
            &lt;artifactId&gt;ehcache&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;!-- springboot start --&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-actuator&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-aop&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-cache&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-quartz&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-starter-web&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;de.codecentric&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-admin-starter-client&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.mybatis.spring.boot&lt;/groupId&gt;
            &lt;artifactId&gt;mybatis-spring-boot-starter&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.retry&lt;/groupId&gt;
            &lt;artifactId&gt;spring-retry&lt;/artifactId&gt;
        &lt;/dependency&gt;

        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-devtools&lt;/artifactId&gt;
            &lt;scope&gt;runtime&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;mysql&lt;/groupId&gt;
            &lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;
            &lt;scope&gt;runtime&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-configuration-processor&lt;/artifactId&gt;
            &lt;optional&gt;true&lt;/optional&gt;
        &lt;/dependency&gt;
        &lt;!-- springboot start --&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;commons-collections&lt;/groupId&gt;
            &lt;artifactId&gt;commons-collections&lt;/artifactId&gt;
        &lt;/dependency&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;commons-io&lt;/groupId&gt;
            &lt;artifactId&gt;commons-io&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;!-- end apache --&gt;

        &lt;!-- DBPool start --&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
            &lt;artifactId&gt;commons-pool2&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
            &lt;artifactId&gt;commons-dbcp2&lt;/artifactId&gt;
        &lt;/dependency&gt;
        &lt;!-- DBPool end --&gt;


        &lt;dependency&gt;
            &lt;groupId&gt;joda-time&lt;/groupId&gt;
            &lt;artifactId&gt;joda-time&lt;/artifactId&gt;
        &lt;/dependency&gt;


        &lt;!-- test start --&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;junit&lt;/groupId&gt;
            &lt;artifactId&gt;junit&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-module-junit4-rule-agent&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock.tests&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-tests-utils&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-core&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-module-junit4&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.mockito&lt;/groupId&gt;
            &lt;artifactId&gt;mockito-all&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-api-mockito&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.powermock&lt;/groupId&gt;
            &lt;artifactId&gt;powermock-classloading-xstream&lt;/artifactId&gt;
            &lt;scope&gt;test&lt;/scope&gt;
        &lt;/dependency&gt;
        &lt;!-- test end --&gt;

    &lt;/dependencies&gt;

    &lt;!-- spring-boot-maven-plugin  start --&gt;
    &lt;build&gt;
        &lt;plugins&gt;
            &lt;plugin&gt;
                &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
                &lt;artifactId&gt;spring-boot-maven-plugin&lt;/artifactId&gt;
            &lt;/plugin&gt;
        &lt;/plugins&gt;
    &lt;/build&gt;

&lt;/project&gt;

</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">【特别注意】</p> 
 <p style="font-size: 14px;">这里需要额外注意一个问题：带有&nbsp;<span class="s1" style="font-family: 'Courier New';">@</span><span class="s2" style="font-family: 'Courier New';">SpringBootApplication 的&nbsp;</span><span style="font-family: 'Courier New';">Application.java(内含</span><span class="s1" style="font-family: 'Courier New';"><strong>public</strong></span><span class="s1" style="font-family: 'Courier New';"><strong>static</strong></span><span class="s1" style="font-family: 'Courier New';"><strong>void</strong></span><span style="font-family: 'Courier New';"> main(String[] </span><span class="s2" style="font-family: 'Courier New';">args</span><span style="font-family: 'Courier New';">)）方法的类，一定要放在几个module公用的package的那一层级，否则会引起找不到各个@Servce等注解类的情况。</span></p> 
 <pre name="code" class="java">org.kanpiaoxue.helloworld_commons
org.kanpiaoxue.helloworld_dao
org.kanpiaoxue.helloworld_service
org.kanpiaoxue.helloworld_web</pre> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New';">&nbsp;针对上面的几个module，它们各自有自己的package。如上。</span></p> 
 <p style="font-size: 14px;"><span style="font-size: 14px; font-family: 'Courier New';">我在&nbsp;</span><span style="font-family: 'Courier New';">org.kanpiaoxue.helloworld_web 下面创建了带有 @SpringBootApplication 的 Application.java(内含public static void main(String[] args)）方法的类，启动程序的是否发现总是有服务类无法被扫描到。因为&nbsp;@SpringBootApplication 是从当前&nbsp;Application.java 所在的package：org.kanpiaoxue.helloworld_web 向下扫描的，它自然无法扫描到其他的几个package：</span></p> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New';">org.kanpiaoxue.helloworld_commons</span></p> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New';">org.kanpiaoxue.helloworld_dao</span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New';">org.kanpiaoxue.helloworld_service</span></p> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New';">解决方案：将带有 @SpringBootApplication 的 Application.java(内含public static void main(String[] args)）方法的类，挪到这几个module公用的package的路径：</span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">org.kanpiaoxue</pre> 
 <p style="font-size: 14px;"><span style="font-family: 'Courier New';">&nbsp;下面，就解决了该问题。</span></p> 
 <p style="font-size: 14px;">&nbsp;我发现也有人遇到类似的问题，可以参考：</p> 
 <p style="font-size: 14px;">关于SpringBoot bean无法注入的问题（与文件包位置有关）改变自动扫描的：<a href="https://blog.csdn.net/u014695188/article/details/52263903">https://blog.csdn.net/u014695188/article/details/52263903</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">还有一种解决<span style="font-size: 14px; font-family: 'Courier New';">Application.java找不到各种@Service的方法就是在</span><span style="font-family: 'Courier New';">@SpringBootApplication里面添加包的扫描路径。如下：</span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@SpringBootApplication(scanBasePackages = "org.kanpiaoxue")
@EnableTransactionManagement
@MapperScan("org.kanpiaoxue.csis.dao")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>