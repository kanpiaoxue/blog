#Guava之旅（三）：初识Guava，基本功能-Strings
###发表时间：2017-05-26
###分类：java,guava
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2085727" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2085727</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>下面是对Strings 这个工具方法使用的Example：</p> 
 <pre name="code" class="java">import org.kanpiaoxue.util.Util;

import com.google.common.base.Strings;

/**
 * &lt;pre&gt;
 * UsingTheStringsClass_04.java
 * @author xuepeng01&lt;br&gt;
 * @version 1.0
 * Create Time 2014年6月16日 下午1:59:10&lt;br&gt;
 * Description :
 * &lt;/pre&gt;
 */
public class UsingTheStringsClass_04 {

    /**
     * &lt;pre&gt;
     * @param args
     * &lt;/pre&gt;
     * 
     * @throws Exception
     */
    public static void main(String[] args) throws Exception {
        UsingTheStringsClass_04 obj = new UsingTheStringsClass_04();
        obj.test();

    }

    /**
     * &lt;pre&gt;
     * &lt;/pre&gt;
     */
    private void test() throws Exception {
        /**
         * &lt;pre&gt;
         * public static String padEnd(String string, int minLength, char padChar)
         * Returns a string, of length at least minLength, consisting of string appended with as many copies of padChar as are necessary to reach that length
         * &lt;/pre&gt;
         */
        System.out.println("padEnd:" + Strings.padEnd("foo", 6, 'x'));
        // output: padEnd:fooxxx

        System.out.println("padEnd:" + Strings.padEnd("4.", 5, '0'));
        // output: padEnd:4.000

        System.out.println("padEnd:" + Strings.padEnd("2010", 3, '!'));
        // output: padEnd:2010
        Util.print();

        /**
         * &lt;pre&gt;
         * public static String padStart(String string, int minLength, char padChar)
         * Returns a string, of length at least minLength, consisting of string prepended with as many copies of padChar as are necessary to reach that length
         * &lt;/pre&gt;
         */
        System.out.println("padStart:" + Strings.padStart("1", 9, '0'));
        // output: padStart:000000001
        Util.print();

        /**
         * &lt;pre&gt;
         * public static String nullToEmpty(@Nullable String string) 
         * Returns the given string if it is non-null; the empty string otherwise.
         * &lt;/pre&gt;
         */
        System.out.println("nullToEmpty:" + Strings.nullToEmpty(null));
        // output: nullToEmpty:

        System.out.println("nullToEmpty:" + Strings.nullToEmpty("test"));
        // output: nullToEmpty:test
        Util.print();

        /**
         * &lt;pre&gt;
         * public static @Nullable String emptyToNull(@Nullable String string)
         * Returns the given string if it is nonempty; null otherwise.
         * &lt;/pre&gt;
         */
        System.out.println("emptyToNull:" + (Strings.emptyToNull("") == null));
        // output: emptyToNull:true

        System.out.println("emptyToNull:" + Strings.emptyToNull("test"));
        // output: emptyToNull:test
        Util.print();

        /**
         * &lt;pre&gt;
         * public static boolean isNullOrEmpty(@Nullable String string) 
         * Returns true if the given string is null or is the empty string.
         * &lt;/pre&gt;
         */
        System.out.println("isNullOrEmpty:" + Strings.isNullOrEmpty(""));
        // output: isNullOrEmpty:true

        System.out.println("isNullOrEmpty:" + Strings.isNullOrEmpty(null));
        // output: isNullOrEmpty:true

        System.out.println("isNullOrEmpty:" + Strings.isNullOrEmpty("hello"));
        // output: isNullOrEmpty:false
        Util.print();

        /**
         * &lt;pre&gt;
         * public static String commonPrefix(CharSequence a, CharSequence b)
         * Returns the longest string prefix such that a.toString().startsWith(prefix) &amp;&amp; b.toString().startsWith(prefix), taking care not to split surrogate pairs.
         * &lt;/pre&gt;
         */
        System.out.println("commonPrefix:" + Strings.commonPrefix("HelloWorld.txt", "HeHe.log"));
        // output: commonPrefix:He
        Util.print();

        /**
         * &lt;pre&gt;
         * public static String commonSuffix(CharSequence a, CharSequence b)
         * Returns the longest string suffix such that a.toString().endsWith(suffix) &amp;&amp; b.toString().endsWith(suffix), taking care not to split surrogate pairs. If a and b have no common suffix, returns the empty string.
         * &lt;/pre&gt;
         */
        System.out.println("commonSuffix:" + Strings.commonSuffix("HelloWorld.java", "HeHe.java"));
        // output: commonSuffix:.java
        Util.print();

        /**
         * &lt;pre&gt;
         *  public static String repeat(String string, int count) 
         *  Returns a string consisting of a specific number of concatenated copies of an input string. 
         *  For example, repeat("hey", 3) returns the string "heyheyhey".
         * &lt;/pre&gt;
         */
        System.out.println("repeat:" + Strings.repeat("=", 10));
        // output: repeat:==========
        Util.print();
    }

}</pre> 
 <p>&nbsp;</p> 
</div>