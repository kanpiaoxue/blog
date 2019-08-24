#Maven的-DskipTests和-Dmaven.test.skip=true的区别
###发表时间：2017-11-30
###分类：maven
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2401472" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2401472</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>mvn package进行install、package的时候，Maven会执行src/test/java中的JUnit单元测试代码，有时为了跳过测试，会使用参数-DskipTests和-Dmaven.test.skip=true，它们的主要区别是：</p> 
 <p>&nbsp;</p> 
 <p>-DskipTests，不执行测试用例，但编译测试用例类生成相应的class文件至target/test-classes下。</p> 
 <p>&nbsp;</p> 
 <p>-Dmaven.test.skip=true，不执行测试用例，也不编译测试用例类。</p> 
</div>