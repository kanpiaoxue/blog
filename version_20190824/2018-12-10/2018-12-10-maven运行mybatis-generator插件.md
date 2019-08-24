#maven运行mybatis-generator插件
###发表时间：2018-12-10
###分类：maven,mybatis,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434996" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434996</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>1、配置pom.xml里面的mybatis-generator插件</p> 
 <pre name="code" class="java">&lt;plugin&gt;
    &lt;groupId&gt;org.mybatis.generator&lt;/groupId&gt;
    &lt;artifactId&gt;mybatis-generator-maven-plugin&lt;/artifactId&gt;
    &lt;version&gt;1.3.7&lt;/version&gt;
    &lt;executions&gt;
        &lt;execution&gt;
            &lt;id&gt;Generate MyBatis Files&lt;/id&gt;
            &lt;goals&gt;
                &lt;goal&gt;generate&lt;/goal&gt;
            &lt;/goals&gt;
            &lt;phase&gt;generate&lt;/phase&gt;
            &lt;configuration&gt;
                &lt;verbose&gt;true&lt;/verbose&gt;
                &lt;overwrite&gt;true&lt;/overwrite&gt;
            &lt;/configuration&gt;
        &lt;/execution&gt;
    &lt;/executions&gt;
    &lt;dependencies&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;mysql&lt;/groupId&gt;
            &lt;artifactId&gt;mysql-connector-java&lt;/artifactId&gt;
            &lt;version&gt;5.1.27&lt;/version&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.mybatis.generator&lt;/groupId&gt;
            &lt;artifactId&gt;mybatis-generator-core&lt;/artifactId&gt;
            &lt;version&gt;1.3.7&lt;/version&gt;
        &lt;/dependency&gt;
        &lt;dependency&gt;
            &lt;groupId&gt;org.mybatis&lt;/groupId&gt;
            &lt;artifactId&gt;mybatis&lt;/artifactId&gt;
            &lt;version&gt;3.4.2&lt;/version&gt;
        &lt;/dependency&gt;
    &lt;/dependencies&gt;
    &lt;configuration&gt;
        &lt;!--配置文件的路径 --&gt;
        &lt;configurationFile&gt;${basedir}/src/main/java/org/kanpiaoxue/testproject/mybatis/generatorConfig.xml&lt;/configurationFile&gt;
        &lt;verbose&gt;true&lt;/verbose&gt;
        &lt;overwrite&gt;true&lt;/overwrite&gt;
    &lt;/configuration&gt;
&lt;/plugin&gt; </pre> 
 <p>&nbsp;</p> 
 <p>2、generatorConfig.xml</p> 
 <pre name="code" class="java">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd"&gt;
&lt;generatorConfiguration&gt;

    &lt;!-- 
        这个文件有两个地方需要注意下：
           I）：targetProject 如果是eclipse插件则只需要配置工程名 work，但用maven插件则不行必须用绝对路径:/work/src/main/java，
                否则会提醒 The specified target project directory pluto-is-server does not exist
           II）：如果生成的文件乱码或者GBK时，则只需要加 &lt;property name="javaFileEncoding" value="UTF-8"/&gt; 
    --&gt;

    &lt;!-- 引入配置文件 --&gt;
    &lt;!-- &lt;properties resource="init.properties" /&gt; --&gt;

    &lt;!-- 指定数据连接驱动jar地址 --&gt;
    &lt;classPathEntry location="/maven_repository/mysql/mysql-connector-java/5.1.27/mysql-connector-java-5.1.27.jar" /&gt;

    &lt;!-- 一个数据库一个context --&gt;
    &lt;context id="testdb"&gt;
        &lt;!-- 注释 --&gt;
        &lt;commentGenerator&gt;
            &lt;!-- 抑制警告 --&gt;
            &lt;property name="suppressTypeWarnings" value="true" /&gt;
            &lt;!-- 是否取消注释 --&gt;
            &lt;property name="suppressAllComments" value="true" /&gt;
            &lt;!-- 是否生成注释代时间戳 --&gt;
            &lt;property name="suppressDate" value="true" /&gt;
        &lt;/commentGenerator&gt;

        &lt;!-- jdbc连接 --&gt;
        &lt;jdbcConnection driverClass="com.mysql.jdbc.Driver"
            connectionURL="jdbc:mysql://localhost:3306/testdb" userId="root" password="root" /&gt;

        &lt;!-- 类型转换 --&gt;
        &lt;javaTypeResolver&gt;
            &lt;!-- 是否使用bigDecimal， false可自动转化以下类型（Long, Integer, Short, etc.） --&gt;
            &lt;property name="forceBigDecimals" value="false" /&gt;
        &lt;/javaTypeResolver&gt;

        &lt;!-- 生成实体类地址 --&gt;
        &lt;javaModelGenerator targetPackage="org.kanpiaoxue.test.testdb_commons.bean"
            targetProject="/work/src/main/java"&gt;
            &lt;!-- 是否在当前路径下新加一层--&gt;
            &lt;property name="enableSubPackages" value="false" /&gt;
            &lt;!-- 是否针对string类型的字段在set的时候进行trim调用 --&gt;
            &lt;property name="trimStrings" value="true" /&gt;
        &lt;/javaModelGenerator&gt;

        &lt;!-- 生成mapxml文件 --&gt;
        &lt;sqlMapGenerator targetPackage="org.kanpiaoxue.test.testdb_commons.mapper"
            targetProject="/work/src/main/java"&gt;
            &lt;!-- 是否在当前路径下新加一层--&gt;
            &lt;property name="enableSubPackages" value="false" /&gt;
        &lt;/sqlMapGenerator&gt;

        &lt;!-- 生成mapxml对应client，也就是接口dao --&gt;
        &lt;javaClientGenerator targetPackage="org.kanpiaoxue.test.testdb_dao.dao"
            targetProject="/work/src/main/java" type="XMLMAPPER"&gt;
            &lt;!-- 是否在当前路径下新加一层--&gt;
            &lt;property name="enableSubPackages" value="false" /&gt;
        &lt;/javaClientGenerator&gt;

        &lt;table schema="testdb" tableName="tb_hello" mapperName="HelloDAO"
            domainObjectName="Hello" enableCountByExample="false"
            enableDeleteByExample="false" enableSelectByExample="false"
            enableUpdateByExample="false"&gt;
            &lt;property name="useActualColumnNames" value="false" /&gt;
        &lt;/table&gt;


    &lt;/context&gt;
&lt;/generatorConfiguration&gt; </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;3、命令行运行maven命令：</p> 
 <pre name="code" class="java">mvn clean mybatis-generator:generate</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>