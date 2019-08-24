#Guava之旅（一）：初识Guava，基本功能-Joiner
###发表时间：2017-05-26
###分类：java,guava
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2085508" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2085508</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;"><span>Guava 是啥？很多朋友都知道了，还有很多朋友不是很清楚。</span></p> 
 <p style="font-size: 14px;"><span>我这里就多唠叨几句，说说Guava的来源。</span></p> 
 <p style="font-size: 14px;"><span>Guava的中文意思是：<span style="font-family: arial, 宋体; line-height: 20px;">番石榴。业界的朋友称他为：瓜娃</span></span></p> 
 <p style="font-size: 14px;"><span><span>Guava源于Google的“Google Collections Library”项目，在它的基础上进行了扩展，涉及到现在Java的</span><span style="font-family: arial, 宋体;"><span>strings, <span>collections, concurrency, I/O, and reflection，提供了大量Java API没有提供的工具方法。很多朋友用过apache下面的commons的各种工具，如 StringUtils。Guava和这些工具类似。</span></span></span></span></p> 
 <p style="font-size: 14px;"><span><span style="font-family: arial, 宋体;"><span><span>Guava的API都经过很多开发者的使用，并且都进行了单元测试。它的可靠性和性能是得到保障的。</span></span></span></span></p> 
 <p style="font-size: 14px;"><span style="font-family: arial, 宋体;">Guava的下载地址：</span><a href="https://code.google.com/p/guava-libraries/"><span style="font-family: arial, 宋体;">https://code.google.</span>com/p/guava-libraries/</a></p> 
 <p style="font-size: 14px;">我这里采用的是Guava 17.0的版本。把下载下来的&nbsp;guava-17.0.jar 放到你的classpath下面，就可以使用了。如果采用的Maven来管理jar的依赖，Maven的 pom.xml 如下：</p> 
 <pre name="code" class="xml">&lt;dependency&gt;
  &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
  &lt;artifactId&gt;guava&lt;/artifactId&gt;
  &lt;version&gt;17.0&lt;/version&gt;
&lt;/dependency&gt;</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">下面步入正题，本小结的目标工具栏： Joiner</p> 
 <p style="font-size: 14px;">Joiner是一个常用工具类，用于将实现 Iterable<code style="font-size: 12px; line-height: 1.5;"> </code>接口的类，通过指定的字符或者字符串进行拼接。它提供了大量的静态方法来实现这个目标。参考下面的代码：</p> 
 <p style="font-size: 14px;">先给出一个公用类：Util.java 。我的程序中使用这个工具类来清晰的区分打印结果的边界。</p> 
 <pre name="code" class="java">import com.google.common.base.Strings;
public class Util {
    private Util(){}
    public static void print() {
        System.out.println(Strings.repeat("=", 100));
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;下面是Joiner的使用，以及API的说明：</p> 
 <pre name="code" class="java">import static com.google.common.base.Joiner.on;

import org.kanpiaoxue.utils.Util;

import com.google.common.collect.Lists;
import com.google.common.collect.Maps;

import java.io.IOException;
import java.util.List;
import java.util.Map;

public class UsingTheJoinerClass_01 {

    public static void main(String[] args) throws Exception {
        UsingTheJoinerClass_01 obj = new UsingTheJoinerClass_01();
        obj.test();
    }

    /**
     * &lt;pre&gt;
     * Joiner可以接受 Array/Iterable/可变变量作为join的参数
     * 提供的方法：
     * appendTo()
     * on()
     * join()
     * skipNulls()
     * useForNull()
     * withKeyValueSeparator()
     * 上面的这些方法有很多重载的版本
     * &lt;/pre&gt;
     */
    private void test() throws IOException {
        int count = 5;
        List&lt;String&gt; stirngList = createDemoList(count);
        // Joiner 的基本用法：用 | 进行拼接，同时忽略掉 null 的空值
        String rs1 = on('|').skipNulls().join(stirngList);
        System.out.println("Joiner base method: " + rs1);
        // output : Joiner base method: hello_1|hello_2|hello_4
        Util.print();

        // Joiner 采用 @ 符号进行拼接，对 null 的控制赋予“invalid value”的值
        rs1 = on('@').useForNull("invalid value").join(stirngList);
        System.out.println("join list:" + rs1);
        // output : join list:invalid value@hello_1@hello_2@invalid
        // value@hello_4
        Util.print();

        String[] arr = { "1", "3", "4", "43", null, "55" };
        // Joiner 对数组array的使用
        rs1 = on('=').skipNulls().join(arr);
        System.out.println("join array:" + rs1);
        // output : join array:1=3=4=43=55
        Util.print();

        StringBuilder stringBuilder = new StringBuilder("===");
        // Joiner 对StringBuilder的使用
        rs1 = on("|").skipNulls().appendTo(stringBuilder, "foo", "bar", "baz").toString();
        System.out.println("join StringBuilder with some String:" + rs1);
        // output : join StringBuilder with some String:===foo|bar|baz
        Util.print();

        StringBuilder stringBuilder1 = new StringBuilder();
        rs1 = on('*').skipNulls()
                .appendTo(stringBuilder1, new String[] { "hello", "world", null, "Green" })
                .toString();
        System.out.println("join StringBuilder with array:" + rs1);
        // output : join StringBuilder with array:hello*world*Green
        Util.print();

        Map&lt;String, String&gt; testMap = Maps.newLinkedHashMap();
        testMap.put("Washington D.C", "Redskins");
        testMap.put("New York City", "Giants");
        testMap.put("Dallas", "Cowboys");
        // Joiner 对Map的使用
        String returnedString = on("#").withKeyValueSeparator("=").join(testMap);
        System.out.println(returnedString);
        // output : Washington D.C=Redskins#New York City=Giants#Dallas=Cowboys
    }

    /**
     * &lt;pre&gt;
     * @param count 生成List的元素个数
     * @return 字符串的List
     * &lt;/pre&gt;
     */
    private List&lt;String&gt; createDemoList(int count) {
        List&lt;String&gt; list = Lists.newArrayList();
        for (int i = 0; i &lt; count; i++) {
            if (i % 3 == 0) {
                list.add(null);
            } else {
                list.add("hello_" + i);
            }
        }
        return list;
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;注意：一旦 Joiner 的实例被创建，它就是不可变的，也就是“线程安全”的。</p> 
 <p style="font-size: 14px;">&nbsp;============== 第一小节结束 ================================</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>