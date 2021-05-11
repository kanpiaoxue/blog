#如何使用restclient来发送post请求参数
###发表时间：2014-09-02
###分类：REST,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2112153" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2112153</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我喜欢使用&nbsp;restclient 来测试我的 REST 风格的应用程序。一般我就是用GET方法，今天用到了POST方法。POST传递参数应该放在body里面，对长度没有限制。不像GET对URL的限制是1024字节。</p> 
 <p>运行&nbsp;restclient ，点选Method选项卡的“POST”方法。然后选择Body选项卡，下下拉列表中选择”String body“的选项，配置上 application/x-www-form-urlencoded;charset=UTF-8 。再出现的body里面写入字符串，也就是你的请求条件，如：query=xpsF</p> 
 <p>这样就可以传递post的参数了。</p> 
 <p>java代码如下：springmvc写的</p> 
 <pre name="code" class="java">    @RequestMapping(value = "/test", method = { RequestMethod.GET,
            RequestMethod.POST })
    public void test(HttpServletResponse response, @RequestBody String message) {
//注意这里的：@RequestBody String message
        LOGGER.debug(String.format("receive message %s", message));
        Map&lt;String, String&gt; map = Maps.newHashMap();

        try {
            map.put("result", message);
            Tools.printToJson(JSON.toJSONString(map), response);
        } catch (Exception e) {
            LOGGER.error(e.getMessage(), e);
        }
    }</pre> 
 <p>&nbsp;</p> 
 <p>如果传递的是一个对象给springmvc，如（代码不全）：</p> 
 <pre name="code" class="java">public class EntitySubscribe {
    private Long entityId;
    private String entityCode;
    private String entityName;
    private String teamCode;
    private SubscribeUsesEnum subscribeUsesEnum;
    private Date gmtCreate;
    private Date gmtModify;
    private Long flowId;
    private OnOffEnum state;

    private String reason;
    private List&lt;Integer&gt; uses;
}</pre> 
 <p>&nbsp;</p> 
 <p>mvc代码：</p> 
 <pre name="code" class="java">    @ResponseBody
    @RequestMapping(value = "/subscribeEntity", method = { RequestMethod.POST })
    public AjaxResult subscribeEntity(@RequestBody EntitySubscribe entitySubscribe, @CookieValue(
            value = Const.COOKIE_USER_KEY, required = false) String userId) {
        LOGGER.debug(this.getClass().getName() + "#subscribeEntity");

        long entityId = entitySubscribe.getEntityId();
        String teamCode = entitySubscribe.getTeamCode();
        String subscribeUses = Joiner.on(",").skipNulls().join(entitySubscribe.getUses());
        String reason = entitySubscribe.getReason();

        Preconditions.checkArgument(StringUtils.isNotBlank(teamCode));
        Preconditions.checkArgument(StringUtils.isNotBlank(subscribeUses));
        Preconditions.checkArgument(StringUtils.isNotBlank(reason));
        Preconditions.checkArgument(StringUtils.isNotBlank(userId));
        return entitySubscribeService.subscribeEntity(entityId, teamCode, subscribeUses, reason, userId);
    }</pre> 
 <p>&nbsp;</p> 
 <p>使用restclient的请求为 ：POST</p> 
 <p>String body 为：&nbsp;application/json; charset=UTF-8</p> 
 <p>body内容为：{"entityId":343,"reason":"for test测试","teamCode":"cdc","uses":[1,2,3]}</p> 
 <p>这样后台就能收到对象了。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>