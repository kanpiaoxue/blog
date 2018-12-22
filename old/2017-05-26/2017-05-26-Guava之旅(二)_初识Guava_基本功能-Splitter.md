#Guava之旅（二）：初识Guava，基本功能-Splitter
###发表时间：2017-05-26
###分类：java,guava
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2085720" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2085720</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>上一篇的Guava文章，提到了Joiner。这个小结将会讲到一个与他有逆向操作的类：Splitter。</p> 
 <p>Splitter 提供将字符串生产List列表的功能。</p> 
 <p>下面给出测试类：</p> 
 <pre name="code" class="java">import org.kanpiaoxue.util.Util;

import com.google.common.base.Splitter;

import java.util.List;
import java.util.Map;
import java.util.regex.Pattern;

public class UsingtheSplitterClass_02 {

    public static void main(String[] args) throws Exception {
        UsingtheSplitterClass_02 obj = new UsingtheSplitterClass_02();
        obj.test();

    }

    /**
     * &lt;pre&gt;
     * &lt;/pre&gt;
     */
    private void test() throws Exception {
        /**
         * &lt;pre&gt;
         * Splitter 的基本用法，使用指定的字符 | 来处理字符串，生成可迭代的Iterable
         * // output : 
         * hello
         * world
         * test
         * &lt;/pre&gt;
         */
        Iterable&lt;String&gt; it = Splitter.on('|').split("hello|world|test");
        for (String str : it) {
            System.out.println(str);
        }
        Util.print();

        /**
         * &lt;pre&gt;
         * 使用 trimResults() 方法对每个元素去掉左右空格。
         * // output : 
         * hello
         * world
         * test
         * &lt;/pre&gt;
         */
        List&lt;String&gt; list = Splitter.on('|').trimResults().splitToList("hello|world| test ");
        for (String str : list) {
            System.out.println(str);
        }
        Util.print();

        /**
         * &lt;pre&gt;
         *  fixedLength(2)方法对指定的字符串"0102030405060708091011121314"按照步长是2来生成list
         *  // output : 
         * 01
         * 02
         * 03
         * 04
         * 05
         * 06
         * 07
         * 08
         * 09
         * 10
         * 11
         * 12
         * 13
         * 14
         * &lt;/pre&gt;
         */
        list = Splitter.fixedLength(2).splitToList("0102030405060708091011121314");
        for (String str : list) {
            System.out.println(str);
        }
        Util.print();

        /**
         * &lt;pre&gt;
         * 使用 limit(3) 方法来限制分割的元素为3个。
         * // output :
         *   01
         * 02
         * 030405060708091011121314
         * &lt;/pre&gt;
         */
        list = Splitter.fixedLength(2).limit(3).splitToList("0102030405060708091011121314");
        for (String str : list) {
            System.out.println(str);
        }
        Util.print();

        /**
         * &lt;pre&gt;
         * 使用 onPattern("[a-z]") 的方法，用知道的正则表达式[a-z]来生成list，
         * 用 omitEmptyStrings() 方法来忽略那些空字符串。
         * // output :
         * 0102
         * 4
         * 6070
         * 314
         * &lt;/pre&gt;
         */
        list = Splitter.onPattern("[a-z]").omitEmptyStrings()
                .splitToList("0102add4max6070kanpiaoxue314");
        for (String str : list) {
            System.out.println(str);
        }
        Util.print();
        /**
         * &lt;pre&gt;
         * 使用on(Pattern separatorPattern)的方法，用知道的正则表达式[a-z]来生成list，
         * 用 omitEmptyStrings() 方法来忽略那些空字符串。
         * // output :
         * 0102
         * 4
         * 6070
         * 314
         * &lt;/pre&gt;
         */
        Pattern pattern = Pattern.compile("[a-z]");
        list = Splitter.on(pattern).omitEmptyStrings().splitToList("0102add4max6070kanpiaoxue314");
        for (String str : list) {
            System.out.println(str);
        }
        Util.print();

        /**
         * &lt;pre&gt;
         * 使用 omitEmptyStrings() 方法来忽略掉空字符串的元素
         * // output :
         * [hello, world, test, last]
         * &lt;/pre&gt;
         */
        Splitter splitter = Splitter.on('|').trimResults().omitEmptyStrings();
        list = splitter.splitToList("hello | world | test ||| | last");
        System.out.println(list);
        Util.print();

        /**
         * &lt;pre&gt;
         * 按照指定的格式，生成Map对象
         * // output :
         * {Washington D.C=Redskins, New York City=Giants, Philadelphia=Eagles, Dallas=Cowboys}
         * &lt;/pre&gt;
         */
        Splitter.MapSplitter mapSplitter = Splitter.on("#").withKeyValueSeparator("=");
        String startString = "Washington D.C=Redskins#New York City=Giants#Philadelphia=Eagles#Dallas=Cowboys";
        Map&lt;String, String&gt; map = mapSplitter.split(startString);
        System.out.println(map);
        Util.print();
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>