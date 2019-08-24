#eclipse 格式化 javadoc 中的@为@的问题
###发表时间：2017-08-14
###分类：eclipse,非技术,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2389595" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2389595</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>之前使用 eclipse 的格式化一直有个问题困扰着我，就是在 javadoc 中的@符号被格式化为&amp;#64; &nbsp;。在很多地方都找寻过答案，一直没得到合理的解决。</p> 
 <p>今天无意中发现了问题的所在，就是我的 javadoc 的用法如下：</p> 
 <pre name="code" class="java">    /**
     * &lt;pre&gt;
     * @param sourceColumn
     * @param targetColumn dfd
     * @param value
     * @author kanpiaoxue
     * @CreateTime 2017/08/14 13:18:25&lt;br&gt;
     * &lt;/pre&gt;
     */</pre> 
 <p>&nbsp;使用 eclipse 格式化之后如下：</p> 
 <pre name="code" class="java">    /**
     * &lt;pre&gt;
     * &amp;#64;param sourceColumn
     * &amp;#64;param targetColumn dfd
     * &amp;#64;param value
     * &amp;#64;author kanpiaoxue
     * &amp;#64;CreateTime 2017/08/14 13:18:25&lt;br&gt;
     * &lt;/pre&gt;
     */</pre> 
 <p>&nbsp;今天我发现把@这个符号放在&lt;pre&gt;标签里面就会存在上面的问题，将@符号从&lt;pre&gt;的范围挪出来就没问题了。</p> 
 <p>如下：</p> 
 <pre name="code" class="java">    /**
     * &lt;pre&gt;
     * Description: this is a test case.
     * &lt;/pre&gt;
     * 
     * @param sourceColumn
     * @param targetColumn dfd
     * @param value
     * @author kanpiaoxue
     * @CreateTime 2017/08/14 13:18:25&lt;br&gt;
     * 
     */</pre> 
 <p>&nbsp;困扰了我很久的问题终于得到了解决。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>