#springboot的应用开发经验小结
###发表时间：2018-09-14
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2430688" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2430688</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;springboot一个主要的特性就是自动配置。只要你把用到的一些关键的功能的类放在classpath里面，它就会自动装配。同时也会引起问题：springboot自己管理了很多依赖jar，它们的版本都是springboot经过冲突测试过的。如果自己贸然引入其他jar和springboot里面的jar重合，比如apache commons 下面的jar，可能引起springboot的运行问题。</p> 
 <p>&nbsp;解决方案：去springboot支持的经过测试的外部依赖去查查自己需要的jar是否已经存在了，如果存在直接引入依赖，不要写被依赖的jar的version即可。下面的url就是springboot的/2.0.5所有测试过的jar。</p> 
 <p><a href="https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/html/appendix-dependency-versions.html">&nbsp;https://docs.spring.io/spring-boot/docs/2.0.5.RELEASE/reference/html/appendix-dependency-versions.html</a></p> 
</div>