#maven web pom文件常用配置
###发表时间：2014-01-17
###分类：java,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2005675" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2005675</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="xml">&lt;project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"&gt;
	&lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;
	&lt;groupId&gt;com.wanmei.demoForYuzhi&lt;/groupId&gt;
	&lt;artifactId&gt;demo&lt;/artifactId&gt;
	&lt;version&gt;0.0.1-SNAPSHOT&lt;/version&gt;
	&lt;packaging&gt;war&lt;/packaging&gt;
	&lt;name&gt;demoForYuzhi&lt;/name&gt;

	&lt;description&gt;给于智做的测试样例&lt;/description&gt;

	&lt;properties&gt;
		&lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
		&lt;spring.version&gt;4.0.0.RELEASE&lt;/spring.version&gt;
		&lt;org.slf4j.version&gt;1.6.6&lt;/org.slf4j.version&gt;
		&lt;commons-logging.version&gt;1.1.1&lt;/commons-logging.version&gt;
		&lt;log4j.version&gt;1.2.14&lt;/log4j.version&gt;
		&lt;guava.version&gt;16.0&lt;/guava.version&gt;
		&lt;junit.version&gt;4.11&lt;/junit.version&gt;
		&lt;fastjson.version&gt;1.1.22&lt;/fastjson.version&gt;
		&lt;h2.version&gt;1.3.175&lt;/h2.version&gt;
		&lt;netty.version&gt;3.8.0.Final&lt;/netty.version&gt;
		&lt;quartz.version&gt;2.2.1&lt;/quartz.version&gt;
                &lt;jetty.version&gt;9.1.4.v20140401&lt;/jetty.version&gt;
	&lt;/properties&gt;

	&lt;dependencies&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.eclipse.jetty.aggregate&lt;/groupId&gt;
			&lt;artifactId&gt;jetty-all&lt;/artifactId&gt;
			&lt;version&gt;${jetty.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- database h2 start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.h2database&lt;/groupId&gt;
			&lt;artifactId&gt;h2&lt;/artifactId&gt;
			&lt;version&gt;${h2.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- database h2 end --&gt;

&lt;dependency&gt;
	&lt;groupId&gt;org.apache.tomcat&lt;/groupId&gt;
	&lt;artifactId&gt;servlet-api&lt;/artifactId&gt;
	&lt;version&gt;6.0.39&lt;/version&gt;
&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.google.guava&lt;/groupId&gt;
			&lt;artifactId&gt;guava&lt;/artifactId&gt;
			&lt;version&gt;${guava.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- test start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;junit&lt;/groupId&gt;
			&lt;artifactId&gt;junit&lt;/artifactId&gt;
			&lt;version&gt;${junit.version}&lt;/version&gt;
			&lt;scope&gt;test&lt;/scope&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.easymock&lt;/groupId&gt;
			&lt;artifactId&gt;easymock&lt;/artifactId&gt;
			&lt;version&gt;3.0&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- test end --&gt;

		&lt;!-- jdbc start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.oracle&lt;/groupId&gt;
			&lt;artifactId&gt;ojdbc6&lt;/artifactId&gt;
			&lt;version&gt;11.0&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;mysql&lt;/groupId&gt;
			&lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;
			&lt;version&gt;5.1.27&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- jdbc end --&gt;


		&lt;!-- commons start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-beanutils&lt;/groupId&gt;
			&lt;artifactId&gt;commons-beanutils&lt;/artifactId&gt;
			&lt;version&gt;1.8.3&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-codec&lt;/groupId&gt;
			&lt;artifactId&gt;commons-codec&lt;/artifactId&gt;
			&lt;version&gt;1.8&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-collections&lt;/groupId&gt;
			&lt;artifactId&gt;commons-collections&lt;/artifactId&gt;
			&lt;version&gt;3.2.1&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;commons-dbcp&lt;/groupId&gt;
			&lt;artifactId&gt;commons-dbcp&lt;/artifactId&gt;
			&lt;version&gt;1.4&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-io&lt;/groupId&gt;
			&lt;artifactId&gt;commons-io&lt;/artifactId&gt;
			&lt;version&gt;2.2&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
			&lt;artifactId&gt;commons-lang3&lt;/artifactId&gt;
			&lt;version&gt;3.1&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- commons end --&gt;



		&lt;!-- json start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.alibaba&lt;/groupId&gt;
			&lt;artifactId&gt;fastjson&lt;/artifactId&gt;
			&lt;version&gt;${fastjson.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- json end --&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;javax.transaction&lt;/groupId&gt;
			&lt;artifactId&gt;jta&lt;/artifactId&gt;
			&lt;version&gt;1.1&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;aopalliance&lt;/groupId&gt;
			&lt;artifactId&gt;aopalliance&lt;/artifactId&gt;
			&lt;version&gt;1.0&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;javax.mail&lt;/groupId&gt;
			&lt;artifactId&gt;mail&lt;/artifactId&gt;
			&lt;version&gt;1.4.3&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;javax.activation&lt;/groupId&gt;
			&lt;artifactId&gt;activation&lt;/artifactId&gt;
			&lt;version&gt;1.1&lt;/version&gt;
		&lt;/dependency&gt;


		&lt;!-- spring dependences start --&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.quartz-scheduler&lt;/groupId&gt;
			&lt;artifactId&gt;quartz&lt;/artifactId&gt;
			&lt;version&gt;${quartz.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-fileupload&lt;/groupId&gt;
			&lt;artifactId&gt;commons-fileupload&lt;/artifactId&gt;
			&lt;version&gt;1.3&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.aspectj&lt;/groupId&gt;
			&lt;artifactId&gt;aspectjweaver&lt;/artifactId&gt;
			&lt;version&gt;1.7.4&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- spring dependences end --&gt;


		&lt;!-- jms start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;javax.jms&lt;/groupId&gt;
			&lt;artifactId&gt;javax.jms-api&lt;/artifactId&gt;
			&lt;version&gt;2.0&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- jms end --&gt;

		&lt;!-- netty start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;io.netty&lt;/groupId&gt;
			&lt;artifactId&gt;netty&lt;/artifactId&gt;
			&lt;version&gt;${netty.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- netty end --&gt;


		&lt;!-- spring start --&gt;

		&lt;!-- spring log dependency start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
			&lt;artifactId&gt;jcl-over-slf4j&lt;/artifactId&gt;
			&lt;version&gt;${org.slf4j.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
			&lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;
			&lt;version&gt;${org.slf4j.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
			&lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
			&lt;version&gt;${org.slf4j.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;log4j&lt;/groupId&gt;
			&lt;artifactId&gt;log4j&lt;/artifactId&gt;
			&lt;version&gt;${log4j.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-logging&lt;/groupId&gt;
			&lt;artifactId&gt;commons-logging&lt;/artifactId&gt;
			&lt;version&gt;${commons-logging.version}&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- spring log dependency end --&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-context&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-aop&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-aspects&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-beans&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-core&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-expression&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-instrument&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-jdbc&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-jms&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-orm&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-oxm&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-test&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-tx&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;


		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-web&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring-webmvc&lt;/artifactId&gt;
			&lt;version&gt;${spring.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;
			&lt;artifactId&gt;jackson-core&lt;/artifactId&gt;
			&lt;version&gt;2.3.0&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.fasterxml.jackson.core&lt;/groupId&gt;
			&lt;artifactId&gt;jackson-databind&lt;/artifactId&gt;
			&lt;version&gt;2.3.0&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- spring end --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;bean-validator&lt;/artifactId&gt;
			&lt;version&gt;3.0-JBoss-4.0.2&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.enterprise.deploy&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.jms&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.management.j2ee&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.eclipse.persistence&lt;/groupId&gt;
			&lt;artifactId&gt;javax.persistence&lt;/artifactId&gt;
			&lt;version&gt;2.0.0&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.resource&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.security.auth.message&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.security.jacc&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.servlet&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.servlet.jsp&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish&lt;/groupId&gt;
			&lt;artifactId&gt;javax.servlet.jsp.jstl&lt;/artifactId&gt;
			&lt;version&gt;3.0.1&lt;/version&gt;
			&lt;!-- &lt;scope&gt;provided&lt;/scope&gt; --&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;javax.xml.bind&lt;/groupId&gt;
			&lt;artifactId&gt;jaxb-api-osgi&lt;/artifactId&gt;
			&lt;version&gt;2.2.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;javax.ws.rs&lt;/groupId&gt;
			&lt;artifactId&gt;jsr311-api&lt;/artifactId&gt;
			&lt;version&gt;1.1.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.glassfish.web&lt;/groupId&gt;
			&lt;artifactId&gt;jstl-impl&lt;/artifactId&gt;
			&lt;version&gt;1.2&lt;/version&gt;
			&lt;!-- scope&gt;provided&lt;/scope&gt; --&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;javax.xml&lt;/groupId&gt;
			&lt;artifactId&gt;webservices-api-osgi&lt;/artifactId&gt;
			&lt;version&gt;2.0.1&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.jboss.weld&lt;/groupId&gt;
			&lt;artifactId&gt;weld-osgi-bundle&lt;/artifactId&gt;
			&lt;version&gt;1.0.1-SP3&lt;/version&gt;
			&lt;scope&gt;provided&lt;/scope&gt;
		&lt;/dependency&gt;
	&lt;/dependencies&gt;

	&lt;build&gt;
		&lt;plugins&gt;
			&lt;plugin&gt;
				&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
				&lt;artifactId&gt;maven-source-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.2.1&lt;/version&gt;
				&lt;executions&gt;
					&lt;execution&gt;
						&lt;id&gt;attach-sources&lt;/id&gt;
						&lt;phase&gt;verify&lt;/phase&gt;
						&lt;goals&gt;
							&lt;goal&gt;jar-no-fork&lt;/goal&gt;
						&lt;/goals&gt;
					&lt;/execution&gt;
				&lt;/executions&gt;
			&lt;/plugin&gt;
			&lt;plugin&gt;
				&lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.3.2&lt;/version&gt;
				&lt;configuration&gt;
					&lt;source&gt;1.7&lt;/source&gt;
					&lt;target&gt;1.7&lt;/target&gt;
				&lt;/configuration&gt;
			&lt;/plugin&gt;
			&lt;plugin&gt;
				&lt;artifactId&gt;maven-war-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.2&lt;/version&gt;
				&lt;configuration&gt;
					&lt;version&gt;3.0&lt;/version&gt;
					&lt;failOnMissingWebXml&gt;false&lt;/failOnMissingWebXml&gt;
				&lt;/configuration&gt;
			&lt;/plugin&gt;
			&lt;plugin&gt;
				&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
				&lt;artifactId&gt;maven-source-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.2.1&lt;/version&gt;
				&lt;!-- &lt;configuration&gt; &lt;outputDirectory&gt;/absolute/path/to/the/output/directory&lt;/outputDirectory&gt; 
					&lt;finalName&gt;filename-of-generated-jar-file&lt;/finalName&gt; &lt;attach&gt;false&lt;/attach&gt; 
					&lt;/configuration&gt; --&gt;
				&lt;executions&gt;
					&lt;execution&gt;
						&lt;id&gt;attach-sources&lt;/id&gt;
						&lt;goals&gt;
							&lt;goal&gt;jar&lt;/goal&gt;
						&lt;/goals&gt;
					&lt;/execution&gt;
				&lt;/executions&gt;
			&lt;/plugin&gt;

		&lt;/plugins&gt;
	&lt;/build&gt;

	&lt;reporting&gt;
		&lt;plugins&gt;
			&lt;!-- 测试报告 --&gt;
			&lt;plugin&gt;
				&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
				&lt;artifactId&gt;maven-surefire-report-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.16&lt;/version&gt;
				&lt;configuration&gt;
					&lt;showSuccess&gt;false&lt;/showSuccess&gt;
				&lt;/configuration&gt;
			&lt;/plugin&gt;

			&lt;!-- 项目源码 plugin --&gt;
			&lt;plugin&gt;
				&lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
				&lt;artifactId&gt;maven-jxr-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.2&lt;/version&gt;
				&lt;configuration&gt;
					&lt;!-- 只有聚合项目需要使用该配置 --&gt;
					&lt;aggregate&gt;false&lt;/aggregate&gt;
				&lt;/configuration&gt;
			&lt;/plugin&gt;

			&lt;!-- PMD 代码分析工具 --&gt;
			&lt;plugin&gt;
				&lt;artifactId&gt;maven-pmd-plugin&lt;/artifactId&gt;
				&lt;version&gt;3.0.1&lt;/version&gt;
				&lt;reportSets&gt;
					&lt;reportSet&gt;
						&lt;reports&gt;
							&lt;report&gt;pmd&lt;/report&gt;
							&lt;report&gt;cpd&lt;/report&gt;
						&lt;/reports&gt;
					&lt;/reportSet&gt;
				&lt;/reportSets&gt;
			&lt;/plugin&gt;
			&lt;plugin&gt;
				&lt;artifactId&gt;maven-javadoc-plugin&lt;/artifactId&gt;
				&lt;version&gt;2.9.1&lt;/version&gt;
			&lt;/plugin&gt;
		&lt;/plugins&gt;
	&lt;/reporting&gt;
&lt;/project&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>maven 命令：</p> 
 <p>mvn help:system &nbsp;--&gt; 所有的Java系统属性和环境变量</p> 
 <p>mvn archetype:generate --&gt; 生产项目的骨架</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">&lt;project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"&gt;
    &lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;

    &lt;!-- Inherit defaults from Spring Boot --&gt;
    &lt;parent&gt;
        &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
        &lt;artifactId&gt;spring-boot-starter-parent&lt;/artifactId&gt;
        &lt;version&gt;2.0.5.RELEASE&lt;/version&gt;
    &lt;/parent&gt;

    &lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
    &lt;artifactId&gt;hello&lt;/artifactId&gt;
    &lt;version&gt;0.0.1&lt;/version&gt;
    &lt;packaging&gt;pom&lt;/packaging&gt;

    &lt;name&gt;hello&lt;/name&gt;
    &lt;url&gt;http://maven.apache.org&lt;/url&gt;

    &lt;modules&gt;
        &lt;module&gt;hello-commons&lt;/module&gt;
        &lt;module&gt;hello-cleanlog&lt;/module&gt;
    &lt;/modules&gt;

    &lt;properties&gt;
        &lt;maven.compiler.source&gt;1.8&lt;/maven.compiler.source&gt;
        &lt;maven.compiler.target&gt;1.8&lt;/maven.compiler.target&gt;

        &lt;guava.version&gt;26.0-jre&lt;/guava.version&gt;
        &lt;gson.version&gt;2.8.5&lt;/gson.version&gt;
        &lt;springboot-admin-client&gt;2.0.3&lt;/springboot-admin-client&gt;

        &lt;!-- test --&gt;
        &lt;junit.version&gt;4.11&lt;/junit.version&gt;
        &lt;powermock.version&gt;1.6.2&lt;/powermock.version&gt;
        &lt;mockito.version&gt;1.10.19&lt;/mockito.version&gt;
    &lt;/properties&gt;


    &lt;dependencyManagement&gt;
        &lt;dependencies&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;de.codecentric&lt;/groupId&gt;
                &lt;artifactId&gt;spring-boot-admin-starter-client&lt;/artifactId&gt;
                &lt;version&gt;${springboot-admin-client}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;!-- https://mvnrepository.com/artifact/com.google.guava/guava --&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
                &lt;artifactId&gt;guava&lt;/artifactId&gt;
                &lt;version&gt;${guava.version}&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;joda-time&lt;/groupId&gt;
                &lt;artifactId&gt;joda-time&lt;/artifactId&gt;
                &lt;version&gt;2.10&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
                &lt;artifactId&gt;commons-lang3&lt;/artifactId&gt;
                &lt;version&gt;3.8&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
                &lt;artifactId&gt;commons-collections4&lt;/artifactId&gt;
                &lt;version&gt;4.2&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;commons-io&lt;/groupId&gt;
                &lt;artifactId&gt;commons-io&lt;/artifactId&gt;
                &lt;version&gt;2.6&lt;/version&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
                &lt;artifactId&gt;commons-configuration2&lt;/artifactId&gt;
                &lt;version&gt;2.3&lt;/version&gt;
            &lt;/dependency&gt;

            &lt;dependency&gt;
                &lt;groupId&gt;com.google.code.gson&lt;/groupId&gt;
                &lt;artifactId&gt;gson&lt;/artifactId&gt;
                &lt;version&gt;${gson.version}&lt;/version&gt;
            &lt;/dependency&gt;


            &lt;!-- test start --&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;junit&lt;/groupId&gt;
                &lt;artifactId&gt;junit&lt;/artifactId&gt;
                &lt;version&gt;${junit.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-module-junit4-rule-agent&lt;/artifactId&gt;
                &lt;version&gt;${powermock.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock.tests&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-tests-utils&lt;/artifactId&gt;
                &lt;version&gt;${powermock.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-core&lt;/artifactId&gt;
                &lt;version&gt;${powermock.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-module-junit4&lt;/artifactId&gt;
                &lt;version&gt;${powermock.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.mockito&lt;/groupId&gt;
                &lt;artifactId&gt;mockito-all&lt;/artifactId&gt;
                &lt;version&gt;${mockito.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-api-mockito&lt;/artifactId&gt;
                &lt;version&gt;${powermock.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;dependency&gt;
                &lt;groupId&gt;org.powermock&lt;/groupId&gt;
                &lt;artifactId&gt;powermock-classloading-xstream&lt;/artifactId&gt;
                &lt;version&gt;${powermock.version}&lt;/version&gt;
                &lt;scope&gt;test&lt;/scope&gt;
            &lt;/dependency&gt;
            &lt;!-- test end --&gt;

        &lt;/dependencies&gt;
    &lt;/dependencyManagement&gt;


&lt;/project&gt;
</pre> 
 <p>&nbsp;</p> 
</div>