#springboot 返回JSON日期格式问题
###发表时间：2021-03-24
###分类：springboot,Spring,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519894" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519894</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>springboot返回的时间格式，根据版本的不同，可能返回时间戳，还可能返回UTC时间格式。</p> 
 <p>如：&nbsp;"createTime": 1537407384500 或者&nbsp;"createTime": "2018-09-18T10:54:06.000+0000"</p> 
 <p>如何定制化springboot返回的时间格式呢？</p> 
 <p>修改&nbsp;application.properties/yml 里面的配置即可。</p> 
 <pre name="code" class="java">spring:
    jackson:
        date: yyyy-MM-dd HH:mm:ss
        time-zone: GMT+8
        serialization:
            write-dates-as-timestamps: false</pre> 
 <p>上面的是全局的时间格式化配置，如果要想在某个特定的接口返回特定的时间格式，如何处理？</p> 
 <pre name="code" class="java">@JsonFormat(pattern="yyyy-MM-dd",timezone = "GMT+8")
private Date createTime;</pre> 
 <p>&nbsp;&nbsp;如上，可以在时间字段上面添加&nbsp;@JsonFormat 来指定时间格式。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考资料：</p> 
 <p>1、<a href="https://blog.csdn.net/jeikerxiao/article/details/86217807">https://blog.csdn.net/jeikerxiao/article/details/86217807</a></p> 
 <p>2、<a href="https://www.baeldung.com/spring-boot-formatting-json-dates">https://www.baeldung.com/spring-boot-formatting-json-dates</a></p> 
</div>