#spring h2 junit 编写单元测试
###发表时间：2014-01-13
###分类：junit,maven,java,Spring,h2
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2003472" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2003472</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>最近在看maven。下面给出一个符合maven结构的用spring嵌入H2数据库，进行的单元测试：</p> 
 <p>&nbsp;</p> 
 <p>h2-schema.sql</p> 
 <pre name="code" class="sql">CREATE TABLE TEST(ID INT PRIMARY KEY, NAME VARCHAR);
CREATE TABLE USER(ID INT(11) PRIMARY KEY, NAME VARCHAR(100), AGE INT(2));</pre> 
 <p>&nbsp;</p> 
 <p>h2-test-data.sql</p> 
 <pre name="code" class="sql">INSERT INTO TEST VALUES(1, 'Hello World');
INSERT INTO USER VALUES(1, 'Hello World01', 1);
INSERT INTO USER VALUES(2, 'Hello World02', 2);
INSERT INTO USER VALUES(3, 'Hello World03', 3);
INSERT INTO USER VALUES(4, 'Hello World04', 4);
INSERT INTO USER VALUES(5, 'Hello World05', 5);
INSERT INTO USER VALUES(6, 'Hello World06', 6);
INSERT INTO USER VALUES(7, 'Hello World07', 7);
INSERT INTO USER VALUES(8, 'Hello World08', 8);
INSERT INTO USER VALUES(9, 'Hello World09', 9);
INSERT INTO USER VALUES(10, 'Hello World10', 10);
INSERT INTO USER VALUES(11, 'Hello World11', 11);
INSERT INTO USER VALUES(12, 'Hello World12', 12);
INSERT INTO USER VALUES(13, 'Hello World13', 13);
INSERT INTO USER VALUES(14, 'Hello World14', 14);
INSERT INTO USER VALUES(15, 'Hello World15', 15);
INSERT INTO USER VALUES(16, 'Hello World16', 16);
INSERT INTO USER VALUES(17, 'Hello World17', 17);
INSERT INTO USER VALUES(18, 'Hello World18', 18);
INSERT INTO USER VALUES(19, 'Hello World19', 19);
INSERT INTO USER VALUES(20, 'Hello World20', 20);
INSERT INTO USER VALUES(21, 'Hello World21', 21);
INSERT INTO USER VALUES(22, 'Hello World22', 22);
INSERT INTO USER VALUES(23, 'Hello World23', 23);
INSERT INTO USER VALUES(24, 'Hello World24', 24);
INSERT INTO USER VALUES(25, 'Hello World25', 25);
INSERT INTO USER VALUES(26, 'Hello World26', 26);
INSERT INTO USER VALUES(27, 'Hello World27', 27);
INSERT INTO USER VALUES(28, 'Hello World28', 28);
INSERT INTO USER VALUES(29, 'Hello World29', 29);
INSERT INTO USER VALUES(30, 'Hello World30', 30);
INSERT INTO USER VALUES(31, 'Hello World31', 31);
INSERT INTO USER VALUES(32, 'Hello World32', 32);
INSERT INTO USER VALUES(33, 'Hello World33', 33);
INSERT INTO USER VALUES(34, 'Hello World34', 34);
INSERT INTO USER VALUES(35, 'Hello World35', 35);
INSERT INTO USER VALUES(36, 'Hello World36', 36);
INSERT INTO USER VALUES(37, 'Hello World37', 37);
INSERT INTO USER VALUES(38, 'Hello World38', 38);
INSERT INTO USER VALUES(39, 'Hello World39', 39);
INSERT INTO USER VALUES(40, 'Hello World40', 40);
INSERT INTO USER VALUES(41, 'Hello World41', 41);
INSERT INTO USER VALUES(42, 'Hello World42', 42);
INSERT INTO USER VALUES(43, 'Hello World43', 43);
INSERT INTO USER VALUES(44, 'Hello World44', 44);
INSERT INTO USER VALUES(45, 'Hello World45', 45);
INSERT INTO USER VALUES(46, 'Hello World46', 46);
INSERT INTO USER VALUES(47, 'Hello World47', 47);
INSERT INTO USER VALUES(48, 'Hello World48', 48);
INSERT INTO USER VALUES(49, 'Hello World49', 49);
INSERT INTO USER VALUES(50, 'Hello World50', 50);
INSERT INTO USER VALUES(51, 'Hello World51', 51);
INSERT INTO USER VALUES(52, 'Hello World52', 52);
INSERT INTO USER VALUES(53, 'Hello World53', 53);
INSERT INTO USER VALUES(54, 'Hello World54', 54);
INSERT INTO USER VALUES(55, 'Hello World55', 55);
INSERT INTO USER VALUES(56, 'Hello World56', 56);
INSERT INTO USER VALUES(57, 'Hello World', 32);
INSERT INTO USER VALUES(58, 'Hello World', 32);
INSERT INTO USER VALUES(59, 'Hello World', 32);
INSERT INTO USER VALUES(60, 'Hello World', 32);
</pre> 
 <p>&nbsp;</p> 
 <p>test-spring-h2-application.xml</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:jee="http://www.springframework.org/schema/jee"
	xmlns:jms="http://www.springframework.org/schema/jms" xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:oxm="http://www.springframework.org/schema/oxm"
	xmlns:p="http://www.springframework.org/schema/p" xmlns:sec="http://www.springframework.org/schema/security"
	xmlns:task="http://www.springframework.org/schema/task" xmlns:tx="http://www.springframework.org/schema/tx"
	xmlns:util="http://www.springframework.org/schema/util"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-3.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-3.0.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-3.0.xsd
		http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-3.0.xsd
		http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-3.0.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-3.0.xsd
		http://www.springframework.org/schema/oxm http://www.springframework.org/schema/oxm/spring-oxm-3.0.xsd
		http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security-3.0.xsd
		http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-3.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-3.0.xsd
		http://www.springframework.org/schema/util http://www.springframework.org/schema/util/spring-util-3.0.xsd"&gt;

	&lt;jdbc:embedded-database id="dataSource" type="H2"&gt;
		&lt;jdbc:script location="classpath:h2-schema.sql" /&gt;
		&lt;jdbc:script location="classpath:h2-test-data.sql" /&gt;
	&lt;/jdbc:embedded-database&gt;

	&lt;bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate"&gt;
		&lt;property name="dataSource" ref="dataSource" /&gt;
	&lt;/bean&gt;

&lt;/beans&gt;
</pre> 
 <p>&nbsp;</p> 
 <p>DataAccessUnitTestTemplateForH2Test.java</p> 
 <pre name="code" class="java">package org.kanpiaoxue.test.h2;

import static org.junit.Assert.assertEquals;
import static org.junit.Assert.assertTrue;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.List;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.ApplicationContext;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.test.context.ContextConfiguration;
import org.springframework.test.context.junit4.SpringJUnit4ClassRunner;

/**
 * &lt;pre&gt;
 * @author kanpiaoxue&lt;br&gt;
 * @date 2014年1月13日&lt;br&gt;
 * @Copyright kanpiaoxue.org [2004-2014]&lt;br&gt;
 * @Description : 测试Spring对嵌入式数据H2的支持。
 * 	H2用来做jUnit的测试数据库
 * &lt;/pre&gt;
 */
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath*:test-spring-h2-application.xml")
public class DataAccessUnitTestTemplateForH2Test {
	private JdbcTemplate jdbcTemplate;
	@Autowired
	private ApplicationContext applicationContext;

	@Before
	public void setUp() {
		jdbcTemplate = applicationContext.getBean("jdbcTemplate",
				JdbcTemplate.class);
	}

	/**
	 *&lt;pre&gt;
	 *	测试jdbcTemplate是否被正确的创建
	 *&lt;/pre&gt;
	 */
	@Test
	public void testJdbcTemplate() {
		System.out.println("jdbcTemplate:"+jdbcTemplate);
		assertTrue(jdbcTemplate != null);
	}
	
	@Test
	public void testTableTest() {
		Object[] args = { 1 };
		String name = jdbcTemplate.queryForObject(
				"select name from test where id= ?", args, String.class);
		System.out.println("=======&gt;name:" + name);

		assertEquals("Hello World", name);
	}

	@Test
	public void testTableUser() {
		Object[] args = { 1 };
		int age = jdbcTemplate.queryForObject(
				"select age from user where id= ?", args, Integer.class).intValue();
		System.out.println("=======&gt;age:" + age);

		assertEquals(1, age);
	}
	@Test
	public void testTableUserLike() {
		Object[] args = { "%Hello World%" };
		int count = jdbcTemplate.queryForObject(
				"select count(1) from user where name like ?", args, Integer.class).intValue();
		System.out.println("=======&gt;count:" + count);
		
		assertEquals(60, count);
	}
	@Test
	public void testTableUserObject() {
		
		Object[] args = { "%Hello World%" };
		List&lt;String&gt; list = jdbcTemplate.query(
				"select * from user where name like ?", args, new RowMapper&lt;String&gt;(){

					@Override
					public String mapRow(ResultSet rs, int rowNum)
							throws SQLException {
						return rs.getString("name");
					}});
		System.out.println("=======&gt;list:" + list);
		
		assertEquals(60, list.size());
	}

	@After
	public void tearDown() {
		//do nothing
	}

}</pre> 
 <p>&nbsp;</p> 
 <p>DataAccessUnitTestTemplateForH2Test.java 在maven项目中的全路径如下：</p> 
 <pre name="code" class="java">src/test/java/org/kanpiaoxue/test/h2/DataAccessUnitTestTemplateForH2Test.java</pre> 
 <p>&nbsp;运行maven命令： mvn clean test</p> 
 <p>结果如下：</p> 
 <pre name="code" class="java">E:\workspace_study\testAll&gt;mvn clean test
[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building testAll 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO]
[INFO] --- maven-clean-plugin:2.4.1:clean (default-clean) @ testAll ---
[INFO] Deleting E:\workspace_study\testAll\target
[INFO]
[INFO] --- maven-resources-plugin:2.5:resources (default-resources) @ testAll ---
[debug] execute contextualize
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 4 resources
[INFO]
[INFO] --- maven-compiler-plugin:2.3.2:compile (default-compile) @ testAll ---
[INFO] Compiling 40 source files to E:\workspace_study\testAll\target\classes
[INFO]
[INFO] --- maven-resources-plugin:2.5:testResources (default-testResources) @ testAll ---
[debug] execute contextualize
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 3 resources
[INFO]
[INFO] --- maven-compiler-plugin:2.3.2:testCompile (default-testCompile) @ testAll ---
[INFO] Compiling 1 source file to E:\workspace_study\testAll\target\test-classes
[INFO]
[INFO] --- maven-surefire-plugin:2.10:test (default-test) @ testAll ---
[INFO] Surefire report directory: E:\workspace_study\testAll\target\surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running org.kanpiaoxue.test.h2.DataAccessUnitTestTemplateForH2Test
log4j: reset attribute= "false".
log4j: Threshold ="null".
log4j: Retreiving an instance of org.apache.log4j.Logger.
log4j: Setting [org.springframework] additivity to [true].
log4j: Level value for org.springframework is  [ERROR].
log4j: org.springframework level set to ERROR
log4j: Class name: [org.apache.log4j.ConsoleAppender]
log4j: Parsing layout of class: "org.apache.log4j.PatternLayout"
log4j: Setting property [conversionPattern] to [%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %p %.200l %x --&gt; %m%n].
log4j: Adding appender named [console] to category [org.springframework].
log4j: Class name: [org.apache.log4j.DailyRollingFileAppender]
log4j: Setting property [file] to [/logs/testAll.log].
log4j: Setting property [datePattern] to ['.'yyyy-MM-dd'.log'].
log4j: Parsing layout of class: "org.apache.log4j.PatternLayout"
log4j: Setting property [conversionPattern] to [%d{yyyy-MM-dd HH:mm:ss.SSS} [%t] %p %.200l %x --&gt; %m%n].
log4j: setFile called: /logs/testAll.log, true
log4j: setFile ended
log4j: Appender [dailyFile] to be rolled at midnight.
log4j: Adding appender named [dailyFile] to category [org.springframework].
log4j: Retreiving an instance of org.apache.log4j.Logger.
log4j: Setting [org.quartz] additivity to [true].
log4j: Level value for org.quartz is  [ERROR].
log4j: org.quartz level set to ERROR
log4j: Adding appender named [console] to category [org.quartz].
log4j: Adding appender named [dailyFile] to category [org.quartz].
log4j: Retreiving an instance of org.apache.log4j.Logger.
log4j: Setting [com.wanmei] additivity to [true].
log4j: Level value for com.wanmei is  [info].
log4j: com.wanmei level set to INFO
log4j: Adding appender named [console] to category [com.wanmei].
log4j: Adding appender named [dailyFile] to category [com.wanmei].
log4j: Retreiving an instance of org.apache.log4j.Logger.
log4j: Setting [java.lang] additivity to [true].
log4j: Level value for java.lang is  [ERROR].
log4j: java.lang level set to ERROR
log4j: Adding appender named [console] to category [java.lang].
log4j: Adding appender named [dailyFile] to category [java.lang].
log4j: Retreiving an instance of org.apache.log4j.Logger.
log4j: Setting [org.apache] additivity to [true].
log4j: Level value for org.apache is  [ERROR].
log4j: org.apache level set to ERROR
log4j: Adding appender named [console] to category [org.apache].
log4j: Adding appender named [dailyFile] to category [org.apache].
=======&gt;name:Hello World
=======&gt;age:1
=======&gt;count:60
jdbcTemplate:org.springframework.jdbc.core.JdbcTemplate@416b47f
=======&gt;list:[Hello World01, Hello World02, Hello World03, Hello World04, Hello World05, Hello World06, Hello World07, Hello World08, Hello World09, Hello World10, Hello World11, Hello World12, Hello World13, Hello World14, Hello
 World15, Hello World16, Hello World17, Hello World18, Hello World19, Hello World20, Hello World21, Hello World22, Hello World23, Hello World24, Hello World25, Hello World26, Hello World27, Hello World28, Hello World29, Hello Wor
ld30, Hello World31, Hello World32, Hello World33, Hello World34, Hello World35, Hello World36, Hello World37, Hello World38, Hello World39, Hello World40, Hello World41, Hello World42, Hello World43, Hello World44, Hello World45
, Hello World46, Hello World47, Hello World48, Hello World49, Hello World50, Hello World51, Hello World52, Hello World53, Hello World54, Hello World55, Hello World56, Hello World, Hello World, Hello World, Hello World]
Tests run: 5, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.883 sec

Results :

Tests run: 5, Failures: 0, Errors: 0, Skipped: 0

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.129s
[INFO] Finished at: Mon Jan 13 17:34:52 CST 2014
[INFO] Final Memory: 21M/227M
[INFO] ------------------------------------------------------------------------</pre> 
 <p>&nbsp;pom.xml 如下：</p> 
 <pre name="code" class="xml">&lt;project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"&gt;
	&lt;modelVersion&gt;4.0.0&lt;/modelVersion&gt;

	&lt;groupId&gt;org.kanpiaoxue.test&lt;/groupId&gt;
	&lt;artifactId&gt;testAll&lt;/artifactId&gt;
	&lt;version&gt;0.0.1-SNAPSHOT&lt;/version&gt;
	&lt;packaging&gt;jar&lt;/packaging&gt;

	&lt;name&gt;testAll&lt;/name&gt;

	&lt;properties&gt;
		&lt;project.build.sourceEncoding&gt;UTF-8&lt;/project.build.sourceEncoding&gt;
		&lt;spring.version&gt;3.2.6.RELEASE&lt;/spring.version&gt;
	&lt;/properties&gt;

	&lt;dependencies&gt;

		&lt;!-- database h2 start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.h2database&lt;/groupId&gt;
			&lt;artifactId&gt;h2&lt;/artifactId&gt;
			&lt;version&gt;1.3.174&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- database h2 end --&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;com.google.guava&lt;/groupId&gt;
			&lt;artifactId&gt;guava&lt;/artifactId&gt;
			&lt;version&gt;15.0&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- test start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;junit&lt;/groupId&gt;
			&lt;artifactId&gt;junit&lt;/artifactId&gt;
			&lt;version&gt;4.11&lt;/version&gt;
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
			&lt;version&gt;2.4&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.apache.commons&lt;/groupId&gt;
			&lt;artifactId&gt;commons-lang3&lt;/artifactId&gt;
			&lt;version&gt;3.1&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt;commons-pool&lt;/groupId&gt;
			&lt;artifactId&gt;commons-pool&lt;/artifactId&gt;
			&lt;version&gt;1.6&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;!-- commons end --&gt;


		&lt;!-- log start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;commons-logging&lt;/groupId&gt;
			&lt;artifactId&gt;commons-logging&lt;/artifactId&gt;
			&lt;version&gt;1.1.3&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.apache.directory.studio&lt;/groupId&gt;
			&lt;artifactId&gt;org.apache.logging.log4j&lt;/artifactId&gt;
			&lt;version&gt;1.2.17&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- slf4j start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
			&lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
			&lt;version&gt;1.7.5&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
			&lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;
			&lt;version&gt;1.7.5&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- slf4j end --&gt;
		&lt;!-- log end --&gt;


		&lt;!-- json start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.alibaba&lt;/groupId&gt;
			&lt;artifactId&gt;fastjson&lt;/artifactId&gt;
			&lt;version&gt;1.1.22&lt;/version&gt;
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
			&lt;version&gt;2.2.1&lt;/version&gt;
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
			&lt;version&gt;3.8.0.Final&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- netty end --&gt;


		&lt;!-- 2D code start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.google.zxing&lt;/groupId&gt;
			&lt;artifactId&gt;core&lt;/artifactId&gt;
			&lt;version&gt;2.2&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.google.zxing&lt;/groupId&gt;
			&lt;artifactId&gt;javase&lt;/artifactId&gt;
			&lt;version&gt;2.2&lt;/version&gt;
		&lt;/dependency&gt;
		&lt;!-- 2D code end --&gt;

		&lt;!-- spring start --&gt;
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
			&lt;artifactId&gt;spring-context&lt;/artifactId&gt;
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
		&lt;!-- spring end --&gt;
	&lt;/dependencies&gt;
&lt;/project&gt;
</pre> 
 <p>&nbsp;</p> 
</div>