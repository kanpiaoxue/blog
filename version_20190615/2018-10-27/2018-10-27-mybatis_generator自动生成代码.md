#mybatis generator自动生成代码
###发表时间：2018-10-27
###分类：java,mybatis,eclipse,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2432838" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2432838</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>generatorConfig.xml</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;!DOCTYPE generatorConfiguration PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN" "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd"&gt;
&lt;generatorConfiguration&gt;

	&lt;classPathEntry
		location="/Users/kanpiaoxue/develop_tools/maven/maven_repository/mysql/mysql-connector-java/5.1.47/mysql-connector-java-5.1.47.jar" /&gt;

	&lt;context id="context1"&gt;
		&lt;property name="javaFileEncoding" value="UTF-8" /&gt;
		
		&lt;!-- 将下面的 com.example.work.mybatisgenerator.MyCommentGenerator 放在 classpath即可使用 --&gt;
		&lt;commentGenerator type="com.example.work.mybatisgenerator.MyCommentGenerator"&gt;
			&lt;property name="suppressAllComments" value="false" /&gt;
		&lt;/commentGenerator&gt;

		&lt;jdbcConnection
			connectionURL="jdbc:mysql://127.0.0.1:3306/beidou"
			driverClass="com.mysql.jdbc.Driver" password="root"
			userId="root" /&gt;

		&lt;javaTypeResolver&gt;
			&lt;property name="forceBigDecimals" value="false" /&gt;
		&lt;/javaTypeResolver&gt;


		&lt;!-- model package and location --&gt;
		&lt;javaModelGenerator targetPackage="org.kanpiaoxuie.beidou.commons.bean.entity"
			targetProject="work/src/main/java"&gt;
			&lt;property name="enableSubPackages" value="true" /&gt;
			&lt;property name="trimStrings" value="true" /&gt;
		&lt;/javaModelGenerator&gt;
		&lt;!-- mapping package and location --&gt;
		&lt;sqlMapGenerator targetPackage="org.kanpiaoxuie.beidou.dao.mapper"
			targetProject="work/src/main/java"&gt;
			&lt;property name="enableSubPackages" value="true" /&gt;
		&lt;/sqlMapGenerator&gt;
		&lt;!-- dao package and location --&gt;
		&lt;javaClientGenerator type="XMLMAPPER"
			targetPackage="org.kanpiaoxuie.beidou.dao"
			targetProject="work/src/main/java"&gt;
			&lt;property name="enableSubPackages" value="true" /&gt;
		&lt;/javaClientGenerator&gt;



		&lt;table tableName="tb_task" domainObjectName="Task" mapperName="TaskDAO"
			enableCountByExample="false" enableUpdateByExample="false"
			enableDeleteByExample="false" enableSelectByExample="false"
			selectByExampleQueryId="false" /&gt;


	&lt;/context&gt;
&lt;/generatorConfiguration&gt;</pre> 
 <p class="p1"><span class="s1">&nbsp;<br></span></p> 
 <p>&nbsp;需要在pom.xml 中添加如下依赖进行扩展：</p> 
 <pre name="code" class="xml">&lt;!-- https://mvnrepository.com/artifact/org.mybatis.generator/mybatis-generator-core --&gt;
&lt;dependency&gt;
 &lt;groupId&gt;org.mybatis.generator&lt;/groupId&gt;
 &lt;artifactId&gt;mybatis-generator-core&lt;/artifactId&gt;
 &lt;version&gt;1.3.7&lt;/version&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/**
 * Copyright kanpiaoxue.org [2017-2018]
 */
package com.example.work.mybatisgenerator;

import static org.mybatis.generator.internal.util.StringUtility.isTrue;

import org.mybatis.generator.api.CommentGenerator;
import org.mybatis.generator.api.IntrospectedColumn;
import org.mybatis.generator.api.IntrospectedTable;
import org.mybatis.generator.api.dom.java.CompilationUnit;
import org.mybatis.generator.api.dom.java.Field;
import org.mybatis.generator.api.dom.java.FullyQualifiedJavaType;
import org.mybatis.generator.api.dom.java.InnerClass;
import org.mybatis.generator.api.dom.java.InnerEnum;
import org.mybatis.generator.api.dom.java.JavaElement;
import org.mybatis.generator.api.dom.java.Method;
import org.mybatis.generator.api.dom.java.Parameter;
import org.mybatis.generator.api.dom.java.TopLevelClass;
import org.mybatis.generator.api.dom.xml.XmlElement;
import org.mybatis.generator.config.PropertyRegistry;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Properties;
import java.util.Set;

/**
 * MyCommentGenerator.java
 * 
 * @author kanpiaoxue
 * @version 1.0
 *          Create Time 2018年10月27日 下午8:37:40
 *          Description :
 */
public class MyCommentGenerator implements CommentGenerator {
    private Properties properties;
    private Properties systemPro;
    private boolean suppressDate;
    private boolean suppressAllComments;
    private String currentDateStr;

    public MyCommentGenerator() {
        super();
        properties = new Properties();
        systemPro = System.getProperties();
        suppressDate = false;
        suppressAllComments = false;
        currentDateStr = (new SimpleDateFormat("yyyy-MM-dd")).format(new Date());
    }

    public void addJavaFileComment(CompilationUnit compilationUnit) {
        // add no file level comments by default
        return;
    }

    /**
     * Adds a suitable comment to warn users that the element was generated, and
     * when it was generated.
     */
    public void addComment(XmlElement xmlElement) {
        return;
    }

    public void addRootComment(XmlElement rootElement) {
        // add no document level comments by default
        return;
    }

    public void addConfigurationProperties(Properties properties) {
        this.properties.putAll(properties);
        suppressDate = isTrue(properties.getProperty(PropertyRegistry.COMMENT_GENERATOR_SUPPRESS_DATE));
        suppressAllComments =
                isTrue(properties.getProperty(PropertyRegistry.COMMENT_GENERATOR_SUPPRESS_ALL_COMMENTS));
    }

    /**
     * This method adds the custom javadoc tag for. You may do nothing if you do
     * not wish to include the Javadoc tag - however, if you do not include the
     * Javadoc tag then the Java merge capability of the eclipse plugin will
     * break.
     * 
     * @param javaElement
     *            the java element
     */
    protected void addJavadocTag(JavaElement javaElement, boolean markAsDoNotDelete) {
        return;
    }

    /**
     * This method returns a formated date string to include in the Javadoc tag
     * and XML comments. You may return null if you do not want the date in
     * these documentation elements.
     * 
     * @return a string representing the current timestamp, or null
     */
    protected String getDateString() {
        String result = null;
        if (!suppressDate) {
            result = currentDateStr;
        }
        return result;
    }

    public void addClassComment(InnerClass innerClass, IntrospectedTable introspectedTable) {
        if (suppressAllComments) {
            return;
        }
        StringBuilder sb = new StringBuilder();
        innerClass.addJavaDocLine("/**");
        sb.append(" * ");
        sb.append(introspectedTable.getFullyQualifiedTable());
        sb.append(" ");
        sb.append(getDateString());
        innerClass.addJavaDocLine(sb.toString().replace("\n", " "));
        innerClass.addJavaDocLine(" */");
    }

    public void addEnumComment(InnerEnum innerEnum, IntrospectedTable introspectedTable) {
        if (suppressAllComments) {
            return;
        }
        StringBuilder sb = new StringBuilder();
        innerEnum.addJavaDocLine("/**");
        sb.append(" * ");
        sb.append(introspectedTable.getFullyQualifiedTable());
        innerEnum.addJavaDocLine(sb.toString().replace("\n", " "));
        innerEnum.addJavaDocLine(" */");
    }

    public void addFieldComment(Field field, IntrospectedTable introspectedTable,
            IntrospectedColumn introspectedColumn) {
        if (suppressAllComments) {
            return;
        }
        StringBuilder sb = new StringBuilder();
        field.addJavaDocLine("/**");
        sb.append(" * ");
        sb.append(introspectedColumn.getRemarks());
        field.addJavaDocLine(sb.toString().replace("\n", " "));
        field.addJavaDocLine(" */");
    }

    public void addFieldComment(Field field, IntrospectedTable introspectedTable) {
        if (suppressAllComments) {
            return;
        }
        StringBuilder sb = new StringBuilder();
        field.addJavaDocLine("/**");
        sb.append(" * ");
        sb.append(introspectedTable.getFullyQualifiedTable());
        field.addJavaDocLine(sb.toString().replace("\n", " "));
        field.addJavaDocLine(" */");
    }

    public void addGeneralMethodComment(Method method, IntrospectedTable introspectedTable) {
        if (suppressAllComments) {
            return;
        }
        String methodName = method.getName();
        String nameDoc = "";
        if ("deleteByPrimaryKey".equals(methodName)) {
            nameDoc = "根据主键删除记录";
        } else if ("insert".equals(methodName)) {
            nameDoc = "新增记录";
        } else if ("insertSelective".equals(methodName)) {
            nameDoc = "根据字段新增记录";
        } else if ("selectByPrimaryKey".equals(methodName)) {
            nameDoc = "根据主键得到记录";

        } else if ("updateByPrimaryKeySelective".equals(methodName)) {
            nameDoc = "根据字段使用主键更新记录";

        } else if ("updateByPrimaryKey".equals(methodName)) {
            nameDoc = "使用主键更新记录";

        } else {
            nameDoc = "";

        }

        method.addJavaDocLine("/**");
        StringBuilder sb = new StringBuilder();
        sb.append(" *\n");
        sb.append(" * ");
        sb.append(nameDoc).append("\n");
        method.addJavaDocLine(sb.toString());

        StringBuilder sb1 = new StringBuilder();
        for (Parameter parm : method.getParameters()) {
            sb1.append(" * @param ");
            sb1.append(parm.getName());
            sb1.append(" ");
            method.addJavaDocLine(sb1.toString().replace("\n", " "));
        }
        StringBuilder sb2 = new StringBuilder();
        sb2.append(" * @return 影响记录数量");
        method.addJavaDocLine(sb2.toString());
        method.addJavaDocLine(" */");
    }

    public void addGetterComment(Method method, IntrospectedTable introspectedTable,
            IntrospectedColumn introspectedColumn) {
        if (suppressAllComments) {
            return;
        }
        method.addJavaDocLine("/**");
        StringBuilder sb = new StringBuilder();
        sb.append(" * ");
        sb.append(introspectedColumn.getRemarks());
        method.addJavaDocLine(sb.toString().replace("\n", " "));
        sb.setLength(0);
        sb.append(" * @return ");
        sb.append(introspectedColumn.getActualColumnName());
        sb.append(" ");
        sb.append(introspectedColumn.getRemarks());
        method.addJavaDocLine(sb.toString().replace("\n", " "));
        method.addJavaDocLine(" */");
    }

    public void addSetterComment(Method method, IntrospectedTable introspectedTable,
            IntrospectedColumn introspectedColumn) {
        if (suppressAllComments) {
            return;
        }
        method.addJavaDocLine("/**");
        StringBuilder sb = new StringBuilder();
        sb.append(" * ");
        sb.append(introspectedColumn.getRemarks());
        method.addJavaDocLine(sb.toString().replace("\n", " "));
        Parameter parm = method.getParameters().get(0);
        sb.setLength(0);
        sb.append(" * @param ");
        sb.append(parm.getName());
        sb.append(" ");
        sb.append(introspectedColumn.getRemarks());
        method.addJavaDocLine(sb.toString().replace("\n", " "));
        method.addJavaDocLine(" */");
    }

    public void addClassComment(InnerClass innerClass, IntrospectedTable introspectedTable,
            boolean markAsDoNotDelete) {
        if (suppressAllComments) {
            return;
        }
        StringBuilder sb = new StringBuilder();
        innerClass.addJavaDocLine("/**");
        sb.append(" * ");
        sb.append(introspectedTable.getFullyQualifiedTable());
        innerClass.addJavaDocLine(sb.toString().replace("\n", " "));
        sb.setLength(0);
        sb.append(" * @author ");
        sb.append(systemPro.getProperty("user.name"));
        sb.append(" ");
        sb.append(currentDateStr);
        innerClass.addJavaDocLine(" */");
    }

    /*
     * (non-Javadoc)
     * @see org.mybatis.generator.api.CommentGenerator#addModelClassComment(org.
     * mybatis.generator.api.dom.java.TopLevelClass,
     * org.mybatis.generator.api.IntrospectedTable)
     */
    @Override
    public void addModelClassComment(TopLevelClass topLevelClass, IntrospectedTable introspectedTable) {

        if (suppressAllComments) {
            return;
        }
        topLevelClass.addJavaDocLine("/**");
        StringBuilder sb = new StringBuilder();
        sb.append(" * 数据表: ");
        sb.append(introspectedTable.getFullyQualifiedTable());
        topLevelClass.addJavaDocLine(sb.toString().replace("\n", " "));
        topLevelClass.addJavaDocLine(" */");

    }

    /*
     * (non-Javadoc)
     * @see
     * org.mybatis.generator.api.CommentGenerator#addGeneralMethodAnnotation(org
     * .mybatis.generator.api.dom.java.Method,
     * org.mybatis.generator.api.IntrospectedTable, java.util.Set)
     */
    @Override
    public void addGeneralMethodAnnotation(Method method, IntrospectedTable introspectedTable,
            Set&lt;FullyQualifiedJavaType&gt; imports) {

    }

    /*
     * (non-Javadoc)
     * @see
     * org.mybatis.generator.api.CommentGenerator#addGeneralMethodAnnotation(org
     * .mybatis.generator.api.dom.java.Method,
     * org.mybatis.generator.api.IntrospectedTable,
     * org.mybatis.generator.api.IntrospectedColumn, java.util.Set)
     */
    @Override
    public void addGeneralMethodAnnotation(Method method, IntrospectedTable introspectedTable,
            IntrospectedColumn introspectedColumn, Set&lt;FullyQualifiedJavaType&gt; imports) {

    }

    /*
     * (non-Javadoc)
     * @see
     * org.mybatis.generator.api.CommentGenerator#addFieldAnnotation(org.mybatis
     * .generator.api.dom.java.Field,
     * org.mybatis.generator.api.IntrospectedTable, java.util.Set)
     */
    @Override
    public void addFieldAnnotation(Field field, IntrospectedTable introspectedTable,
            Set&lt;FullyQualifiedJavaType&gt; imports) {

    }

    /*
     * (non-Javadoc)
     * @see
     * org.mybatis.generator.api.CommentGenerator#addFieldAnnotation(org.mybatis
     * .generator.api.dom.java.Field,
     * org.mybatis.generator.api.IntrospectedTable,
     * org.mybatis.generator.api.IntrospectedColumn, java.util.Set)
     */
    @Override
    public void addFieldAnnotation(Field field, IntrospectedTable introspectedTable,
            IntrospectedColumn introspectedColumn, Set&lt;FullyQualifiedJavaType&gt; imports) {

    }

    /*
     * (non-Javadoc)
     * @see
     * org.mybatis.generator.api.CommentGenerator#addClassAnnotation(org.mybatis
     * .generator.api.dom.java.InnerClass,
     * org.mybatis.generator.api.IntrospectedTable, java.util.Set)
     */
    @Override
    public void addClassAnnotation(InnerClass innerClass, IntrospectedTable introspectedTable,
            Set&lt;FullyQualifiedJavaType&gt; imports) {

    }
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>