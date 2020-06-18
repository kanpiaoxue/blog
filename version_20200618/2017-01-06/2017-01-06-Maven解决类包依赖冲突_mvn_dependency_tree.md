#Maven解决类包依赖冲突:mvn dependency:tree
###发表时间：2017-01-06
###分类：maven,非技术,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2350824" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2350824</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>在使用maven管理jar的依赖关系的时候，经常发生jar的不同版本冲突。如何解决呢？</p> 
 <p>使用命令：&nbsp;mvn dependency:tree 来查看依赖关系树形结构，从中排查冲突的jar。</p> 
 <p>可以使用命令 &nbsp;mvn dependency:tree &gt; dependency_tree.txt 的文件，使用文件编辑器查看效果更好。</p> 
 <p>如果找到冲突的jar，该如何处理呢？在冲突的地方进行排除即可，如下：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;dependency&gt;
	&lt;groupId&gt;org.kanpiaoxue&lt;/groupId&gt;
	&lt;artifactId&gt;configcenter-bjf&lt;/artifactId&gt;
	&lt;version&gt;${configcenter.version}&lt;/version&gt;
	&lt;!-- 排除掉冲突的jar start --&gt;
	&lt;exclusions&gt;
		&lt;exclusion&gt;
			&lt;groupId&gt;org.springframework&lt;/groupId&gt;
			&lt;artifactId&gt;spring&lt;/artifactId&gt;
		&lt;/exclusion&gt;
		&lt;exclusion&gt;
			&lt;groupId&gt;commons-httpclient&lt;/groupId&gt;
			&lt;artifactId&gt;commons-httpclient&lt;/artifactId&gt;
		&lt;/exclusion&gt;
	&lt;/exclusions&gt;
	&lt;!-- 排除掉冲突的jar end  --&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>