#springboot RestTemplate整合
###发表时间：2019-10-08
###分类：Spring,springboot,java,REST
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2508613" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2508613</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.client.ClientHttpRequestFactory;
import org.springframework.http.client.SimpleClientHttpRequestFactory;
import org.springframework.web.client.RestTemplate;

import com.google.common.primitives.Ints;

import java.util.Objects;

/**
 * RestTemplate配置类
 *
 * @ClassName: RestTemplateConfig
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/10/08 09:42:39
 * @Description:
 */
@Configuration
public class RestTemplateConfig {
    private static final Logger LOGGER = LoggerFactory.getLogger(RestTemplateConfig.class);

    @Value("${csis.http.connectTimeout:15000}")
    private String connectTimeoutString;
    @Value("${csis.http.readTimeout:5000}")
    private String readTimeoutString;

    @Bean
    public RestTemplate restTemplate(ClientHttpRequestFactory factory) {
        return new RestTemplate(factory);
    }

    @Bean
    public ClientHttpRequestFactory simpleClientHttpRequestFactory() {
        LOGGER.info("start to simpleClientHttpRequestFactory. readTimeoutString:{},connectTimeoutString:{}",
                readTimeoutString, connectTimeoutString);

        Objects.requireNonNull(readTimeoutString, "readTimeoutString is null");
        Objects.requireNonNull(connectTimeoutString, "connectTimeoutString is null");

        int connectTimeout = Ints.tryParse(connectTimeoutString);
        int readTimeout = Ints.tryParse(readTimeoutString);

        SimpleClientHttpRequestFactory factory = new SimpleClientHttpRequestFactory();
        factory.setConnectTimeout(connectTimeout);
        factory.setReadTimeout(readTimeout);
        return factory;
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Service
public class HelloService {
 
    @Autowired
    private RestTemplate restTemplate;
 
    public String get(Integer id){
        return restTemplate.getForObject("http://localhost:8080/hello?userId="+id,String.class);
    }
}
</pre> 
 <p>&nbsp;</p> 
</div>