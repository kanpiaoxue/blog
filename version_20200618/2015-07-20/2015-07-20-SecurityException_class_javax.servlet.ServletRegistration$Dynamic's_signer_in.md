#SecurityException: class "javax.servlet.ServletRegistration$Dynamic"'s signer in
###发表时间：2015-07-20
###分类：maven,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2228874" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2228874</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在运行maven打包程序或者使用maven运行单测的时候，遇到下面的问题：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  java.lang.IllegalStateException: Failed to load ApplicationContext
  <br> at org.springframework.test.context.DefaultCacheAwareContextLoaderDelegate.loadContext(DefaultCacheAwareContextLoaderDelegate.java:94)
  <br> at org.springframework.test.context.DefaultTestContext.getApplicationContext(DefaultTestContext.java:72)
  <br> at org.springframework.test.context.support.DependencyInjectionTestExecutionListener.injectDependencies(DependencyInjectionTestExecutionListener.java:117)
  <br> at org.springframework.test.context.support.DependencyInjectionTestExecutionListener.prepareTestInstance(DependencyInjectionTestExecutionListener.java:83)
  <br> at org.springframework.test.context.TestContextManager.prepareTestInstance(TestContextManager.java:212)
  <br> at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.createTest(SpringJUnit4ClassRunner.java:200)
  <br> at org.springframework.test.context.junit4.SpringJUnit4ClassRunner$1.runReflectiveCall(SpringJUnit4ClassRunner.java:259)
  <br> at org.junit.internal.runners.model.ReflectiveCallable.run(ReflectiveCallable.java:12)
  <br> at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.methodBlock(SpringJUnit4ClassRunner.java:261)
  <br> at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:219)
  <br> at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.runChild(SpringJUnit4ClassRunner.java:83)
  <br> at org.junit.runners.ParentRunner$3.run(ParentRunner.java:238)
  <br> at org.junit.runners.ParentRunner$1.schedule(ParentRunner.java:63)
  <br> at org.junit.runners.ParentRunner.runChildren(ParentRunner.java:236)
  <br> at org.junit.runners.ParentRunner.access$000(ParentRunner.java:53)
  <br> at org.junit.runners.ParentRunner$2.evaluate(ParentRunner.java:229)
  <br> at org.springframework.test.context.junit4.statements.RunBeforeTestClassCallbacks.evaluate(RunBeforeTestClassCallbacks.java:61)
  <br> at org.springframework.test.context.junit4.statements.RunAfterTestClassCallbacks.evaluate(RunAfterTestClassCallbacks.java:68)
  <br> at org.junit.runners.ParentRunner.run(ParentRunner.java:309)
  <br> at org.springframework.test.context.junit4.SpringJUnit4ClassRunner.run(SpringJUnit4ClassRunner.java:163)
  <br> at org.eclipse.jdt.internal.junit4.runner.JUnit4TestReference.run(JUnit4TestReference.java:50)
  <br> at org.eclipse.jdt.internal.junit.runner.TestExecution.run(TestExecution.java:38)
  <br> at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:459)
  <br> at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.runTests(RemoteTestRunner.java:675)
  <br> at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.run(RemoteTestRunner.java:382)
  <br> at org.eclipse.jdt.internal.junit.runner.RemoteTestRunner.main(RemoteTestRunner.java:192)
  <br>Caused by: java.lang.SecurityException: class "javax.servlet.ServletRegistration$Dynamic"'s signer information does not match signer information of other classes in the same package
  <br> at java.lang.ClassLoader.checkCerts(ClassLoader.java:806)
  <br> at java.lang.ClassLoader.preDefineClass(ClassLoader.java:487)
  <br> at java.lang.ClassLoader.defineClassCond(ClassLoader.java:625)
  <br> at java.lang.ClassLoader.defineClass(ClassLoader.java:615)
  <br> at java.security.SecureClassLoader.defineClass(SecureClassLoader.java:141)
  <br> at java.net.URLClassLoader.defineClass(URLClassLoader.java:283)
  <br> at java.net.URLClassLoader.access$000(URLClassLoader.java:58)
  <br> at java.net.URLClassLoader$1.run(URLClassLoader.java:197)
  <br> at java.security.AccessController.doPrivileged(Native Method)
  <br> at java.net.URLClassLoader.findClass(URLClassLoader.java:190)
  <br> at java.lang.ClassLoader.loadClass(ClassLoader.java:306)
  <br> at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:301)
  <br> at java.lang.ClassLoader.loadClass(ClassLoader.java:247)
  <br> at java.lang.Class.getDeclaredMethods0(Native Method)
  <br> at java.lang.Class.privateGetDeclaredMethods(Class.java:2436)
  <br> at java.lang.Class.getDeclaredMethods(Class.java:1793)
  <br> at org.springframework.util.ReflectionUtils.getDeclaredMethods(ReflectionUtils.java:571)
  <br> at org.springframework.util.ReflectionUtils.doWithMethods(ReflectionUtils.java:488)
  <br> at org.springframework.util.ReflectionUtils.doWithMethods(ReflectionUtils.java:474)
  <br> at org.springframework.beans.factory.annotation.AutowiredAnnotationBeanPostProcessor.determineCandidateConstructors(AutowiredAnnotationBeanPostProcessor.java:241)
  <br> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.determineConstructorsFromBeanPostProcessors(AbstractAutowireCapableBeanFactory.java:1065)
  <br> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBeanInstance(AbstractAutowireCapableBeanFactory.java:1038)
  <br> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:504)
  <br> at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:476)
  <br> at org.springframework.beans.factory.support.AbstractBeanFactory$1.getObject(AbstractBeanFactory.java:303)
  <br> at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:230)
  <br> at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:299)
  <br> at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:194)
  <br> at org.springframework.beans.factory.support.DefaultListableBeanFactory.preInstantiateSingletons(DefaultListableBeanFactory.java:755)
  <br> at org.springframework.context.support.AbstractApplicationContext.finishBeanFactoryInitialization(AbstractApplicationContext.java:757)
  <br> at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:480)
  <br> at org.springframework.test.context.support.AbstractGenericContextLoader.loadContext(AbstractGenericContextLoader.java:125)
  <br> at org.springframework.test.context.support.AbstractGenericContextLoader.loadContext(AbstractGenericContextLoader.java:60)
  <br> at org.springframework.test.context.support.AbstractDelegatingSmartContextLoader.delegateLoading(AbstractDelegatingSmartContextLoader.java:109)
  <br> at org.springframework.test.context.support.AbstractDelegatingSmartContextLoader.loadContext(AbstractDelegatingSmartContextLoader.java:261)
  <br> at org.springframework.test.context.DefaultCacheAwareContextLoaderDelegate.loadContextInternal(DefaultCacheAwareContextLoaderDelegate.java:68)
  <br> at org.springframework.test.context.DefaultCacheAwareContextLoaderDelegate.loadContext(DefaultCacheAwareContextLoaderDelegate.java:86)
  <br> ... 25 more
 </div> 
 <p>&nbsp;</p> 
 <p>看了看，主要是说：在classpath里面存在一个同名同包的类出现了多次，造成程序运行的过程中无法确定具体引用那个类来运行程序。</p> 
 <p>maven引入jar的时候，这些pom.xml里面声明的jar还会依赖于别的jar，会被maven自动下载下来放入classpath里面。这个时候就会造成同名同包的jar被多次引用。</p> 
 <p>知道了问题，就需要进行解决：将那么多余的同名同包的jar进行排查，只留下一个合适的jar。</p> 
 <p>如何排除呢？如下：</p> 
 <pre name="code" class="xml">		&lt;dependency&gt;
			&lt;groupId&gt;com.baidu.rigel.dmap&lt;/groupId&gt;
			&lt;artifactId&gt;dmap-business&lt;/artifactId&gt;
			&lt;version&gt;${project.version}&lt;/version&gt;
			&lt;scope&gt;test&lt;/scope&gt;
			&lt;type&gt;test-jar&lt;/type&gt;
			&lt;exclusions&gt;
				&lt;exclusion&gt;
					&lt;groupId&gt;javax.servlet&lt;/groupId&gt;
					&lt;artifactId&gt;servlet-api&lt;/artifactId&gt;
				&lt;/exclusion&gt;
			&lt;/exclusions&gt;
		&lt;/dependency&gt;</pre> 
 <p>&nbsp;使用&nbsp;<span style="font-family: monospace; line-height: 1.5; background-color: #fafafa;">exclusions 将这些jar排查。</span></p> 
 <p><span style="font-family: monospace;"><span style="background-color: #fafafa;">那么如何确定有哪些jar是同名同包冲突的呢？</span></span></p> 
 <p><span style="font-family: monospace;"><span style="background-color: #fafafa;">可以执行maven的一个命令，查找依赖关系树：</span></span></p> 
 <p><span style="font-family: monospace;"><span style="background-color: #fafafa;">mvn -f=D:\baidu\workspaces\workspace_java\dmap\dmap-scheduleframework\pom.xml &nbsp;dependency:tree &gt; d:\dependency.tree.txt</span></span></p> 
 <p><span style="font-family: monospace;"><span style="background-color: #fafafa;">这样就可以将这些依赖关系保存在文件中，如下：</span></span></p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  写道
 </div> 
 <p>&nbsp;</p> 
 <div class="quote_div">
  [INFO] Scanning for projects...
  <br>[WARNING] 
  <br>[WARNING] Some problems were encountered while building the effective model for org.kanpiaoxue.rigel.dmap:dmap-scheduleframework:jar:1.0
  <br>[WARNING] 'dependencies.dependency.(groupId:artifactId:type:classifier)' must be unique: mysql:mysql-connector-java:jar -&gt; version (?) vs 5.1.13 @ org.kanpiaoxue.rigel.dmap:dmap-scheduleframework:[unknown-version], D:\baidu\workspaces\workspace_java\dmap\dmap-scheduleframework\pom.xml, line 492, column 15
  <br>[WARNING] 
  <br>[WARNING] It is highly recommended to fix these problems because they threaten the stability of your build.
  <br>[WARNING] 
  <br>[WARNING] For this reason, future Maven versions might no longer support building such malformed projects.
  <br>[WARNING] 
  <br>[INFO] 
  <br>[INFO] ------------------------------------------------------------------------
  <br>[INFO] Building dmap-scheduleframework 1.0
  <br>[INFO] ------------------------------------------------------------------------
  <br>[WARNING] The artifact freemarker:freemarker:jar:2.3.9 has been relocated to org.freemarker:freemarker:jar:2.3.9
  <br>[INFO] 
  <br>[INFO] --- maven-dependency-plugin:2.8:tree (default-cli) @ dmap-scheduleframework ---
  <br>[WARNING] The artifact freemarker:freemarker:jar:2.3.9 has been relocated to org.freemarker:freemarker:jar:2.3.9
  <br>[INFO] org.kanpiaoxue.rigel.dmap:dmap-scheduleframework:jar:1.0
  <br>[INFO] +- org.kanpiaoxue.uic:uic-client:jar:2.0.0:compile
  <br>[INFO] | +- org.apache.cxf:cxf-rt-core:jar:2.7.5:compile
  <br>[INFO] | | +- org.apache.cxf:cxf-api:jar:2.7.5:compile
  <br>[INFO] | | | +- org.codehaus.woodstox:woodstox-core-asl:jar:4.2.0:compile
  <br>[INFO] | | | | \- org.codehaus.woodstox:stax2-api:jar:3.1.1:compile
  <br>[INFO] | | | \- wsdl4j:wsdl4j:jar:1.6.3:compile
  <br>[INFO] | | +- com.sun.xml.bind:jaxb-impl:jar:2.2.6:compile
  <br>[INFO] | | +- org.apache.ws.xmlschema:xmlschema-core:jar:2.0.3:compile
  <br>[INFO] | | \- org.apache.geronimo.specs:geronimo-javamail_1.4_spec:jar:1.7.1:compile
  <br>[INFO] | +- org.apache.cxf:cxf-rt-frontend-jaxws:jar:2.7.5:compile
  <br>[INFO] | | +- xml-resolver:xml-resolver:jar:1.2:compile
  <br>[INFO] | | +- asm:asm:jar:3.3.1:compile
  <br>[INFO] | | +- org.apache.cxf:cxf-rt-bindings-soap:jar:2.7.5:compile
  <br>[INFO] | | | \- org.apache.cxf:cxf-rt-databinding-jaxb:jar:2.7.5:compile
  <br>[INFO] | | +- org.apache.cxf:cxf-rt-bindings-xml:jar:2.7.5:compile
  <br>[INFO] | | +- org.apache.cxf:cxf-rt-frontend-simple:jar:2.7.5:compile
  <br>[INFO] | | \- org.apache.cxf:cxf-rt-ws-addr:jar:2.7.5:compile
  <br>[INFO] | | \- org.apache.cxf:cxf-rt-ws-policy:jar:2.7.5:compile
  <br>[INFO] | | \- org.apache.neethi:neethi:jar:3.0.2:compile
  <br>[INFO] | +- org.apache.cxf:cxf-rt-transports-http:jar:2.7.5:compile
  <br>[INFO] | \- commons-lang:commons-lang:jar:2.4:compile
  <br>[INFO] +- net.sf.ehcache:ehcache:jar:2.8.3:compile
  <br>[INFO] +- org.kanpiaoxue.rigel.dmap:dmap-commons:jar:1.0:compile
  <br>[INFO] | \- commons-validator:commons-validator:jar:1.4.0:compile
  <br>[INFO] | \- commons-digester:commons-digester:jar:1.8:compile
  <br>[INFO] +- org.kanpiaoxue.rigel.dmap:dmap-protobuf:jar:1.0:compile
  <br>[INFO] +- org.kanpiaoxue.rigel.dmap:dmap-business:test-jar:tests:1.0:test
  <br>[INFO] | +- org.springframework:spring-context-support:jar:4.1.6.RELEASE:compile
  <br>[INFO] | \- org.kanpiaoxue:bjf:jar:1.0.0.9:compile
  <br>[INFO] | +- org.kanpiaoxue:bjf-management:jar:1.0.0.2:compile
  <br>[INFO] | +- org.kanpiaoxue:bjf-tcom-compatible:jar:1.0.0.0:compile
  <br>[INFO] | +- org.kanpiaoxue.rigel:tcom-base:jar:1.0.0.6.2:compile
  <br>[INFO] | | \- com.ibm.icu:icu4j:jar:49.1:compile
  <br>[INFO] | +- commons-httpclient:commons-httpclient:jar:3.1:compile
  <br>[INFO] | +- org.hibernate:hibernate:jar:3.2.7.ga:compile
  <br>[INFO] | | +- asm:asm-attrs:jar:1.5.3:compile
  <br>[INFO] | | +- antlr:antlr:jar:2.7.6:compile
  <br>[INFO] | | \- cglib:cglib:jar:2.1_3:compile
  <br>[INFO] | +- org.jasypt:jasypt:jar:1.6:compile
  <br>[INFO] | +- com.google:jsonplugin:jar:0.30:compile
  <br>[INFO] | +- javax.annotation:jsr250-api:jar:1.0:compile
  <br>[INFO] | +- org.apache.struts:struts2-convention-plugin:jar:2.2.1:compile
  <br>[INFO] | +- org.kanpiaoxue.rigel.tmp:struts2-core:jar:2.2.1.1.1:compile
  <br>[INFO] | +- org.ostermiller:utils:jar:1.07.00:compile
  <br>[INFO] | +- commons-net:commons-net:jar:2.0:compile
  <br>[INFO] | +- org.hibernate:hibernate-annotations:jar:3.4.0.GA:compile
  <br>[INFO] | | +- org.hibernate:ejb3-persistence:jar:1.0.2.GA:compile
  <br>[INFO] | | \- org.hibernate:hibernate-commons-annotations:jar:3.1.0.GA:compile
  <br>[INFO] | +- org.kanpiaoxue.rigel.tmp:mcpack:jar:1.0.1:compile
  <br>[INFO] | +- org.kanpiaoxue.rigel.tmp:json-rpc:jar:1.1.2:compile
  <br>[INFO] | +- org.kanpiaoxue.rigel.tmp:wireformat:jar:1.0:compile
  <br>[INFO] | +- org.kanpiaoxue.rigel:security-client:jar:1.0.0.0:compile
  <br>[INFO] | +- net.spy:memcached:jar:2.1:compile
  <br>[INFO] | +- com.caucho:hessian:jar:3.2.0:compile
  <br>[INFO] | +- net.spy:spy:jar:2.4:compile
  <br>[INFO] | +- org.apache.struts.xwork:xwork-core:jar:2.2.1.1:compile
  <br>[INFO] | | \- ognl:ognl:jar:3.0:compile
  <br>[INFO] | +- oro:oro:jar:2.0.8:compile
  <br>[INFO] | +- org.apache.velocity:velocity:jar:1.6.3:compile
  <br>[INFO] | +- javax.servlet.jsp:jsp-api:jar:2.1:compile
  <br>[INFO] | +- redis.clients:jedis:jar:2.0.0:compile
  <br>[INFO] | \- velocity-tools:velocity-tools:jar:1.4:compile
  <br>[INFO] +- org.kanpiaoxue.rigel.dmap:dmap-business:jar:1.0:compile
  <br>[INFO] +- org.kanpiaoxue.rigel.drun:drun-client:jar:1.0:compile
  <br>[INFO] +- org.kanpiaoxue.rigel.drun:drun-commons:jar:1.0:compile
  <br>[INFO] | \- io.netty:netty:jar:3.8.0.Final:compile
  <br>[INFO] +- io.netty:netty-all:jar:4.0.24.Final:compile
  <br>[INFO] +- org.freemarker:freemarker:jar:2.3.9:compile
  <br>[INFO] +- org.apache.zookeeper:zookeeper:jar:3.4.5:compile
  <br>[INFO] | \- jline:jline:jar:0.9.94:compile
  <br>[INFO] +- com.google.protobuf:protobuf-java:jar:2.6.0:compile
  <br>[INFO] +- org.apache.httpcomponents:httpclient:jar:4.3.2:compile
  <br>[INFO] +- org.apache.httpcomponents:httpcore:jar:4.3.2:compile
  <br>[INFO] +- org.apache.thrift:libthrift:jar:0.9.1:compile
  <br>[INFO] +- commons-pool:commons-pool:jar:1.6:compile
  <br>[INFO] +- commons-io:commons-io:jar:2.4:compile
  <br>[INFO] +- com.google.code.gson:gson:jar:2.2.2:compile
  <br>[INFO] +- commons-configuration:commons-configuration:jar:1.10:compile
  <br>[INFO] +- org.apache.curator:curator-recipes:jar:2.7.0:compile
  <br>[INFO] | \- org.apache.curator:curator-framework:jar:2.7.0:compile
  <br>[INFO] | \- org.apache.curator:curator-client:jar:2.7.0:compile
  <br>[INFO] +- org.apache.curator:curator-x-discovery:jar:2.7.0:compile
  <br>[INFO] | \- org.codehaus.jackson:jackson-mapper-asl:jar:1.9.13:compile
  <br>[INFO] | \- org.codehaus.jackson:jackson-core-asl:jar:1.9.13:compile
  <br>[INFO] +- commons-collections:commons-collections:jar:3.2.1:compile
  <br>[INFO] +- org.kanpiaoxue.cap:billboard-client:jar:2.0.0.1:compile
  <br>[INFO] +- joda-time:joda-time:jar:2.5:compile
  <br>[INFO] +- org.eclipse.jetty.aggregate:jetty-all:jar:8.1.17.v20150415:compile
  <br>[INFO] | \- org.eclipse.jetty.orbit:javax.servlet:jar:3.0.0.v201112011016:compile
  <br>[INFO] +- com.google.guava:guava:jar:18.0:compile
  <br>[INFO] +- junit:junit:jar:4.11:test
  <br>[INFO] | \- org.hamcrest:hamcrest-core:jar:1.3:test
  <br>[INFO] +- org.easymock:easymock:jar:3.2:test
  <br>[INFO] | +- cglib:cglib-nodep:jar:2.2.2:test
  <br>[INFO] | \- org.objenesis:objenesis:jar:1.3:test
  <br>[INFO] +- org.powermock:powermock-module-junit4-rule-agent:jar:1.5.6:test
  <br>[INFO] | \- org.powermock:powermock-module-javaagent:jar:1.5.6:test
  <br>[INFO] +- org.powermock.tests:powermock-tests-utils:jar:1.5.6:test
  <br>[INFO] +- org.powermock:powermock-core:jar:1.5.6:test
  <br>[INFO] | +- org.powermock:powermock-reflect:jar:1.5.6:test
  <br>[INFO] | \- org.javassist:javassist:jar:3.18.2-GA:test
  <br>[INFO] +- org.powermock:powermock-module-junit4:jar:1.5.6:test
  <br>[INFO] | \- org.powermock:powermock-module-junit4-common:jar:1.5.6:test
  <br>[INFO] +- org.powermock:powermock-api-mockito:jar:1.5.6:test
  <br>[INFO] | +- org.mockito:mockito-all:jar:1.9.5:test
  <br>[INFO] | \- org.powermock:powermock-api-support:jar:1.5.6:test
  <br>[INFO] +- org.powermock:powermock-classloading-xstream:jar:1.5.6:test
  <br>[INFO] | +- org.powermock:powermock-classloading-base:jar:1.5.6:test
  <br>[INFO] | \- com.thoughtworks.xstream:xstream:jar:1.4.2:test
  <br>[INFO] | +- xmlpull:xmlpull:jar:1.1.3.1:test
  <br>[INFO] | \- xpp3:xpp3_min:jar:1.1.4c:test
  <br>[INFO] +- dom4j:dom4j:jar:1.6.1:compile
  <br>[INFO] | \- xml-apis:xml-apis:jar:1.0.b2:compile
  <br>[INFO] +- mysql:mysql-connector-java:jar:5.1.13:compile
  <br>[INFO] +- commons-beanutils:commons-beanutils:jar:1.8.3:compile
  <br>[INFO] +- commons-codec:commons-codec:jar:1.8:compile
  <br>[INFO] +- commons-dbcp:commons-dbcp:jar:1.4:compile
  <br>[INFO] +- org.apache.commons:commons-lang3:jar:3.1:compile
  <br>[INFO] +- com.alibaba:fastjson:jar:1.1.41:compile
  <br>[INFO] +- javax.transaction:jta:jar:1.1:compile
  <br>[INFO] +- aopalliance:aopalliance:jar:1.0:compile
  <br>[INFO] +- javax.mail:mail:jar:1.4.3:compile
  <br>[INFO] +- javax.activation:activation:jar:1.1:compile
  <br>[INFO] +- org.quartz-scheduler:quartz:jar:2.2.1:compile
  <br>[INFO] | \- c3p0:c3p0:jar:0.9.1.1:compile
  <br>[INFO] +- commons-fileupload:commons-fileupload:jar:1.3:compile
  <br>[INFO] +- org.aspectj:aspectjweaver:jar:1.7.4:compile
  <br>[INFO] +- org.slf4j:slf4j-api:jar:1.7.1:compile
  <br>[INFO] +- org.slf4j:slf4j-log4j12:jar:1.7.1:compile
  <br>[INFO] +- log4j:log4j:jar:1.2.17:compile
  <br>[INFO] +- commons-logging:commons-logging:jar:1.1.3:compile
  <br>[INFO] +- org.springframework:spring-context:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-aop:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-aspects:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-beans:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-core:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-expression:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-instrument:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-jdbc:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-jms:jar:4.1.6.RELEASE:compile
  <br>[INFO] | \- org.springframework:spring-messaging:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-orm:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-oxm:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-test:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-tx:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-web:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- org.springframework:spring-webmvc:jar:4.1.6.RELEASE:compile
  <br>[INFO] +- com.fasterxml.jackson.core:jackson-core:jar:2.3.0:compile
  <br>[INFO] +- com.fasterxml.jackson.core:jackson-databind:jar:2.3.0:compile
  <br>[INFO] | \- com.fasterxml.jackson.core:jackson-annotations:jar:2.3.0:compile
  <br>[INFO] \- com.dbdeploy:maven-dbdeploy-plugin:maven-plugin:3.0M3:compile
  <br>[INFO] +- org.apache.maven:maven-plugin-api:jar:2.0:compile
  <br>[INFO] \- com.dbdeploy:dbdeploy-core:jar:3.0M3:compile
  <br>[INFO] ------------------------------------------------------------------------
  <br>[INFO] BUILD SUCCESS
  <br>[INFO] ------------------------------------------------------------------------
  <br>[INFO] Total time: 4.857 s
  <br>[INFO] Finished at: 2015-07-20T21:40:00+08:00
  <br>[INFO] Final Memory: 16M/216M
  <br>[INFO] ------------------------------------------------------------------------
 </div> 
 <p><span style="font-family: monospace;"><span style="font-family: monospace;">&nbsp;在这个文件里面搜索报错的类就能找到。我报错的是servlet被多次引入。可以在这个文件里面搜索servlet，看看有哪些jar额外的引入了servlet。只保留一个即可。</span></span></p> 
 <p>&nbsp;</p> 
 <p><span style="font-family: monospace;"><span style="font-family: monospace;">还可以参考：<a href="http://stackoverflow.com/questions/2877262/java-securityexception-signer-information-does-not-match">http://stackoverflow.com/questions/2877262/java-securityexception-signer-information-does-not-match</a></span></span></p> 
 <p>&nbsp;</p> 
</div>