#maven创建可执行jar（Executable JAR）
###发表时间：2014-04-01
###分类：java,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2039570" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2039570</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>使用maven创建可执行的jar。</p> 
 <p>插件：maven-shade-plugin，它可以让用户配置Main-Class的值，然后在打包的时候将值填入/META-INF/MANIFEST.MF文件。关于项目的依赖，它很聪明地将依赖JAR文件全部解压后，再将得到的.class文件连同当前项目的.class文件一起合并到最终的CLI包中，这样，在执行CLI JAR文件的时候，所有需要的类就都在Classpath中了。</p> 
 <p>maven-shade-plugin 插件的地址：&nbsp;<a href="http://maven.apache.org/plugins/maven-shade-plugin/">http://maven.apache.org/plugins/maven-shade-plugin/</a></p> 
 <p>Executable JAR的例子：&nbsp;<a href="http://maven.apache.org/plugins/maven-shade-plugin/examples/executable-jar.html">http://maven.apache.org/plugins/maven-shade-plugin/examples/executable-jar.html</a></p> 
 <p>例子的XML：</p> 
 <p>To create an executable uber JAR, one simply needs to set the main class that serves as the application entry point:</p> 
 <pre name="code" class="xml">&lt;project&gt;
  ...
  &lt;build&gt;
    &lt;!-- 指定最终package的jar的名称 --&gt;
    &lt;finalName&gt;mysql-backup&lt;/finalName&gt;
    &lt;plugins&gt;
      &lt;plugin&gt;
        &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
        &lt;artifactId&gt;maven-shade-plugin&lt;/artifactId&gt;
        &lt;version&gt;2.2&lt;/version&gt;
        &lt;executions&gt;
          &lt;execution&gt;
            &lt;phase&gt;package&lt;/phase&gt;
            &lt;goals&gt;
              &lt;goal&gt;shade&lt;/goal&gt;
            &lt;/goals&gt;
            &lt;configuration&gt;
              &lt;transformers&gt;
                &lt;transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer"&gt;
                  &lt;mainClass&gt;org.sonatype.haven.HavenCli&lt;/mainClass&gt;
                &lt;/transformer&gt;
              &lt;/transformers&gt;
            &lt;/configuration&gt;
          &lt;/execution&gt;
        &lt;/executions&gt;
      &lt;/plugin&gt;
    &lt;/plugins&gt;
  &lt;/build&gt;
  ...
&lt;/project&gt;</pre> 
 <p>&nbsp;</p> 
 <p><span style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 15.600000381469727px;">This snippet configures a special resource transformer which sets the&nbsp;</span><tt style="font-size: 12px; line-height: 15.600000381469727px;">Main-Class</tt><span style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 15.600000381469727px;">&nbsp;entry in the&nbsp;</span><tt style="font-size: 12px; line-height: 15.600000381469727px;">MANIFEST.MF</tt><span style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 15.600000381469727px;">&nbsp;of the shaded JAR. Other entries can be added to the&nbsp;</span><tt style="font-size: 12px; line-height: 15.600000381469727px;">MANIFEST.MF</tt><span style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 15.600000381469727px;">&nbsp;as well via key-value pairs in the&nbsp;</span><tt style="font-size: 12px; line-height: 15.600000381469727px;">&lt;manifestEntries&gt;</tt><span style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 15.600000381469727px;">&nbsp;section:</span></p> 
 <pre name="code" class="xml">&lt;project&gt;
  ...
  &lt;build&gt;
    &lt;!-- 指定最终package的jar的名称 --&gt;
    &lt;finalName&gt;mysql-backup&lt;/finalName&gt;
    &lt;plugins&gt;
      &lt;plugin&gt;
        &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
        &lt;artifactId&gt;maven-shade-plugin&lt;/artifactId&gt;
        &lt;version&gt;2.2&lt;/version&gt;
        &lt;executions&gt;
          &lt;execution&gt;
            &lt;phase&gt;package&lt;/phase&gt;
            &lt;goals&gt;
              &lt;goal&gt;shade&lt;/goal&gt;
            &lt;/goals&gt;
            &lt;configuration&gt;
              &lt;transformers&gt;
                &lt;transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer"&gt;
                  &lt;manifestEntries&gt;
                    &lt;Main-Class&gt;org.sonatype.haven.ExodusCli&lt;/Main-Class&gt;
                    &lt;Build-Number&gt;123&lt;/Build-Number&gt;
                  &lt;/manifestEntries&gt;
                &lt;/transformer&gt;
              &lt;/transformers&gt;
            &lt;/configuration&gt;
          &lt;/execution&gt;
        &lt;/executions&gt;
      &lt;/plugin&gt;
    &lt;/plugins&gt;
  &lt;/build&gt;
  ...
&lt;/project&gt;</pre> 
 <p><span style="font-family: Verdana, Helvetica, Arial, sans-serif; font-size: 12px; line-height: 15.600000381469727px;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>