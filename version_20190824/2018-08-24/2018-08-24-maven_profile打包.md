#maven profile打包
###发表时间：2018-08-24
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2429292" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2429292</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;plugin&gt;
    &lt;artifactId&gt;maven-assembly-plugin&lt;/artifactId&gt;
    &lt;version&gt;3.1.0&lt;/version&gt;
    &lt;configuration&gt;
        &lt;finalName&gt;${jarFinalName}-${pom.version}&lt;/finalName&gt;
        &lt;appendAssemblyId&gt;false&lt;/appendAssemblyId&gt;
        &lt;descriptors&gt;
            &lt;descriptor&gt;${packageDescriptor}&lt;/descriptor&gt;
        &lt;/descriptors&gt;
    &lt;/configuration&gt;
    &lt;executions&gt;
        &lt;execution&gt;
            &lt;id&gt; make-assembly &lt;/id&gt;
            &lt;phase&gt;package&lt;/phase&gt;
            &lt;goals&gt;
                &lt;goal&gt;single&lt;/goal&gt;
            &lt;/goals&gt;
        &lt;/execution&gt;
    &lt;/executions&gt;
&lt;/plugin&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">&lt;profiles&gt;
    &lt;profile&gt;
        &lt;!-- mvn clean package -PsyncColumnIntegerIdx --&gt;
        &lt;id&gt;syncColumnIntegerIdx&lt;/id&gt;
        &lt;activation&gt;
            &lt;activeByDefault&gt;true&lt;/activeByDefault&gt;
        &lt;/activation&gt;
        &lt;properties&gt;
            &lt;packageDescriptor&gt;src/main/java/org/kanpiaoxue/hello/assemble/package.xml&lt;/packageDescriptor&gt;
            &lt;jarFinalName&gt;syncColumnIntegerIdx&lt;/jarFinalName&gt;
        &lt;/properties&gt;
    &lt;/profile&gt;
    &lt;profile&gt;
        &lt;!-- mvn clean package -PminuteReportStatistics --&gt;
        &lt;id&gt;minuteReportStatistics&lt;/id&gt;
        &lt;properties&gt;
            &lt;packageDescriptor&gt;src/main/java/org/kanpiaoxue/hello/minutereport/assemble/package.xml&lt;/packageDescriptor&gt;
            &lt;jarFinalName&gt;minuteReportStatistics&lt;/jarFinalName&gt;
        &lt;/properties&gt;
    &lt;/profile&gt;
&lt;/profiles&gt;</pre> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  maven打包 写道
 </div> 
 <div class="quote_div">
  mvn clean package -PminuteReportStatistics
 </div> 
 <p>&nbsp;</p> 
</div>