#spring@value的默认值和SpEL的使用赋值
###发表时间：2018-12-08
###分类：springboot,Spring,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434940" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434940</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">@Value("${testWeb.host}") // 注入属性
private String host;
@Value("${testWeb.startpagenumber:1}") // 设置默认值
private Integer startPageNumber;
@Value("${testWeb.endpagenumber: #{T(java.lang.Integer).MAX_VALUE}}") // 使用SpEL设置默认值
private Integer endPageNumber; </pre> 
 <p>&nbsp;</p> 
</div>