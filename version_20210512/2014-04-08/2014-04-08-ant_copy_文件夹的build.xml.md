#ant copy 文件夹的build.xml
###发表时间：2014-04-08
###分类：java,ant
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2041968" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2041968</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>通过该xml，可以让ant拷贝指定的源文件夹的所有内容到目的文件夹，ant会自动创建目的文件夹下面所有的子文件夹和文件。这个copy的过程，会忽略掉所有SVN的文件，比如：.svn 文件夹下面所有的内容。</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;?xml version="1.0" encoding="UTF-8" ?&gt;
&lt;project default="copy" name="copyTask"&gt;

	&lt;property name="base-dir" value="workspaces" /&gt;
	&lt;property name="to-dir" value="G:/xuepeng/E-disk/${base-dir}" /&gt;
	&lt;property name="from-dir" value="E:/${base-dir}" /&gt;
	
	&lt;defaultexcludes echo="true" /&gt;
	
	&lt;description&gt;
		Copy files from ${from-dir} to ${to-dir} without .svn files etc.
	&lt;/description&gt;
	
	&lt;target name="clean"&gt;
		&lt;delete dir="${to-dir}" /&gt;
	&lt;/target&gt;

	&lt;target name="init" depends="clean"&gt;
		&lt;mkdir dir="${to-dir}" /&gt;
	&lt;/target&gt;
		
	&lt;target name="copy" depends="init"&gt;
		&lt;copy todir="${to-dir}"&gt;
			&lt;fileset dir="${from-dir}"&gt;
				&lt;include name="**/*" /&gt;
			&lt;/fileset&gt;
		&lt;/copy&gt;
	&lt;/target&gt;

&lt;/project&gt;
</pre> 
 <p>&nbsp;</p> 
</div>