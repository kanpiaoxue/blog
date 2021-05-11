#java Convert an Iterator to Iterable in Java
###发表时间：2020-05-20
###分类：java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2514232" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2514232</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料：&nbsp;<a href="https://www.techiedelight.com/convert-iterator-iterable-java/">https://www.techiedelight.com/convert-iterator-iterable-java/</a></p> 
 <p><span style="color: #222222; font-family: Menlo, monospace; font-size: 11px; white-space: pre-wrap;">1. Java 7 and before</span></p> 
 <pre name="code" class="java">import java.util.Arrays;
import java.util.Iterator;

// Program to Convert an Iterator to Iterable in Java
class IteratorUtils
{
	public static&lt;T&gt; Iterable&lt;T&gt; iteratorToIterable(Iterator&lt;T&gt; iterator) {
		return new Iterable&lt;T&gt;() {
			@Override
			public Iterator&lt;T&gt; iterator() {
				return iterator;
			}
		};
	}

	public static void main(String[] args)
	{
		Iterator&lt;Integer&gt; iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();

		Iterable&lt;Integer&gt; iterable = iteratorToIterable(iterator);
		iterable.forEach(System.out::println);
	}
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p><span style="color: #222222; font-family: Menlo, monospace; font-size: 11px; white-space: pre-wrap;">2. Java 8 and above</span></p> 
 <pre name="code" class="java">import java.util.Arrays;
import java.util.Iterator;

// Program to Convert an Iterator to Iterable in Java 8 and above
class IteratorUtils
{
	public static&lt;T&gt; Iterable&lt;T&gt; iteratorToIterable(Iterator&lt;T&gt; iterator) {
		return () -&gt; iterator;
	}

	public static void main(String[] args)
	{
		Iterator&lt;Integer&gt; iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();

		Iterable&lt;Integer&gt; iterable = iteratorToIterable(iterator);
		iterable.forEach(System.out::println);
	}
}</pre> 
 <p><span style="color: #222222; font-family: Menlo, monospace; font-size: 11px; white-space: pre-wrap;">&nbsp;</span></p> 
 <p><span style="color: #222222; font-family: Menlo, monospace; font-size: 11px; white-space: pre-wrap;">3. Converting Iterator to Spliterators</span></p> 
 <pre name="code" class="java">import java.util.Arrays;
import java.util.Iterator;
import java.util.Spliterators;
import java.util.stream.Collectors;
import java.util.stream.StreamSupport;

// Program to Convert an Iterator to Iterable in Java
class IteratorUtils
{
	private static &lt;T&gt; Iterable&lt;T&gt; iteratorToIterable(Iterator&lt;T&gt; iterator)
	{
		// 1. Convert the iterator into a Spliterator
		// 2. Convert the spliterator into a sequential stream
		// 3. Convert the stream to an iterable
		return StreamSupport
					.stream(Spliterators.spliteratorUnknownSize(iterator, 0),
							false)
					.collect(Collectors.toList());
	}

	public static void main(String[] args)
	{
		Iterator&lt;Integer&gt; iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();

		Iterable&lt;Integer&gt; iterable = iteratorToIterable(iterator);
		iterable.forEach(System.out::println);
	}
}</pre> 
 <p><span style="color: #222222; font-family: Menlo, monospace; font-size: 11px; white-space: pre-wrap;">&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>