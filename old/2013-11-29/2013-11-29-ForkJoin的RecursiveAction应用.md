#ForkJoin的RecursiveAction应用
###发表时间：2013-11-29
###分类：经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1982836" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1982836</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>RecursiveAction的应用</p> 
 <pre name="code" class="java">//通用 divide-and-conquer 并行算法的伪代码。
                
// PSEUDOCODE
Result solve(Problem problem) { 
    if (problem.size &lt; SEQUENTIAL_THRESHOLD)
        return solveSequentially(problem);
    else {
        Result left, right;
        INVOKE-IN-PARALLEL { 
            left = solve(extractLeftHalf(problem));
            right = solve(extractRightHalf(problem));
        }
        return combine(left, right);
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;我自己写了一个例子：</p> 
 <pre name="code" class="java">import java.util.ArrayList;
import java.util.List;
import java.util.Random;
import java.util.concurrent.ForkJoinPool;
import java.util.concurrent.RecursiveAction;

/**
 * &lt;pre&gt;
 * @author kanpiaoxue
 * Date 2013-11-29
 * &lt;/pre&gt;
 */
public class DivideAndConquer extends RecursiveAction {

	private static final long serialVersionUID = 5349972192067990608L;
	private final List&lt;Integer&gt; datas;
	private final int threshold;
	private int result;

	public DivideAndConquer(List&lt;Integer&gt; datas, int level) {
		super();
		this.datas = datas;
		this.threshold = level;
	}

	public static int sum(List&lt;Integer&gt; list) {
		int sum = 0;
		for (Integer i : list) {
			sum += i;
		}
		return sum;
	}

	@Override
	protected void compute() {
		System.out
				.println(Thread.currentThread().getName() + " start to work.");
		if (datas.size() &lt; threshold) {
			result = sum(datas);
		} else {
			int toIndex = datas.size() / 2;
			DivideAndConquer left = new DivideAndConquer(datas.subList(0,
					toIndex), threshold);
			DivideAndConquer right = new DivideAndConquer(datas.subList(
					toIndex, datas.size()), threshold);
			invokeAll(left, right);
			result = Math.max(left.result, right.result);
		}
	}

	public int getResult() {
		return result;
	}

	private static List&lt;Integer&gt; createTestDatas(int count) {
		List&lt;Integer&gt; list = new ArrayList&lt;Integer&gt;();
		Random random = new Random();
		for (int i = 0; i &lt; count; i++) {
			list.add(random.nextInt(1000));
		}
		return list;
	}

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		int count = 100000;
		int level = count / 5;
		List&lt;Integer&gt; datas = createTestDatas(count);
		System.out.println("DivideAndConquer.main()");
		DivideAndConquer t = new DivideAndConquer(datas, level);
		ForkJoinPool pool = new ForkJoinPool(Runtime.getRuntime()
				.availableProcessors() * 4);
		long before = System.currentTimeMillis();
		pool.invoke(t);
		System.out.println("max:" + t.getResult() + ", it consumes "
				+ (System.currentTimeMillis() - before) + " ms.");
	}

}
</pre> 
 <p>&nbsp;</p> 
 <p>更多的内容请参考：</p> 
 <p><a href="http://www.ibm.com/developerworks/cn/java/j-lo-forkjoin/index.html">http://www.ibm.com/developerworks/cn/java/j-lo-forkjoin/index.html</a></p> 
 <p><a href="http://www.ibm.com/developerworks/cn/java/j-jtp11137.html">http://www.ibm.com/developerworks/cn/java/j-jtp11137.html</a></p> 
 <p><a href="http://www.ibm.com/developerworks/cn/java/j-jtp03048.html">http://www.ibm.com/developerworks/cn/java/j-jtp03048.html</a></p> 
</div>