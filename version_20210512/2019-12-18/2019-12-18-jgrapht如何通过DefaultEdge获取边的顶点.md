#jgrapht如何通过DefaultEdge获取边的顶点
###发表时间：2019-12-18
###分类：jgrapht,java,graph
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2511219" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2511219</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考地址：<a href="https://stackoverflow.com/questions/14296463/protected-getsource-and-gettarget-methods-on-jgrapht-defaultedge-class">https://stackoverflow.com/questions/14296463/protected-getsource-and-gettarget-methods-on-jgrapht-defaultedge-class</a></p> 
 <p>&nbsp;</p> 
 <p>问题如下：</p> 
 <p>The methods getSource() and getTarget() of DefaultEdge on org.jgrapht.graph.DefaultEdge are protected.</p> 
 <pre name="code" class="java">import java.util.Set;

import org.jgrapht.UndirectedGraph;
import org.jgrapht.graph.DefaultEdge;
import org.jgrapht.graph.SimpleGraph;

public class TestEdges
{
    public static void main(String [] args)
    {
        UndirectedGraph&lt;String, DefaultEdge&gt; g =
            new SimpleGraph&lt;String, DefaultEdge&gt;(DefaultEdge.class);

        String A = "A";
        String B = "B";
        String C = "C";

        // add the vertices
        g.addVertex(A);
        g.addVertex(B);
        g.addVertex(C);

        g.addEdge(A, B);
        g.addEdge(B, C);
        g.addEdge(A, C);

        Set&lt;DefaultEdge&gt; edges = g.edgeSet();

        for(DefaultEdge edge : edges) {
            String v1   = edge.getSource(); // Error getSource() is protected method
            String v2   = edge.getTarget(); // Error getTarget() is protected method
        }
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>The "correct" method to access edges source and target, according to JGraphT mailing list is to use the method getEdgeSource(E) and getEdgeTarget(E) from the interface Interface Graph&lt;V,E&gt; of org.jgrapht</p> 
 <p>the modification of the code is then</p> 
 <pre name="code" class="java">for(DefaultEdge edge : edges) {
   String v1   = g.getEdgeSource(edge);
   String v2   = g.getEdgeTarget(edge);
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>