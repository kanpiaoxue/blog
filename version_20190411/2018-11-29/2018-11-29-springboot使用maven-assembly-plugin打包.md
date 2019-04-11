#springboot使用maven-assembly-plugin打包
###发表时间：2018-11-29
###分类：springboot,Spring,java,经验,maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434508" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434508</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考材料：</p> 
 <p>1、<a href="https://www.cnblogs.com/littleatp/p/9278517.html">https://www.cnblogs.com/littleatp/p/9278517.html</a></p> 
 <p>2、<a href="https://www.jianshu.com/p/3bd850fcb488">https://www.jianshu.com/p/3bd850fcb488</a></p> 
 <p>&nbsp;</p> 
 <p>项目的目录结构：（忽略掉target目录）</p> 
 <pre name="code" class="java">helloWorld
├── pom.xml
└── src
 &nbsp;&nbsp; └── main
 &nbsp;&nbsp;  &nbsp;&nbsp; ├── assemble
 &nbsp;&nbsp;  &nbsp;&nbsp; │&nbsp;&nbsp; ├── package.xml
 &nbsp;&nbsp;  &nbsp;&nbsp; │&nbsp;&nbsp; └── start.sh
 &nbsp;&nbsp;  &nbsp;&nbsp; ├── java
 &nbsp;&nbsp;  &nbsp;&nbsp; │&nbsp;&nbsp; └── org
 &nbsp;&nbsp;  &nbsp;&nbsp; └── resources
 &nbsp;&nbsp;  &nbsp;&nbsp;     ├── application-dev.yml
 &nbsp;&nbsp;  &nbsp;&nbsp;     ├── application-prod.yml
 &nbsp;&nbsp;  &nbsp;&nbsp;     ├── application-test.yml
 &nbsp;&nbsp;  &nbsp;&nbsp;     └── application.yml</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>目标 zip 文件的结构：</p> 
 <pre name="code" class="java">.
├── config
│&nbsp;&nbsp; ├── application-dev.yml
│&nbsp;&nbsp; └── application.yml
├── helloWorld-0.0.1.jar
└── start.sh</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>pom.xml</p> 
 <pre name="code" class="java">&lt;!-- build start --&gt;
&lt;build&gt;
    &lt;plugins&gt;
        &lt;plugin&gt;
            &lt;groupId&gt;org.springframework.boot&lt;/groupId&gt;
            &lt;artifactId&gt;spring-boot-maven-plugin&lt;/artifactId&gt;
            &lt;executions&gt;
                &lt;execution&gt;
                    &lt;goals&gt;
                        &lt;goal&gt;repackage&lt;/goal&gt;
                    &lt;/goals&gt;
                &lt;/execution&gt;
            &lt;/executions&gt;
        &lt;/plugin&gt;
        &lt;plugin&gt;
            &lt;artifactId&gt;maven-assembly-plugin&lt;/artifactId&gt;
            &lt;configuration&gt;
                &lt;finalName&gt;helloWorld&lt;/finalName&gt;
                &lt;finalName&gt;${project.artifactId}-${project.version}&lt;/finalName&gt;
                &lt;appendAssemblyId&gt;false&lt;/appendAssemblyId&gt;
                &lt;descriptors&gt;
                    &lt;descriptor&gt;src/main/assemble/package.xml&lt;/descriptor&gt;
                &lt;/descriptors&gt;
            &lt;/configuration&gt;
            &lt;executions&gt;
                &lt;execution&gt;
                    &lt;id&gt;bundle&lt;/id&gt;
                    &lt;phase&gt;package&lt;/phase&gt;
                    &lt;goals&gt;
                        &lt;goal&gt;single&lt;/goal&gt;
                    &lt;/goals&gt;
                &lt;/execution&gt;
            &lt;/executions&gt;
        &lt;/plugin&gt;
    &lt;/plugins&gt;
&lt;/build&gt;
&lt;!-- build end --&gt;

&lt;profiles&gt;
    &lt;profile&gt;
        &lt;!-- mvn clean package -Pdev --&gt;
        &lt;id&gt;dev&lt;/id&gt;
        &lt;activation&gt;
            &lt;activeByDefault&gt;true&lt;/activeByDefault&gt;
        &lt;/activation&gt;
        &lt;properties&gt;
            &lt;environment&gt;dev&lt;/environment&gt;
        &lt;/properties&gt;
    &lt;/profile&gt;
    &lt;profile&gt;
        &lt;!-- mvn clean package -Ptest --&gt;
        &lt;id&gt;test&lt;/id&gt;
        &lt;properties&gt;
            &lt;environment&gt;test&lt;/environment&gt;
        &lt;/properties&gt;
    &lt;/profile&gt;
    &lt;profile&gt;
        &lt;!-- mvn clean package -Pprod --&gt;
        &lt;id&gt;prod&lt;/id&gt;
        &lt;properties&gt;
            &lt;environment&gt;prod&lt;/environment&gt;
        &lt;/properties&gt;
    &lt;/profile&gt;
&lt;/profiles&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>dev/package.xml： 这里只给出了dev 测试环境目录下面的配置，其他的test、prod的在pom.xml的profile中添加一下即可。</p> 
 <pre name="code" class="java">&lt;assembly xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/assembly-1.0.0.xsd"&gt;
    &lt;id&gt;package&lt;/id&gt;
    &lt;formats&gt;
        &lt;format&gt;zip&lt;/format&gt;
    &lt;/formats&gt;
    &lt;includeBaseDirectory&gt;true&lt;/includeBaseDirectory&gt;

    &lt;fileSets&gt;
        &lt;!-- shell file --&gt;
        &lt;!-- gump job file: ${environment} from pom.xml --&gt;
        &lt;fileSet&gt;
            &lt;directory&gt;src/main/assemble&lt;/directory&gt;
            &lt;includes&gt;
                &lt;include&gt;start.sh&lt;/include&gt;
            &lt;/includes&gt;
            &lt;outputDirectory&gt;/&lt;/outputDirectory&gt;
        &lt;/fileSet&gt;
        &lt;!-- config file: ${environment} from pom.xml --&gt;
        &lt;fileSet&gt;
            &lt;directory&gt;src/main/resources&lt;/directory&gt;
            &lt;includes&gt;
                &lt;include&gt;application.yml&lt;/include&gt;
                &lt;include&gt;application-${environment}.yml&lt;/include&gt;
            &lt;/includes&gt;
            &lt;outputDirectory&gt;/config&lt;/outputDirectory&gt;
        &lt;/fileSet&gt;
        &lt;!-- executable jar --&gt;
        &lt;fileSet&gt;
            &lt;directory&gt;${project.build.directory}&lt;/directory&gt;
            &lt;includes&gt;
                &lt;include&gt;${project.artifactId}-${project.version}.jar&lt;/include&gt;
            &lt;/includes&gt;
            &lt;outputDirectory&gt;/&lt;/outputDirectory&gt;
        &lt;/fileSet&gt;
    &lt;/fileSets&gt;
&lt;/assembly&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;打包命令：</p> 
 <pre name="code" class="java">mvn clean package -Pdev
#mvn clean package -Ptest
#mvn clean package -Pprod</pre> 
 <p>&nbsp;</p> 
</div>