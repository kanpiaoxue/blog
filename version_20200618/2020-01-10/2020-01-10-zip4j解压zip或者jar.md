#zip4j解压zip或者jar
###发表时间：2020-01-10
###分类：zip4j,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2511924" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2511924</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：&nbsp;<a href="https://stackoverflow.com/questions/9324933/what-is-a-good-java-library-to-zip-unzip-files">https://stackoverflow.com/questions/9324933/what-is-a-good-java-library-to-zip-unzip-files</a></p> 
 <pre name="code" class="xml">&lt;!-- https://mvnrepository.com/artifact/net.lingala.zip4j/zip4j --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;net.lingala.zip4j&lt;/groupId&gt;
    &lt;artifactId&gt;zip4j&lt;/artifactId&gt;
    &lt;version&gt;2.3.0&lt;/version&gt;
&lt;/dependency&gt;
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import net.lingala.zip4j.exception.ZipException;
import net.lingala.zip4j.core.ZipFile;


public static void unzip(){
    String source = "some/compressed/file.zip";
    String destination = "some/destination/folder";
    String password = "password";

    try {
         ZipFile zipFile = new ZipFile(source);
         if (zipFile.isEncrypted()) {
            zipFile.setPassword(password);
         }
         zipFile.extractAll(destination);
    } catch (ZipException e) {
        e.printStackTrace();
    }
}</pre> 
 <p>&nbsp;</p> 
</div>