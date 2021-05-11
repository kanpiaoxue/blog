#spring读取classpath下文件
###发表时间：2020-01-09
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2511881" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2511881</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>开发过程中，必不可少的需要读取文件，对于打包方式的不同，还会存在一些坑，比如以jar包方式部署时，文件都存在于jar包中，某些读取方式在开发工程中都可行，但是打包后，由于文件被保存在jar中，会导致读取失败。</p> 
 <p>　　这时就需要通过类加载器读取文件，类加载器可以读取jar包中的class类当然也可以读取jar包中的文件。</p> 
 <pre name="code" class="java">// 方法1：获取文件或流

this.getClass().getResource("/")+fileName;

this.getClass().getResourceAsStream(failName);

// 方法2：获取文件

File file = org.springframework.util.ResourceUtils.getFile("classpath:test.txt");

// 方法3：获取文件或流

ClassPathResource classPathResource = new ClassPathResource("test.txt");

classPathResource .getFile();

classPathResource .getInputStream();



// &gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt;&gt; 下面方法可以读取jar包下文件

假设resources目录下有一个test.txt文件，首先获得当前的类加载器，通过类加载器读取文件。



// 方法1

InputStream io = Thread.currentThread().getContextClassLoader().getResourceAsStream("test.txt");

// 方法2

InputStream io = getClass().getClassLoader().getResourceAsStream("test.txt");</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>注意：Spring工具类会对classpath路径做处理，类加载器不会对classpath做处理，因此使用类加载器读取文件，路径中不要添加classpath</p> 
 <p>&nbsp;</p> 
 <p>原文链接：https://blog.csdn.net/weixin_38229356/article/details/80783142</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>