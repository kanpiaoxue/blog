#ajax向springmvc传递对象参数
###发表时间：2017-10-26
###分类：Spring,javascript,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2397672" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2397672</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我们在使用前端的ajax技术过程中，有的时候简简单单的向后台的springmvn传递参数，直接使用如下代码即可：（jquery的ajax代码）</p> 
 <pre name="code" class="js">var options = {
    url: 'helloworld',
    method: 'get',
    dataType: 'json',
    data: {
        teamId: 123
    },
    success: function (rs) {
        // code here
    },
    error: function (rs) {
        // code here
    }
};
$.ajax(options);</pre> 
 <p>&nbsp;后台springmvc代码：</p> 
 <pre name="code" class="java">@RequestMapping(value = { "/helloworld" }, method = { RequestMethod.GET })
@ResponseBody
public Boolean helloworld(@RequestParam("teamId") Long teamId)  {
    LOGGER.debug("start to helloworld. teamId:{}", teamId);
   
    Boolean rs = null; // coder here
    LOGGER.debug("finish helloworld. teamId:{}", teamId);
    return rs;
}</pre> 
 <p>&nbsp;上面也是常用的情况。</p> 
 <p>但是有的时候我们需要用ajax向后台传递对象，该如何做呢？前端传递的是JavaScript的对象，而后台接收的是java的对象。springmvn为我们做好了由JavaScript对象到Java对象的json转换。如下：</p> 
 <pre name="code" class="js">var paramsArr = [];
for(var i = 0; i &lt; 10; i++) {
    var obj = {
        id: i,
        name: 'name-' + i
    };
    paramsArr.push(obj);
}

var options = {
    url: 'helloworld',
    method: 'post', // 注意这里，传递对象给后台，这里必须是 POST 否则无法将对象封装到POST的body中流
    dataType: 'json',
    contentType: 'application/json', // 注意这里，传递对象给后台，这里必须是 application/json
    data: JSON.stringify(paramsArr), // 注意这里，传递对象给后台，这里必须将对象进行序列化
    success: function (rs) {
        // code here
    },
    error: function (rs) {
        // code here
    }
};
$.ajax(options);</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">class Person {
    private Long id;
    private String name;
    // setter / getter here
}

/**
 * 
 *  注意参数中的 @RequestBody。 它将会读取POST请求中的body中的数据流，然后JSON反序列化为java的对象。
 */
@RequestMapping(value = { "/helloworld" }, method = { RequestMethod.POST })
@ResponseBody
public Boolean helloworld(@RequestBody List&lt;Person&gt; persons)  {
    LOGGER.debug("start to helloworld. persons:{}", persons);
   
    Boolean rs = null; // coder here
    LOGGER.debug("finish helloworld. persons:{}", persons);
    return rs;
}</pre> 
 <p>这样对象参数就能传递给后台了。</p> 
</div>