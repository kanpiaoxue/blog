#Lucene的pom.xml
###发表时间：2014-07-17
###分类：java,lucene
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2093198" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2093198</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="xml">&lt;properties&gt;
	&lt;lucene.version&gt;4.9.0&lt;/lucene.version&gt;
&lt;/properties&gt;		

&lt;!-- lucene start --&gt;
		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-analyzers&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-ant&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-bdb&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-benchmark&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-collation&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-core&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-highlighter&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-instantiated&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-lucli&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-memory&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-misc&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-queries&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-queryparser&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-regex&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-remote&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-smartcn&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-snowball&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-spatial&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-spellchecker&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-surround&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-swing&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-wikipedia&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;dependency&gt;
			&lt;groupId&gt; org.apache.lucene&lt;/groupId&gt;
			&lt;artifactId&gt;lucene-wordnet&lt;/artifactId&gt;
			&lt;version&gt; ${lucene.version}&lt;/version&gt;
		&lt;/dependency&gt;

		&lt;!-- lucene end --&gt;</pre> 
 <p>&nbsp;</p> 
</div>