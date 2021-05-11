#Spring RestTemplate处理请求的泛型的情况：ParameterizedTypeReference
###发表时间：2020-04-26
###分类：REST,java,Spring,RestTemplate
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2513850" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2513850</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考文章：&nbsp;<a href="https://stackoverflow.com/questions/36915823/spring-resttemplate-and-generic-types-parameterizedtypereference-collections-lik">https://stackoverflow.com/questions/36915823/spring-resttemplate-and-generic-types-parameterizedtypereference-collections-lik</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public &lt;T&gt; List&lt;T&gt; exchangeAsList(String uri, ParameterizedTypeReference&lt;List&lt;T&gt;&gt; responseType) {
    return restTemplate.exchange(uri, HttpMethod.GET, null, responseType).getBody();
}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">List&lt;MyDto&gt; dtoList = this.exchangeAsList("http://my/url", new ParameterizedTypeReference&lt;List&lt;MyDto&gt;&gt;() {});</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;比较完整的示例代码：</p> 
 <pre name="code" class="java">private HttpHeaders buildHeader() {
    HttpHeaders headers = new HttpHeaders();
    headers.set("authToken", "hello-token");
    headers.setContentType(MediaType.APPLICATION_JSON_UTF8);
    return headers;
}


public &lt;T, E&gt; List&lt;T&gt; postExchangeAsList(String url, E body,
        ParameterizedTypeReference&lt;List&lt;T&gt;&gt; responseType) {
    Stopwatch sw = Stopwatch.createStarted();
    HttpHeaders headers = buildHeader();
    HttpEntity&lt;E&gt; entity = new HttpEntity&lt;E&gt;(body, headers);
    HttpEntity&lt;List&lt;T&gt;&gt; httpResponse =
            restTemplate.exchange(url, HttpMethod.POST, entity, responseType);
    List&lt;T&gt; result = httpResponse.getBody();
    return result;
}



private &lt;T&gt; List&lt;T&gt; getExchangeAsList(String url,
        ParameterizedTypeReference&lt;List&lt;T&gt;&gt; responseType) {
    Stopwatch sw = Stopwatch.createStarted();

    HttpHeaders headers = buildHeader();
    HttpEntity&lt;Object&gt; entity = new HttpEntity&lt;Object&gt;(headers);

    ResponseEntity&lt;List&lt;T&gt;&gt; response =
            restTemplate.exchange(url, HttpMethod.GET, entity, responseType);
    List&lt;T&gt; result = response.getBody();
    return result;
}


List&lt;String&gt; list = getExchangeAsList("http://my/helloGet", new ParameterizedTypeReference&lt;List&lt;String&gt;&gt;&gt;() {
                });


String body = "hello world";
List&lt;String&gt; list = postExchangeAsList("http://my/helloPost", body,
                new ParameterizedTypeReference&lt;List&lt;String&gt;&gt;() {
                });</pre> 
 <p>&nbsp;&nbsp;</p> 
</div>