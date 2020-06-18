#静态导入import static 及如何在eclipse中方便使用
###发表时间：2013-11-20
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1977862" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1977862</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>import导入，对于java程序员来肯定不陌生，作用主要是保持语义不变的基础上减少编程时键入的代码量。集成开发环境如eclipse什么的也都提供了方便的导入手段（Ctrl+Shift+O），所以除了构建路径上有多个同名类时需要特别指明一下以外一般都不用特别操心。直到今天才发现还有一个“静态导入”的概念，是JDK5.0的新特性，还真有点孤陋寡闻了。</p> 
 <p>静态导入，是对于import语句的加强，使其不仅能让你省略包名，还能省略静态方法/字段所在类的类名。也就是说，静态导入允许你在调用其它类中定义的静态成员时，忽略类名。</p> 
 <p>&nbsp; &nbsp;1: &nbsp;package test;</p> 
 <p>&nbsp; &nbsp;2: &nbsp;import static java.lang.Math.max;//导入了Math的max方法</p> 
 <p>&nbsp; &nbsp;3: &nbsp;public class StaticImportTest{</p> 
 <p>&nbsp; &nbsp;4: &nbsp; &nbsp; &nbsp;public static void main(String[] args) {</p> 
 <p>&nbsp; &nbsp;5: &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;System.out.println(max(1, 2));//不用写Math了</p> 
 <p>&nbsp; &nbsp;6: &nbsp; &nbsp; &nbsp;}</p> 
 <p>&nbsp; &nbsp;7: &nbsp;}</p> 
 <p>eclipse自动导入功能是不包含静态导入的，也就是说写代码的时候不能写个max然后Ctrl+Shift+O等着eclipse帮咱们加上"importstatic java.lang.Math.max;“的。不过也是，eclipse也不能到所有的类里面找一遍到底哪个类里有一个叫做max的方法，是吧。如果想让工具代劳一下怎么办呢，给eclipse一点提示吧。Window-&gt;Preferences-&gt;Java-&gt;Editor-&gt;Content Assist-&gt;Favorites页面里，增加你希望参与静态导入的类或类中的静态字段/方法。写代码的时候敲上max，然后Alt+/，eclipse会帮你补全静态导入的代码。当然了前提是开启静态导入选项Window-&gt;Preferences-&gt;Java-&gt;Editor-&gt;Content Assist页面选中Use static imports。对于那些特别常用的静态方法/字段，这么做也算方便了。</p> 
 <p>来源：&nbsp;<a style="font-size: 12px; line-height: 1.5;" href="http://blog.csdn.net/abbuggy/article/details/6571429">http://blog.csdn.net/abbuggy/article/details/6571429</a></p> 
</div>