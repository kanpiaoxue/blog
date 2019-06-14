#springboot的logback和spring-data-hbase的log4j冲突解决方法
###发表时间：2019-04-15
###分类：Spring,springboot,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2440120" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2440120</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>springboot默认的日志框架是logback，它的性能较好，功能强大。选择使用它的时候是默认支持的。但是在springboot里面引入spring-data-hbase（org.springframework.data.hadoop.hbase.HbaseTemplate）的时候，会引入mavendpom.xml的依赖。在hadoop、hbase的依赖里面会引入log4j。springboot在启动的时候感知到classpath里面有Log4j和logback，就会报错。</p> 
 <p>该如何处理呢？</p> 
 <p>方案：排除掉log4j的依赖，不能排除的将它转换为 slf4j</p> 
 <p>参考资料：&nbsp;<a href="https://stackoverflow.com/questions/34863719/spring-boot-use-logback-instead-of-log4j">https://stackoverflow.com/questions/34863719/spring-boot-use-logback-instead-of-log4j</a></p> 
 <p>&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">there are these three logging frameworks:</p> 
 <ul style="margin-bottom: 1em; margin-left: 30px; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; color: #242729;"> 
  <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: inherit; vertical-align: baseline;"> <code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">log4j</code>&nbsp;(ancient)</li> 
  <li style="margin-bottom: 0.5em; margin-left: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: inherit; vertical-align: baseline;"> <code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">slf4j</code>&nbsp;(api used everywhere, there are different backends available)</li> 
  <li style="margin-bottom: 0px; margin-left: 0px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: inherit; vertical-align: baseline;"> <code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">logback</code>&nbsp;(has nice features and configuration, successor of&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">slf4j</code>)</li> 
 </ul> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">you have to manually throw out&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">log4j</code>&nbsp;and replace it with the compatibility bridge&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">log4j-over-slf4j</code>.</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">there is a&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">slf4j</code>&nbsp;backend called&nbsp;<code style="margin: 0px; padding: 1px 5px; border: 0px; font-style: inherit; font-variant: inherit; font-weight: inherit; line-height: inherit; font-family: Consolas, Menlo, Monaco, 'Lucida Console', 'Liberation Mono', 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', 'Courier New', monospace, sans-serif; font-size: 13px; vertical-align: baseline; background-color: #eff0f1; white-space: pre-wrap;">logback-classic</code>.</p> 
 <pre name="code" class="xml">&lt;dependency&gt;
    &lt;!-- legacy log4j ==&gt; slf4j *** 这里是关键 ***--&gt;
    &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
    &lt;artifactId&gt;log4j-over-slf4j&lt;/artifactId&gt;
    &lt;version&gt;1.7.21&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
    &lt;!-- slf4j ==&gt; logback 这里也可以不明确的引入logback，因为springboot默认提供 --&gt;
    &lt;groupId&gt;ch.qos.logback&lt;/groupId&gt;
    &lt;artifactId&gt;logback-classic&lt;/artifactId&gt;
    &lt;version&gt;1.1.7&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
    &lt;groupId&gt;...no maintainer...&lt;/groupId&gt;
    &lt;artifactId&gt;...old stuff...&lt;/artifactId&gt;
    &lt;version&gt;...ancient...&lt;/version&gt;
    &lt;exclusions&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;log4j&lt;/groupId&gt;
            &lt;artifactId&gt;log4j&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
            &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
        &lt;/exclusion&gt;
    &lt;/exclusions&gt;
&lt;/dependency&gt;</pre> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
 <p style="margin-bottom: 1em; border: 0px; line-height: inherit; font-family: Arial, 'Helvetica Neue', Helvetica, sans-serif; font-size: 15px; vertical-align: baseline; clear: both; color: #242729;">&nbsp;</p> 
 <p>&nbsp;</p> 
</div>