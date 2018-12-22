#RestTemplate访问Protobuf
###发表时间：2014-09-28
###分类：java,REST,protobuf,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2123406" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2123406</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用RestTemplate访问google的protobuf的例子。其实很简单，Client端的代码如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">RestTemplate restTemplate = new RestTemplate();
byte[] rs = restTemplate.getForObject(url, byte[].class, args);
ProtobufResult.PBResult obj = ProtobufResult.PBResult.parseFrom(rs);</pre> 
 <p>RestTemplate的另一种声明，使用spring的xml，利用HttpClient的高级功能。</p> 
 <pre name="code" class="xml">&lt;bean id="restTemplate" class="org.springframework.web.client.RestTemplate"&gt;
&lt;constructor-arg&gt;
&lt;bean class="org.springframework.http.client.HttpComponentsClientHttpRequestFactory" /&gt;
&lt;/constructor-arg&gt;
&lt;/bean&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;ProtobufResult.PBResult 是我根据pbresult.proto&nbsp;文件生成的类文件。</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  #protoc.exe ./proto/pbresult.proto --java_out=./src
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>server端的代码，用来返回给客户端Protobuf的消息：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    /**
     * &lt;pre&gt;
     * @param response
     * @param status 0 成功，其他：不成功
     * @param statusInfo 信息
     * @param data 返回的数据json格式
     * &lt;/pre&gt;
     */
    public static void processProtobufResultWithData(HttpServletResponse response,
            int status, String statusInfo, String data) {
        ProtobufResult.PBResult.Builder builder = ProtobufResult.PBResult
                .newBuilder();
        OutputStream out = null;
        try {
            out = response.getOutputStream();
            builder.setStatus(status).setStatusInfo(statusInfo).setData(data)
                    .build().writeTo(out);
        } catch (IOException e) {
            LOGGER.error(e.getMessage(), e);
            try {
                builder.setStatus(-1).setStatusInfo(e.getMessage()).build()
                        .writeTo(out);
            } catch (IOException ex) {
                LOGGER.error(ex.getMessage(), ex);
            }
        } finally {
            IOUtils.closeQuietly(out);
        }
    }</pre> 
 <pre name="code" class="java">    /**
     * &lt;pre&gt;
     * @param response
     * @param status 0 成功，其他：不成功
     * @param statusInfo 信息
     * &lt;/pre&gt;
     */
    public static void processProtobufResultWithoutData(HttpServletResponse response,
            int status, String statusInfo) {
        processProtobufResultWithData(response, status, statusInfo, null);
    }</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>pbresult.proto</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  package tutorial;
  <br>
  <br>option java_package = "org.kanpiaoxue.test.protobuf";
  <br>option java_outer_classname = "ProtobufResult";
  <br>
  <br>message PBResult {
  <br> required int32 status = 1;
  <br> optional string statusInfo = 2;
  <br> optional string data = 3;
  <br>}
 </div> 
 <p>&nbsp;</p> 
 <p>我们有的时候需要向HTTP的对方发起POST请求，而且post的参数都要使用Protobuf进行封装，如果操作呢？</p> 
 <p>下面是发送方的springmvc的Controller的代码：</p> 
 <pre name="code" class="java"> /**
     *&lt;pre&gt;
     * @param response
     * @param id
     * @param name
     * @param email
     * 
     * http://localhost:8080/dmap-console/web/testPb/receiveAndPOSTTestPBMessage
     *&lt;/pre&gt;
     */
    @RequestMapping(value = "/receiveAndPOSTTestPBMessage",
            method = { RequestMethod.POST })
    public void receiveAndPOSTTestPBMessage(HttpServletResponse response,
            int id, String name, String email) {
        String url = createRemoteUrl(receiveAndPOSTTestPBMessageUrl);
        LOGGER.debug(String.format(
                "receive id:%d,name:%s,email:%s and route url[%s]", id, name,
                email, url));
        try {
            Preconditions.checkArgument(id &gt; 0);
            Preconditions.checkArgument(!Strings.isNullOrEmpty(name));
            Preconditions.checkArgument(!Strings.isNullOrEmpty(email));
            
            PostArgsExample.Message.Builder builder = PostArgsExample.Message
                    .newBuilder();
            byte[] args = builder.setId(id).setName(name).setEmail(email)
                    .build().toByteArray();
            AjaxResult result = postForPBResult(restTemplate, url, args);

            Tools.printToJson(result, response);
        } catch (Exception e) {
            e.printStackTrace();
            processErrorForResponse(response, e.getMessage());
        }
    }


    /**
     * &lt;pre&gt;
     * @param restTemplate 
     * @param url http地址
     * @param args 参数
     * @return AjaxResult
     * @throws InvalidProtocolBufferException  抛出异常
     * 根据url使用POST从远程取回结果
     * &lt;/pre&gt;
     */
    public static AjaxResult postForPBResult(RestTemplate restTemplate,
            String url, Object args) throws InvalidProtocolBufferException {
        byte[] rs = restTemplate.postForObject(url, args, byte[].class);
        ProtobufResult.PBResult obj = ProtobufResult.PBResult.parseFrom(rs);
        AjaxResult result = new AjaxResult();
        result.setStatus(obj.getStatus());
        result.setStatusInfo(obj.getStatusInfo());
        return result;
    }</pre> 
 <p>&nbsp;</p> 
 <p>下面是接收方Controller的代码：</p> 
 <pre name="code" class="java">    /**
     * &lt;pre&gt;
     * @param response
     * @param args
     * &lt;/pre&gt;
     */
    @RequestMapping(value = "/receiveAndPOSTTestPBMessage",
            method = { RequestMethod.POST })
    public void receiveAndPOSTTestPBMessage(HttpServletResponse response,
            @RequestBody byte[] args) {
        LOGGER.debug("receiveAndPOSTTestPBMessage");
        try {
            Preconditions.checkNotNull(args, "byte[] args is null!");
            PostArgsExample.Message message = PostArgsExample.Message
                    .parseFrom(args);
            LOGGER.debug(String.format("receive message %s", message.toString()));
            int status = 0;
            String statusInfo = "OK";
            Tools.processProtobufResultWithData(response, status, statusInfo,
                    message.toString());
        } catch (Exception e) {
            e.printStackTrace();
            Tools.processProtobufResultWithoutData(response, -1, "error-test");
        }
    }</pre> 
 <p>&nbsp;</p> 
</div>