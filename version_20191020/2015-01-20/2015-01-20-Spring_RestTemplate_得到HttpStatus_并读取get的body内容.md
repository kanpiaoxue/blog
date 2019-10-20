#Spring RestTemplate 得到HttpStatus，并读取get的body内容
###发表时间：2015-01-20
###分类：REST,java,Spring,RestTemplate
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2177693" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2177693</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
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


	&lt;bean id="template" class="org.springframework.web.client.RestTemplate"&gt;
		&lt;constructor-arg&gt;
			&lt;bean class="org.springframework.http.client.HttpComponentsClientHttpRequestFactory"/&gt;
		&lt;/constructor-arg&gt;
	&lt;/bean&gt;

	
&lt;/beans&gt;
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;
import org.springframework.http.HttpEntity;
import org.springframework.http.HttpHeaders;
import org.springframework.http.HttpMethod;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.client.RestTemplate;
import org.springframework.web.util.UriComponents;
import org.springframework.web.util.UriComponentsBuilder;

import java.net.URI;

/**
 * &lt;pre&gt;
 * Example01.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2015年1月20日 下午2:59:00&lt;br&gt;
 * Description :类实现描述
 * &lt;/pre&gt;
 */
public class Example01 {
    
    public static URI createUri(String host, int port, String path,
            Object... args) {
        UriComponents uriComponents = UriComponentsBuilder.newInstance()
                .port(port).scheme("http").host(host).path(path).build();
        if (null != args &amp;&amp; args.length &gt; 0) {
            uriComponents.expand(args);
        }
        uriComponents.encode();
        return uriComponents.toUri();
    }

    /**
     * &lt;pre&gt;
     * @param args
     * &lt;/pre&gt;
     */
    public static void init(String[] args) {
        context = new FileSystemXmlApplicationContext(
                "D:/baidu/workspaces/workspace_java/test/src/main/java/com/baidu/learn/spring/restTemplate/spring-ctx-application.xml");
        template = context.getBean("template", RestTemplate.class);
    }

    public static void main(String[] args) {
        init(args);
        // ===========================
        Example01 e = new Example01();
        e.testHttpCode();
        e.testHttpLog();
    }

    private static ApplicationContext context;

    private static RestTemplate template;

    private final String url = "http://cp01-rd-crm-cdc-db05.cp01.baidu.com:8097/dispatch-cdc-etl-test-leader-4597-20150120041830-ShellRunner-0.out";

    /**
     * &lt;pre&gt;
     * @param template
     * @param url
     * @return 是否2xx的成功状态
     * &lt;/pre&gt;
     */
    private boolean is2xxSuccessful(RestTemplate template, String url) {
        HttpHeaders headers = new HttpHeaders();
        headers.add("Content-Type", "text/html");
        headers.add(
                "Accept",
                "text/html,application/xhtml+xml,application/xml,application/json;q=0.9,image/webp,*/*;q=0.8");
        headers.add("Accept-Encoding", "gzip, deflate, sdch");
        headers.add("Cache-Control", "max-age=0");
        headers.add("Connection", "keep-alive");
        HttpEntity&lt;String&gt; requestEntity = new HttpEntity&lt;String&gt;(headers);
        ResponseEntity&lt;String&gt; responseEntity = template.exchange(url,
                HttpMethod.GET, requestEntity, String.class);
        HttpStatus status = responseEntity.getStatusCode();
        return status.is2xxSuccessful();
    }

    /**
     * &lt;pre&gt;
     * @param template
     * @param url
     * @return 读取远程url的文件内容
     * &lt;/pre&gt;
     */
    private String readContentFromRemote(RestTemplate template, String url) {
        ResponseEntity&lt;String&gt; entity = template
                .getForEntity(url, String.class);
        return entity.getBody();
    }

    private void testHttpCode() {
        boolean is2xxSuccessful = is2xxSuccessful(template, url);
        System.out.println(String.format("url:%s : %s", url, is2xxSuccessful));
    }

    private void testHttpLog() {
        String body = readContentFromRemote(template, url);
        System.out.println(body);
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>