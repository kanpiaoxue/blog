#Spring整合JUnit4测试使用注解引入多个配置文件
###发表时间：2014-11-03
###分类：Spring,junit,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2151903" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2151903</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>我们使用spring写junit单测的时候，有的时候我们的spring配置文件只有一个。我们在类的注释上面会这样写：</p> 
 <pre name="code" class="java">@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath*:spring-ctx-application.xml")</pre> 
 <p>&nbsp;但有的时候我们的项目很复杂，其中的spring配置文件被拆分成了多个，这样该如何写上面这段单测代码而引入多个配置文件呢？如下：</p> 
 <pre name="code" class="java">@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = { "classpath*:spring-ctx-application.xml",
        "classpath*:spring-ctx-consumer.xml" })</pre> 
 <p>&nbsp;这样就可以轻松的引入多个spring的配置文件了。</p> 
 <p>或者配置符合某一个正则表达式的一类文件，如：</p> 
 <pre name="code" class="java">@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath*:spring-ctx-*.xml")</pre> 
 <p>&nbsp;</p> 
</div>