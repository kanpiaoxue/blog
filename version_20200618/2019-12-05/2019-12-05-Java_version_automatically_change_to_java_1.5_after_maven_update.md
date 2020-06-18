#Java version automatically change to java 1.5 after maven update
###发表时间：2019-12-05
###分类：eclipse,经验,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2510830" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2510830</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>Java version automatically change to java 1.5 after maven update</p> 
 <p>参考地址：<a href="https://stackoverflow.com/questions/28509928/java-version-automatically-change-to-java-1-5-after-maven-update/28510029">https://stackoverflow.com/questions/28509928/java-version-automatically-change-to-java-1-5-after-maven-update/28510029</a></p> 
 <p>&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">Open your&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">pom.xml</code>&nbsp;file and add the following lines on it:</p> 
 <pre name="code" class="xml">&lt;properties&gt;
    &lt;maven.compiler.source&gt;1.8&lt;/maven.compiler.source&gt; 
    &lt;maven.compiler.target&gt;1.8&lt;/maven.compiler.target&gt;
&lt;/properties&gt;</pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">Where&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">1.8</code>&nbsp;is the java version of your current JDK/JRE. Another way of doing this is adding a&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">&lt;build&gt;</code>&nbsp;with the&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">maven-compile-plugin</code>&nbsp;as</p> 
 <pre name="code" class="xml">&lt;build&gt;
 &lt;plugins&gt;
  &lt;plugin&gt;
    &lt;groupId&gt;org.apache.maven.plugins&lt;/groupId&gt;
    &lt;artifactId&gt;maven-compiler-plugin&lt;/artifactId&gt;
    &lt;version&gt;3.2&lt;/version&gt;
   &lt;!-- or whatever current version --&gt;
  &lt;configuration&gt;
     &lt;source&gt;1.8&lt;/source&gt;
     &lt;target&gt;1.8&lt;/target&gt;
  &lt;/configuration&gt;
 &lt;/plugin&gt;
 &lt;/plugins&gt;
&lt;/build&gt;</pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
 <p>&nbsp;</p> 
</div>