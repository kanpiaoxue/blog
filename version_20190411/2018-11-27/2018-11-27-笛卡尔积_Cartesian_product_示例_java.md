#笛卡尔积：Cartesian product 示例:java
###发表时间：2018-11-27
###分类：算法,java,经验,笛卡尔积
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434408" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434408</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>笛卡尔积：&nbsp;<a href="https://baike.baidu.com/item/%E7%AC%9B%E5%8D%A1%E5%B0%94%E4%B9%98%E7%A7%AF/6323173?fr=aladdin">https://baike.baidu.com/item/%E7%AC%9B%E5%8D%A1%E5%B0%94%E4%B9%98%E7%A7%AF/6323173?fr=aladdin</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.apache.commons.collections4.CollectionUtils;

import com.google.common.base.Joiner;
import com.google.common.base.Preconditions;
import com.google.common.collect.Lists;

import java.util.LinkedList;
import java.util.List;
import java.util.stream.Collectors;

/**
 * CartesianProductUtils.java
 *
 * @author kanpiaoxue
 * @version 1.0
 *          Create Time 2018年11月27日 下午10:28:50
 *          Description : 笛卡尔积：Cartesian product 工具类
 */
public class CartesianProductUtils {

    /**
     *
     * @param datas
     *            笛卡尔积维度数据
     * @return 笛卡尔积结果
     * @author kanpiaoxue
     * @CreateTime: 2018/11/28 10:12:21
     * @Description: 根据笛卡尔积维度数据计算笛卡尔积结果
     *
     *               &lt;pre&gt;
     *               List&lt;List&lt;String&gt;&gt; datas = Lists.newArrayList();
     *               List&lt;String&gt; a = Lists.newArrayList("A", "B");
     *               datas.add(a);
     *               List&lt;String&gt; b = Lists.newArrayList("C", "D", "E");
     *               datas.add(b);
     *               List&lt;String&gt; c = Lists.newArrayList("F", "G");
     *               datas.add(c);
     *               List&lt;String&gt; d = Lists.newArrayList("H", "I", "J", "K");
     *               datas.add(d);
     *
     *               List&lt;List&lt;String&gt;&gt; rs = cartesianProduct(datas);
     *               rs.forEach(System.out::println);
     *               ==================== output ====================
     *               [A, C, F, H]
     *               [A, C, F, I]
     *               [A, C, F, J]
     *               [A, C, F, K]
     *               [A, C, G, H]
     *               [A, C, G, I]
     *               [A, C, G, J]
     *               [A, C, G, K]
     *               [A, D, F, H]
     *               [A, D, F, I]
     *               [A, D, F, J]
     *               [A, D, F, K]
     *               [A, D, G, H]
     *               [A, D, G, I]
     *               [A, D, G, J]
     *               [A, D, G, K]
     *               [A, E, F, H]
     *               [A, E, F, I]
     *               [A, E, F, J]
     *               [A, E, F, K]
     *               [A, E, G, H]
     *               [A, E, G, I]
     *               [A, E, G, J]
     *               [A, E, G, K]
     *               [B, C, F, H]
     *               [B, C, F, I]
     *               [B, C, F, J]
     *               [B, C, F, K]
     *               [B, C, G, H]
     *               [B, C, G, I]
     *               [B, C, G, J]
     *               [B, C, G, K]
     *               [B, D, F, H]
     *               [B, D, F, I]
     *               [B, D, F, J]
     *               [B, D, F, K]
     *               [B, D, G, H]
     *               [B, D, G, I]
     *               [B, D, G, J]
     *               [B, D, G, K]
     *               [B, E, F, H]
     *               [B, E, F, I]
     *               [B, E, F, J]
     *               [B, E, F, K]
     *               [B, E, G, H]
     *               [B, E, G, I]
     *               [B, E, G, J]
     *               [B, E, G, K]
     *               &lt;/pre&gt;
     */
    public static &lt;T&gt; List&lt;List&lt;T&gt;&gt; cartesianProduct(List&lt;List&lt;T&gt;&gt; datas) {
        if (CollectionUtils.isEmpty(datas)) {
            // 如果为空列表，返回空列表
            return Lists.newArrayList();
        }
        // 使用 LinkedList 的链表特性
        LinkedList&lt;List&lt;T&gt;&gt; dims = Lists.newLinkedList(datas);
        // LinkedList 中取出第一个元素作为起始维度
        List&lt;List&lt;T&gt;&gt; startDim = dims.poll().stream().map(data -&gt; {
            return Lists.newArrayList(data);
        }).collect(Collectors.toList());

        List&lt;List&lt;T&gt;&gt; result = Lists.newArrayList();
        recursion(startDim, dims, result);
        return result;
    }

    /**
     * @param datas
     *            笛卡尔积维度集合
     * @return 维度数量（层级）
     * @author kanpiaoxue
     *         Create Time 2018年11月28日 上午8:34:08
     *         Description : 计算得到笛卡尔积维度集合的维度数量（层级）
     */
    public static &lt;T&gt; int cartesianProductSize(List&lt;List&lt;T&gt;&gt; datas) {
        if (CollectionUtils.isEmpty(datas)) {
            return 0;
        }
        int size = 1;
        for (List&lt;T&gt; data : datas) {
            int tempSize = CollectionUtils.isNotEmpty(data) ? data.size() : 1;
            size *= tempSize;
        }
        return size;
    }

    /**
     * @param separator
     *            分隔符
     * @param datas
     *            笛卡尔积维度集合
     * @return 拼接的字符串
     * @author kanpiaoxue
     *         Create Time 2018年11月28日 上午8:35:47
     *         Description : 将各个维度使用分隔符进行拼接
     */
    public static &lt;T&gt; List&lt;String&gt; join(String separator, List&lt;List&lt;T&gt;&gt; datas) {
        Preconditions.checkNotNull(separator, "separator is null");
        if (CollectionUtils.isEmpty(datas)) {
            return Lists.newArrayList();
        }
        String tmpSeparator = separator.trim();
        return datas.stream().map(e -&gt; {
            return Joiner.on(tmpSeparator).skipNulls().join(e);
        }).collect(Collectors.toList());
    }

    /**
     * @param args
     * @author kanpiaoxue
     *         Create Time 2018年11月27日 下午10:28:51
     */
    public static void main(String[] args) {
        List&lt;List&lt;String&gt;&gt; datas = Lists.newArrayList();
        List&lt;String&gt; a = Lists.newArrayList("A", "B");
        datas.add(a);
        List&lt;String&gt; b = Lists.newArrayList("C", "D", "E");
        datas.add(b);
        List&lt;String&gt; c = Lists.newArrayList("F", "G");
        datas.add(c);
        List&lt;String&gt; d = Lists.newArrayList("H", "I", "J", "K");
        datas.add(d);

        List&lt;List&lt;String&gt;&gt; rs = cartesianProduct(datas);
        System.out.println("result:" + rs);
        rs.forEach(System.out::println);

        int cartesianProductSize = cartesianProductSize(datas);
        System.out.println("cartesianProductSize:" + cartesianProductSize);
        System.out.println("rs.size:" + rs.size());

        join("=", rs).forEach(System.out::println);
    }

    /**
     * @param start
     *            开始维度：笛卡尔积的第一个集合
     * @param leftDatas
     *            剩余维度：笛卡尔积剩下的其他集合
     * @param result
     *            结果
     * @author kanpiaoxue
     *         Create Time 2018年11月28日 上午8:27:05
     *         Description : 递归求取笛卡尔积
     */
    private static &lt;T&gt; void recursion(List&lt;List&lt;T&gt;&gt; start, LinkedList&lt;List&lt;T&gt;&gt; leftDatas,
            List&lt;List&lt;T&gt;&gt; result) {
        if (!leftDatas.isEmpty()) {
            List&lt;T&gt; leftElement = leftDatas.poll();
            List&lt;List&lt;T&gt;&gt; newStart = start.stream().flatMap(startElement -&gt; {
                return leftElement.stream().map(e -&gt; {
                    List&lt;T&gt; tmpList = Lists.newArrayList(startElement);
                    tmpList.add(e);
                    return tmpList;
                });
            }).collect(Collectors.toList());
            recursion(newStart, leftDatas, result);
        } else {
            result.addAll(start);
        }
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  === output: 写道
 </div> 
 <div class="quote_div">
  result:[[A, C, F, H], [A, C, F, I], [A, C, F, J], [A, C, F, K], [A, C, G, H], [A, C, G, I], [A, C, G, J], [A, C, G, K], [A, D, F, H], [A, D, F, I], [A, D, F, J], [A, D, F, K], [A, D, G, H], [A, D, G, I], [A, D, G, J], [A, D, G, K], [A, E, F, H], [A, E, F, I], [A, E, F, J], [A, E, F, K], [A, E, G, H], [A, E, G, I], [A, E, G, J], [A, E, G, K], [B, C, F, H], [B, C, F, I], [B, C, F, J], [B, C, F, K], [B, C, G, H], [B, C, G, I], [B, C, G, J], [B, C, G, K], [B, D, F, H], [B, D, F, I], [B, D, F, J], [B, D, F, K], [B, D, G, H], [B, D, G, I], [B, D, G, J], [B, D, G, K], [B, E, F, H], [B, E, F, I], [B, E, F, J], [B, E, F, K], [B, E, G, H], [B, E, G, I], [B, E, G, J], [B, E, G, K]]
  <br>[A, C, F, H]
  <br>[A, C, F, I]
  <br>[A, C, F, J]
  <br>[A, C, F, K]
  <br>[A, C, G, H]
  <br>[A, C, G, I]
  <br>[A, C, G, J]
  <br>[A, C, G, K]
  <br>[A, D, F, H]
  <br>[A, D, F, I]
  <br>[A, D, F, J]
  <br>[A, D, F, K]
  <br>[A, D, G, H]
  <br>[A, D, G, I]
  <br>[A, D, G, J]
  <br>[A, D, G, K]
  <br>[A, E, F, H]
  <br>[A, E, F, I]
  <br>[A, E, F, J]
  <br>[A, E, F, K]
  <br>[A, E, G, H]
  <br>[A, E, G, I]
  <br>[A, E, G, J]
  <br>[A, E, G, K]
  <br>[B, C, F, H]
  <br>[B, C, F, I]
  <br>[B, C, F, J]
  <br>[B, C, F, K]
  <br>[B, C, G, H]
  <br>[B, C, G, I]
  <br>[B, C, G, J]
  <br>[B, C, G, K]
  <br>[B, D, F, H]
  <br>[B, D, F, I]
  <br>[B, D, F, J]
  <br>[B, D, F, K]
  <br>[B, D, G, H]
  <br>[B, D, G, I]
  <br>[B, D, G, J]
  <br>[B, D, G, K]
  <br>[B, E, F, H]
  <br>[B, E, F, I]
  <br>[B, E, F, J]
  <br>[B, E, F, K]
  <br>[B, E, G, H]
  <br>[B, E, G, I]
  <br>[B, E, G, J]
  <br>[B, E, G, K]
  <br>cartesianProductSize:48
  <br>rs.size:48
  <br>A=C=F=H
  <br>A=C=F=I
  <br>A=C=F=J
  <br>A=C=F=K
  <br>A=C=G=H
  <br>A=C=G=I
  <br>A=C=G=J
  <br>A=C=G=K
  <br>A=D=F=H
  <br>A=D=F=I
  <br>A=D=F=J
  <br>A=D=F=K
  <br>A=D=G=H
  <br>A=D=G=I
  <br>A=D=G=J
  <br>A=D=G=K
  <br>A=E=F=H
  <br>A=E=F=I
  <br>A=E=F=J
  <br>A=E=F=K
  <br>A=E=G=H
  <br>A=E=G=I
  <br>A=E=G=J
  <br>A=E=G=K
  <br>B=C=F=H
  <br>B=C=F=I
  <br>B=C=F=J
  <br>B=C=F=K
  <br>B=C=G=H
  <br>B=C=G=I
  <br>B=C=G=J
  <br>B=C=G=K
  <br>B=D=F=H
  <br>B=D=F=I
  <br>B=D=F=J
  <br>B=D=F=K
  <br>B=D=G=H
  <br>B=D=G=I
  <br>B=D=G=J
  <br>B=D=G=K
  <br>B=E=F=H
  <br>B=E=F=I
  <br>B=E=F=J
  <br>B=E=F=K
  <br>B=E=G=H
  <br>B=E=G=I
  <br>B=E=G=J
  <br>B=E=G=K
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p class="p1">guava 的 Sets 提供了笛卡尔积的计算能力。 它其实还提供了集合的并集、差集等一系列的集合操作。</p> 
 <pre name="code" class="java">import org.apache.commons.lang3.StringUtils;

import com.google.common.collect.ImmutableList;
import com.google.common.collect.ImmutableSet;
import com.google.common.collect.Lists;
import com.google.common.collect.Sets;

import java.util.List;
import java.util.Set;

/**
 * @ClassName: TestAll
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/04/03 17:54:27
 */
public class TestAll {

    /**
     *
     * @param args
     * @author kanpiaoxue
     * @CreateTime: 2019/04/03 17:54:27
     */
    public static void main(String[] args) {
        // guava 的 Sets 提供了笛卡尔积的计算能力。 它其实还提供了集合的并集、差集等一系列的集合操作。
        Set&lt;List&lt;Object&gt;&gt; rs = Sets.cartesianProduct(ImmutableList.of(ImmutableSet.of(1, 2),
                ImmutableSet.of("A", "B", "C"), ImmutableSet.of("e", "f", "g")));
        rs.forEach(System.out::println);

        System.out.println(StringUtils.repeat("=", 100));

        rs = Sets.cartesianProduct(Lists.newArrayList(Sets.newLinkedHashSet(Lists.newArrayList(1, 2)),
                Sets.newLinkedHashSet(Lists.newArrayList("A", "B", "C")),
                Sets.newLinkedHashSet(Lists.newArrayList("e", "f"))));

        rs.forEach(System.out::println);
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>输出结果：</p> 
 <div class="quote_div">
  [1, A, e]
  <br>[1, A, f]
  <br>[1, A, g]
  <br>[1, B, e]
  <br>[1, B, f]
  <br>[1, B, g]
  <br>[1, C, e]
  <br>[1, C, f]
  <br>[1, C, g]
  <br>[2, A, e]
  <br>[2, A, f]
  <br>[2, A, g]
  <br>[2, B, e]
  <br>[2, B, f]
  <br>[2, B, g]
  <br>[2, C, e]
  <br>[2, C, f]
  <br>[2, C, g]
  <br>==========================================================================
  <br>[1, A, e]
  <br>[1, A, f]
  <br>[1, B, e]
  <br>[1, B, f]
  <br>[1, C, e]
  <br>[1, C, f]
  <br>[2, A, e]
  <br>[2, A, f]
  <br>[2, B, e]
  <br>[2, B, f]
  <br>[2, C, e]
  <br>[2, C, f]
 </div> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>