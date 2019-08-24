#JSONObject与JSONArray的使用
###发表时间：2015-12-08
###分类：json,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2262718" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2262718</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>在进行json的反序列化的时候，往往我只需要json中的一段报文，而不是整个报文。该如何处理呢？</p> 
 <p>这个时候我们就可以使用”JSONObject与JSONArray“来解决我们的问题。如下面的代码，我只对其中json里面的<span style="font-family: monospace; line-height: 1.5; background-color: #fafafa;">processActions的数组里面的</span><span style="font-family: monospace; line-height: 1.5; background-color: #fafafa;">clazzName感兴趣。我将会进行如下处理：（使用的是</span><span style="font-family: monospace;">com.alibaba.fastjson这个包，阿里提供的</span><span style="font-family: monospace; line-height: 1.5; background-color: #fafafa;">）</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">        String json = "{\"beforeActions\":[],\"finallyActions\":[],\"processActions\":[{\"clazzName\":\"com.baidu.rigel.dmap.runner.shell.ShellRunner\",\"configProperties\":[{\"name\":\"command\",\"value\":\"source /home/work/.ctrc &amp;&amp; make -f /home/work/workspace/ods-monitor/Makefile #  20150416\"},{\"name\":\"exitValue\",\"value\":\"0\"}],\"order\":1,\"resourceReq\":{\"runwayMemory\":0,\"runwayPoolMemory\":0},\"type\":1}],\"processParallel\":false}";
        
        JSONObject obj = JSONObject.parseObject(json);
        String str = obj.getString("processActions");
        JSONArray objs = JSONObject.parseArray(str);
        for(Object o : objs){
            JSONObject oTempbj = (JSONObject)o;
            System.out.println(oTempbj.get("clazzName"));
        }
        </pre> 
 <p>&nbsp;</p> 
 <p>参考文章：<a href="http://www.cnblogs.com/xwdreamer/archive/2011/12/16/2296904.html">http://www.cnblogs.com/xwdreamer/archive/2011/12/16/2296904.html</a></p> 
 <p>虽然这个文章是&nbsp;json-lib-2.2.2-jdk15.jar ，但是用法是一致的。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>