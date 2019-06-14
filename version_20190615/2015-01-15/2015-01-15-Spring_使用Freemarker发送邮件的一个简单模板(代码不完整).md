#Spring 使用Freemarker发送邮件的一个简单模板（代码不完整）
###发表时间：2015-01-15
###分类：Freemarker,mail
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2176342" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2176342</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>下面是一个使用过的Freemarker的模板，可以作为参考（代码不完整）。附件就是它的源文件。</p> 
 <p>dmap-alarm-template-mail.ftl</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="html">&lt;!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd"&gt;
&lt;html xmlns="http://www.w3.org/1999/xhtml"&gt;
&lt;head&gt;
		&lt;meta http-equiv="Content-Type" content="text/html; charset=utf-8" /&gt;
		&lt;title&gt;报警邮件&lt;/title&gt;
&lt;style&gt;
*{
	font-size: 12px;
}
.mailTitle{
	text-align: center;
	margin-top: 25px;
}
.mailBody{
	margin: 25 25 25 25;
}
.mailTitleTaskName{
	font-size: 16px;
	color: red;
	font-weight: bolder;
}
.mailTitleErrorMessage{
	font-size: 16px;
	color: red;
	font-weight: bolder;	
}
table{margin-left:25px; margin-top:10px; width:95%; border:1px blue solid;}
td{ border:1px solid #cccccc;padding:5px 5px 5px 5px;}
caption{
	background-color: rgb(95,175,17);
	font-weight: bold;
	padding-top: 5px;
	padding-bottom:5px;
}

.copyRight{text-align: center;font-size: 14px; font-weight:bold;color: silver;margin-top:10px;margin-bottom:25px;}
.firstRow{text-align: center;font-size: 14px;font-weight:bold;}
.run_other_state{color: blue;font-weight:bold;}
.run_wait_running{color: silver;font-weight:bold;}
.run_success{color: green;font-weight:bold;}
.run_failure{color: red;font-weight:bold;}
.current_first_column{width:30%;font-weight:bold;}
&lt;/style&gt;
&lt;/head&gt;
	&lt;body&gt;
		&lt;div class="mailTitle"&gt;
			&lt;div class="mailTitleTaskName"&gt;任务ID：${current_task_id}&lt;/div&gt;
			&lt;div&gt;数据版本：${current_dataversion_no}&lt;/div&gt;
			&lt;div class="mailTitleErrorMessage"&gt;${current_task_error_message}&lt;/div&gt;
		&lt;/div&gt;
		&lt;div class="mailBody"&gt;
			&lt;table&gt;
				&lt;caption&gt;任务信息&lt;/caption&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;任务ID&lt;/td&gt;
					&lt;td&gt;${current_task_id}&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;任务名称&lt;/td&gt;
					&lt;td&gt;${current_task_name}&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;数据版本最后更新时间&lt;/td&gt;
					&lt;td&gt;${current_dataversion_last_mofied}&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;所属团队&lt;/td&gt;
					&lt;td&gt;${current_task_team_name}&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;任务启动延迟时间点&lt;/td&gt;
					&lt;td&gt;${current_launched_timeout}&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;运行超时时间&lt;/td&gt;
					&lt;td&gt;${current_running_timeout}分钟&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;版本运行信息&lt;/td&gt;
					&lt;td&gt;
					&lt;textarea rows="5" style="width:100%;text-align:left;"&gt;${current_data_version_message!""}&lt;/textarea&gt;					
					&lt;/td&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;第一值班人&lt;/td&gt;
					&lt;#if current_task_duty_first??&gt;
						&lt;td&gt;${current_task_duty_first.name}(${current_task_duty_first.username},手机号码：${(current_task_duty_first.mobileNumber)!"无"},邮箱：&lt;a href="mailto:${current_task_duty_first.email}"&gt;${current_task_duty_first.email}&lt;/a&gt;)&lt;/td&gt;
					&lt;#else&gt;
						&lt;td&gt;无&lt;/td&gt;
					&lt;/#if&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;第二值班人&lt;/td&gt;
					&lt;#if current_task_duty_second??&gt;
						&lt;td&gt;${current_task_duty_second.name}(${current_task_duty_second.username},手机号码：${(current_task_duty_first.mobileNumber)!"无"},邮箱：&lt;a href="mailto:${current_task_duty_second.email}"&gt;${current_task_duty_second.email}&lt;/a&gt;)&lt;/td&gt;
					&lt;#else&gt;
						&lt;td&gt;无&lt;/td&gt;
					&lt;/#if&gt;
				&lt;/tr&gt;
				&lt;tr&gt;
					&lt;td class="current_first_column"&gt;直接下游任务数量(DOWN)&lt;/td&gt;
					&lt;td&gt;${current_task_down_stream_count}&lt;/td&gt;
				&lt;/tr&gt;
			&lt;/table&gt;

			&lt;#if down_stream_effect_map?exists&gt;
			&lt;#assign rowIndex = 0&gt;
				&lt;#assign mapsize = down_stream_effect_map?size&gt;
				&lt;#if (mapsize&gt;0)&gt;	
				&lt;table style="text-align: center;"&gt;
					&lt;caption&gt;当前任务的直接下游任务列表&lt;/caption&gt;
					&lt;tr class="firstRow"&gt;
						&lt;td&gt;#&lt;/td&gt;
						&lt;td&gt;任务类型&lt;/td&gt;
						&lt;td&gt;任务ID&lt;/td&gt;
						&lt;td&gt;任务名称&lt;/td&gt;
						&lt;td&gt;数据版本&lt;/td&gt;
						&lt;td&gt;所属团队&lt;/td&gt;
						&lt;td&gt;第一值班人&lt;/td&gt;
						&lt;td&gt;第二值班人&lt;/td&gt;
					&lt;/tr&gt;
						&lt;#list down_stream_effect_map?keys as key&gt;
							&lt;#assign ls = down_stream_effect_map[key]&gt;
							&lt;#assign rowspan = ls?size&gt;
							&lt;#list ls as object&gt;
								&lt;#assign rowIndex = rowIndex + 1&gt;
								&lt;tr&gt;
								&lt;td&gt;${rowIndex}&lt;/td&gt;
								&lt;#if object_index == 0&gt;
									&lt;td rowspan="${rowspan}"&gt;下游任务&lt;/td&gt;
									&lt;td rowspan="${rowspan}"&gt;${object.taskIdString}&lt;/td&gt;
									&lt;td rowspan="${rowspan}"&gt;${object.taskName}&lt;/td&gt;
								&lt;/#if&gt;
								&lt;td&gt;${object.dataVersionNo}&lt;/td&gt;
								&lt;#if object_index == 0&gt;
									&lt;td rowspan="${rowspan}"&gt;${object.teamName}&lt;/td&gt;
									&lt;#if object.firstUser??&gt;
										&lt;td rowspan="${rowspan}"&gt;${object.firstUser.name}(${object.firstUser.username},手机号码：${(object.firstUser.mobileNumber)!"无"},邮箱：&lt;a href="mailto:${object.firstUser.email}"&gt;${object.firstUser.email}&lt;/a&gt;)&lt;/td&gt;
									&lt;#else&gt;
										&lt;td rowspan="${rowspan}"&gt;无&lt;/td&gt;
									&lt;/#if&gt;
									&lt;#if object.secondUser??&gt;
										&lt;td rowspan="${rowspan}"&gt;${object.secondUser.name}(${object.secondUser.username},手机号码：${(object.secondUser.mobileNumber)!"无"},邮箱：&lt;a href="mailto:${object.secondUser.email}"&gt;${object.secondUser.email}&lt;/a&gt;)&lt;/td&gt;
									&lt;#else&gt;
										&lt;td rowspan="${rowspan}"&gt;无&lt;/td&gt;
									&lt;/#if&gt;
								&lt;/#if&gt;
							&lt;/tr&gt;																					
							&lt;/#list&gt;
						&lt;/#list&gt;					
				&lt;/table&gt;
			&lt;/#if&gt;
			&lt;/#if&gt;
			&lt;div class="copyRight"&gt;@Copyright: 运营产品研发部-CDC[2014.11-${current_year_month}]&lt;/div&gt;
		&lt;/div&gt;
	&lt;/body&gt;
&lt;/html&gt;</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.ui.freemarker.FreeMarkerTemplateUtils;
import org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer;

import freemarker.template.Template;

import java.util.Map;

public class TemplateEmailService {
    private FreeMarkerConfigurer freeMarkerConfigurer;
    private String fileName;
    public FreeMarkerConfigurer getFreeMarkerConfigurer() {
        return freeMarkerConfigurer;
    }

    // 通过模板构造邮件内容，参数username将替换模板文件中的${username}标签。
    public &lt;K, V&gt; String getMailText(Map&lt;K, V&gt; map) {
        String htmlText = "";
        try {
            // 通过指定模板名获取FreeMarker模板实例
            Template tpl = freeMarkerConfigurer.getConfiguration().getTemplate(
                    fileName);
            // FreeMarker通过Map传递动态数据
            // 解析模板并替换动态数据，最终username将替换模板文件中的${username}标签。
            htmlText = FreeMarkerTemplateUtils.processTemplateIntoString(tpl,
                    map);
        } catch (Exception e) {
            e.printStackTrace();
        }
        return htmlText;
    }

    public void setFreeMarkerConfigurer(
            FreeMarkerConfigurer freeMarkerConfigurer) {
        this.freeMarkerConfigurer = freeMarkerConfigurer;
    }

    public String getFileName() {
        return fileName;
    }

    public void setFileName(String fileName) {
        this.fileName = fileName;
    }
    
}
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8"?&gt;
&lt;beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:jdbc="http://www.springframework.org/schema/jdbc" xmlns:jee="http://www.springframework.org/schema/jee"
	xmlns:jms="http://www.springframework.org/schema/jms" xmlns:lang="http://www.springframework.org/schema/lang"
	xmlns:mvc="http://www.springframework.org/schema/mvc" xmlns:oxm="http://www.springframework.org/schema/oxm"
	xmlns:p="http://www.springframework.org/schema/p" xmlns:sec="http://www.springframework.org/schema/security"
	xmlns:task="http://www.springframework.org/schema/task" xmlns:tx="http://www.springframework.org/schema/tx"

	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.0.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd
		http://www.springframework.org/schema/jdbc http://www.springframework.org/schema/jdbc/spring-jdbc-4.0.xsd
		http://www.springframework.org/schema/jee http://www.springframework.org/schema/jee/spring-jee-4.0.xsd
		http://www.springframework.org/schema/jms http://www.springframework.org/schema/jms/spring-jms-4.0.xsd
		http://www.springframework.org/schema/lang http://www.springframework.org/schema/lang/spring-lang-4.0.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
		http://www.springframework.org/schema/oxm http://www.springframework.org/schema/oxm/spring-oxm-4.0.xsd
		http://www.springframework.org/schema/security http://www.springframework.org/schema/security/spring-security-4.0.xsd
		http://www.springframework.org/schema/task http://www.springframework.org/schema/task/spring-task-4.0.xsd
		http://www.springframework.org/schema/tx http://www.springframework.org/schema/tx/spring-tx-4.0.xsd"&gt;

	&lt;bean id="freeMarker"
		class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer"&gt;
		&lt;property name="templateLoaderPath" value="classpath:org/kanpiaoxue/test/freemarker" /&gt;&lt;!--指定模板文件目录 --&gt;
		&lt;property name="freemarkerSettings"&gt;&lt;!-- 设置FreeMarker环境属性 --&gt;
			&lt;props&gt;
				&lt;prop key="template_update_delay"&gt;1800&lt;/prop&gt;&lt;!--刷新模板的周期，单位为秒 --&gt;
				&lt;prop key="default_encoding"&gt;UTF-8&lt;/prop&gt;&lt;!--模板的编码格式 --&gt;
				&lt;prop key="locale"&gt;zh_CN&lt;/prop&gt;&lt;!-- 本地化设置 --&gt;
			&lt;/props&gt;
		&lt;/property&gt;
	&lt;/bean&gt;
	&lt;bean id="templateEmail" class="org.kanpiaoxue.test.freemarker.TemplateEmailService"&gt;
		&lt;property name="freeMarkerConfigurer" ref="freeMarker"&gt;&lt;/property&gt;
	&lt;/bean&gt;
&lt;/beans&gt;
</pre> 
 <p>&nbsp;main 函数的部分代码：</p> 
 <pre name="code" class="java">    private static final String CURRENT_TASK_ID = "current_task_id";
    private static final String CURRENT_TASK_NAME = "current_task_name";
    private static final String CURRENT_TASK_TEAM_NAME = "current_task_team_name";
    private static final String CURRENT_TASK_ERROR_MESSAGE = "current_task_error_message";
    private static final String CURRENT_TASK_DUTY_FIRST = "current_task_duty_first";
    private static final String CURRENT_TASK_DUTY_SECOND = "current_task_duty_second";
    private static final String CURRENT_TASK_DOWN_STREAM_COUNT = "current_task_down_stream_count";
    private static final String CURRENT_DATAVERSION_NO = "current_dataversion_no";
    private static final String CURRENT_DATAVERSION_LAST_MOFIED = "current_dataversion_last_mofied";
    private static final String CURRENT_LAUNCHED_TIMEOUT = "current_launched_timeout";
    private static final String CURRENT_RUNNING_TIMEOUT = "current_running_timeout";
    private static final String DOWN_STREAM_EFFECT_MAP = "down_stream_effect_map";
    private static final String CURRENT_YEAR_MONTH = "current_year_month";
    private static final String CURRENT_DATA_VERSION_MESSAGE = "current_data_version_message";     

 String message = "当前任务运行失败，是由于执行脚本错误：echo 'hello' ,exist code: 1";
        Map&lt;String, Object&gt; map = Maps.newHashMap();
        map.put(CURRENT_TASK_ID, taskId);
        map.put(CURRENT_TASK_NAME, taskName);
        map.put(CURRENT_TASK_TEAM_NAME, teamName);
        map.put(CURRENT_TASK_ERROR_MESSAGE, title);
        map.put(CURRENT_DATAVERSION_NO, dataVersion);
        map.put(CURRENT_DATAVERSION_LAST_MOFIED, lastModifiedTime);
        map.put(CURRENT_TASK_DUTY_FIRST, firstDutyDetail);
        map.put(CURRENT_TASK_DUTY_SECOND, secondDutyDetail);
        map.put(CURRENT_TASK_DOWN_STREAM_COUNT, downstreamCount);
        map.put(CURRENT_LAUNCHED_TIMEOUT, launchedTimeoutString);
        map.put(CURRENT_RUNNING_TIMEOUT, runingTimeout);
        map.put(DOWN_STREAM_EFFECT_MAP, downStreamEffecMap);
        map.put(CURRENT_DATA_VERSION_MESSAGE, message);
        map.put(CURRENT_YEAR_MONTH, DateTime.now().toString("yyyy.MM"));
        String html = template.getMailText(map);

        System.out.println(html);</pre> 
 <p>&nbsp;</p> 
</div>