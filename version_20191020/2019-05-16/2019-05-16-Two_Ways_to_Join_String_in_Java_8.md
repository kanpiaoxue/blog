#Two Ways to Join String in Java 8
###发表时间：2019-05-16
###分类：java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2440990" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2440990</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>参考地址：&nbsp;<a href="https://dzone.com/articles/two-ways-to-join-string-in-java-8-stringjoiner-and?edition=479269&amp;utm_source=Daily%20Digest&amp;utm_medium=email&amp;utm_campaign=Daily%20Digest%202019-05-15">https://dzone.com/articles/two-ways-to-join-string-in-java-8-stringjoiner-and?edition=479269&amp;utm_source=Daily%20Digest&amp;utm_medium=email&amp;utm_campaign=Daily%20Digest%202019-05-15</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package test;
import java.util.Arrays;
import java.util.List;
import java.util.StringJoiner;
/**
 * Java program      ADVERTISEMENT                           to show how to join String in Java 8.
 * There are two ways to do that in Java 8, by using StringJoiner or
 * by using join() method of String class.
 * @author Javin
 */
public class Test {
    public static void main(String args[]) {
        // StringJoiner can join multiple String using any delimiter
        // Let's create a CSV String by joining Stirng using comma
        StringJoiner joiner = new StringJoiner(",");
        joiner.add("one");
        joiner.add("two");
        joiner.add("three");
        System.out.println("Comma separated String : " + joiner.toString());
        // You can combine all three lines into one because
        // StringJoiner provides a fluent interface
        StringJoiner delimitedString = new StringJoiner("|").add("id").add("name"); 
        System.out.println("Pipe delimited String : " + delimitedString);
        // 2nd Example: You can also join String by String.join() method
        // By far, this is the most convenient method to join Strings
        // in Java.    
        String csv = String.join(":", "abc", "bcd", "def");
        System.out.println("colon separated String : " + csv);
        // You can even use String.join() method to join contents of
        // ArrayList, Array, LinkedList or any collection, actually
        // any container which implements Iterable interface
        List mylist = Arrays.asList("London", "Paris", "NewYork");
        String joined = String.join("||", mylist);
        System.out.println("Joined String : " + joined);  
    }
}
Output
Comma separated String : one,two,three
Pipe delimited String : id|name
colon separated String : abc:bcd:def
Joined String : London||Paris||NewYork</pre> 
 <p>&nbsp;</p> 
</div>