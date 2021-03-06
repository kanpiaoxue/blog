#RestTemplate例子
###发表时间：2014-09-01
###分类：java,Spring,REST,RestTemplate
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2111780" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2111780</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>RestTemplate的一个例子，很简单。更多<span style="font-size: 12px; line-height: 1.5;">RestTemplate</span><span style="font-size: 12px; line-height: 1.5;">的内容请看附件。</span></p> 
 <p>pom.xml</p> 
 <pre name="code" class="java">&lt;dependency&gt;
	&lt;groupId&gt;org.apache.httpcomponents&lt;/groupId&gt;
	&lt;artifactId&gt;httpclient&lt;/artifactId&gt;
	&lt;version&gt;4.3.5&lt;/version&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <p>spring的xml</p> 
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
 <p>Java类：</p> 
 <pre name="code" class="java">import org.springframework.context.ApplicationContext;
import org.springframework.context.support.FileSystemXmlApplicationContext;
import org.springframework.http.client.HttpComponentsClientHttpRequestFactory;
import org.springframework.web.client.RestTemplate;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

/**
 * &lt;pre&gt;
 * ExampleRestTemplate.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年9月1日 下午4:21:51&lt;br&gt;
 * Description : RestTemplate例子
 * &lt;/pre&gt;
 */
public class ExampleRestTemplate {

    /**
     * &lt;pre&gt;
     * @param args
     * &lt;/pre&gt;
     */
    public static void main(String[] args) {

        RestTemplate template = new RestTemplate(
                new HttpComponentsClientHttpRequestFactory());
        String rs = template
                .getForObject(
                        "http://localhost:8080/dmap-console/web/config/test?message={message}",
                        String.class, "hello");
        System.out.println(rs);

        // spring start
        @SuppressWarnings("resource")
        ApplicationContext context = new FileSystemXmlApplicationContext(
                "D:/spring/restTemplate/spring-ctx-application.xml");
        final RestTemplate template1 = context.getBean("template",
                RestTemplate.class);

        ExecutorService exec = Executors.newCachedThreadPool();
        for (int i = 0, j = Runtime.getRuntime().availableProcessors() * 2; i &lt; j; i++) {
            exec.execute(new Runnable() {

                @Override
                public void run() {

                    for (int n = 0; n &lt; 10000; n++) {
                        String rs1 = template1
                                .getForObject(
                                        "http://localhost:8080/dmap-console/web/config/test?message={message}",
                                        String.class, "hello");
                        System.out.println(rs1);
                    }

                }
            });
        }
        exec.shutdown();
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>使用get请求，携带http header信息：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    public Result&lt;Void&gt; clearApiServerCache() {
        LOGGER.info("start to clearApiServerCache.");
        String url = "http://www.kanpiaoxue.org/team/clearAllTeamCache";        
        HttpHeaders headers = new HttpHeaders();
        headers.set("auth_token", "34qwljfalfjdl");
        headers.setContentType(MediaType.APPLICATION_JSON);
// application/json

        HttpEntity&lt;String&gt; entity = new HttpEntity&lt;String&gt;(headers);
        HttpEntity&lt;String&gt; response = restTemplate.exchange(url, HttpMethod.GET, entity, String.class);
        LOGGER.info("clearApiServerCache response:{}", response);
        Type typeOfT = new TypeToken&lt;Result&lt;Void&gt;&gt;() {
        }.getType();
        Result&lt;Void&gt; rs = new GsonBuilder().create().fromJson(response.getBody(), typeOfT);
        LOGGER.info("finish clearApiServerCache. rs:{}", rs);
        return rs;
    }</pre> &nbsp; 
 <p>&nbsp;定制ClientHttpRequestFactory，设置各种超时时间。</p> 
 <pre name="code" class="java">   private ClientHttpRequestFactory getClientHttpRequestFactory(int timeout) {
        RequestConfig config = RequestConfig.custom().setConnectTimeout(timeout)
                .setConnectionRequestTimeout(timeout).setSocketTimeout(timeout).build();
        CloseableHttpClient client = HttpClientBuilder.create().setDefaultRequestConfig(config).build();
        return new HttpComponentsClientHttpRequestFactory(client);
    }

ClientHttpRequestFactory requestFactory = getClientHttpRequestFactory(timeout);
        RestTemplate restTemplate = new RestTemplate(requestFactory);</pre> 
 <p>&nbsp;</p> 
 <p>携带header发送POST的请求</p> 
 <pre name="code" class="java">public void post() {
    String body = "热爱祖国";
    // 防止中文乱码
    MediaType mediaType = MediaType.parseMediaType("application/json; charset=UTF-8"); 
    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(mediaType);
    HttpEntity&lt;String&gt; request = new HttpEntity&lt;String&gt;(body, headers);
    String rs = restTemplate.postForObject(postUrl, request, String.class);
    System.out.println(rs);
}</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>解决RestTemplate的返回值的泛型问题</p> 
 <pre name="code" class="java">HttpHeaders headers = new HttpHeaders();
        headers.set("authToken", changefreeApiToken);
        headers.setContentType(MediaType.APPLICATION_JSON);

HttpEntity&lt;ApplyChangefreeArgs&gt; entity =
                new HttpEntity&lt;ApplyChangefreeArgs&gt;(body, headers);

ParameterizedTypeReference&lt;Result&lt;ChangefreeResult&gt;&gt; typeRef =
                new ParameterizedTypeReference&lt;Result&lt;ChangefreeResult&gt;&gt;() {
                };

        HttpEntity&lt;Result&lt;ChangefreeResult&gt;&gt; response =
                restTemplate.exchange(url, HttpMethod.POST, entity, typeRef);</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>比较完整的例子：</p> 
 <pre name="code" class="java">@Service
public class RestTemplateServiceImpl implements RestTemplateService {
    private static final Logger LOGGER = LoggerFactory.getLogger(RestTemplateServiceImpl.class);

   
    @Override
    public RestTemplate factory() {
        LOGGER.debug("start to factory.");
        ClientHttpRequestFactory requestFactory = getClientHttpRequestFactory();
        RestTemplate restTemplate = new RestTemplate(requestFactory);
        return restTemplate;
    }

    private ClientHttpRequestFactory getClientHttpRequestFactory() {
        // 默认30s超时
        int connectTimeout = 5000;
        int connectionRequestTimeout = 5000;
        int timeout = 5000;

        RequestConfig config = RequestConfig.custom().setConnectTimeout(connectTimeout)
                .setConnectionRequestTimeout(connectionRequestTimeout).setSocketTimeout(timeout).build();
        CloseableHttpClient client = HttpClientBuilder.create().setDefaultRequestConfig(config).build();
        return new HttpComponentsClientHttpRequestFactory(client);
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">private &lt;RQ, RP&gt; RP post(String apiUrl, RQ requestBody, ParameterizedTypeReference&lt;Result&lt;RP&gt;&gt; typeRef) {
    RestTemplate restTemplate = restTemplateService.factory();
    HttpHeaders headers = headers();
    String url = "http://xxxx:8080/hello";
    HttpEntity&lt;RQ&gt; entity = new HttpEntity&lt;RQ&gt;(requestBody, headers);

    Stopwatch sw = Stopwatch.createStarted();
    LOGGER.info("start to post. url:{},requestBody:{}", url, requestBody);
    HttpEntity&lt;Result&lt;RP&gt;&gt; response = restTemplate.exchange(url, HttpMethod.POST, entity, typeRef);
    Result&lt;RP&gt; result = response.getBody();
    LOGGER.info("finish post. url:{},requestBody:{},responseBody:{}. it consumes {}", url, requestBody,
            result, sw);
    Preconditions.checkArgument(result.isSuccess(), "access the url:%s get some error:%s", url,
            result.getError());
    return result.getData();
}
</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">private HttpHeaders headers() {
        String changefreeApiToken = "helloToken"
        HttpHeaders headers = new HttpHeaders();
        headers.set("authToken", changefreeApiToken);
        headers.setContentType(MediaType.APPLICATION_JSON);
        return headers;
    }    </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;<a href="https://www.baeldung.com/tag/resttemplate/">https://www.baeldung.com/tag/resttemplate/</a></p> 
</div>