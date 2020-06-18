#jgraph快速生成drawio可绘制图
###发表时间：2019-09-20
###分类：jgrapht,java,graph,drawio
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2470875" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2470875</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>使用java的jgrapht的库组织的图像快速可视化，该如何做呢？</p> 
 <p>这里给出一个简洁的办法。</p> 
 <p>工具：</p> 
 <p>1、java的graph的库：&nbsp;<a href="https://jgrapht.org/">https://jgrapht.org/</a></p> 
 <p>2、JavaScript的可视化在线图工具：<a href="https://www.draw.io/">https://www.draw.io/</a></p> 
 <p>&nbsp;</p> 
 <p>用于打印边的类</p> 
 <pre name="code" class="java">public class SimpleDefaultEdge extends DefaultEdge {

    /**
     *
     */
    private static final long serialVersionUID = 1870891835682617414L;

    @Override
    public Object getSource() {
        return super.getSource();
    }

    @Override
    public Object getTarget() {
        return super.getTarget();
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return String.format("%s-&gt;%s", this.getSource(), this.getTarget());
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>图的组织</p> 
 <pre name="code" class="java">public static void test026() throws Exception {
        Graph&lt;Integer, SimpleDefaultEdge&gt; dag =
                new DirectedAcyclicGraph&lt;Integer, SimpleDefaultEdge&gt;(SimpleDefaultEdge.class);
        /**
         * DAG的结构如下，有3个联通子图。
         *
         * &lt;pre&gt;
         *            1     9   10  11
         *        / |   | \ |       |
         *      2   3   4   5       12
         *        \ | / | /
         *          6   7
         *           \ /|
         *            8 13
         * &lt;/pre&gt;
         */
        IntStream.rangeClosed(1, 13).forEach(v -&gt; {
            dag.addVertex(v);
        });

        dag.addEdge(1, 2);
        dag.addEdge(1, 3);
        dag.addEdge(1, 4);
        dag.addEdge(1, 5);
        dag.addEdge(9, 5);

        dag.addEdge(2, 6);
        dag.addEdge(3, 6);
        dag.addEdge(4, 6);
        dag.addEdge(4, 7);
        dag.addEdge(5, 7);

        dag.addEdge(6, 8);
        dag.addEdge(7, 8);
        dag.addEdge(7, 13);

        dag.addEdge(11, 12);

        dag.edgeSet().forEach(e -&gt; {
            System.out.println(e);
        });

    }</pre> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  输出 写道
 </div> 
 <div class="quote_div">
  1-&gt;2
  <br>1-&gt;3
  <br>1-&gt;4
  <br>1-&gt;5
  <br>9-&gt;5
  <br>2-&gt;6
  <br>3-&gt;6
  <br>4-&gt;6
  <br>4-&gt;7
  <br>5-&gt;7
  <br>6-&gt;8
  <br>7-&gt;8
  <br>7-&gt;13
  <br>11-&gt;12
 </div> 
 <p>&nbsp;</p> 
 <p>进入&nbsp;<a href="https://www.draw.io/">https://www.draw.io/</a>&nbsp;找到菜单“调整图形” -&gt; “插入”-&gt; “高级”-&gt; “从文本...”。 在弹出的对话框里面的select下拉框里面选择“图标”，可以看见里面有范例代码如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  ;Example:
  <br>a-&gt;b
  <br>b-&gt;edge label-&gt;c
  <br>c-&gt;a
 </div> 
 <p>&nbsp;我们把刚刚java里面输出的内容更新到里面，如下：</p> 
 <div class="quote_title">
  写道
 </div> 
 <div class="quote_div">
  ;Example:
  <br>1-&gt;2
  <br>1-&gt;3
  <br>1-&gt;4
  <br>1-&gt;5
  <br>9-&gt;5
  <br>2-&gt;6
  <br>3-&gt;6
  <br>4-&gt;6
  <br>4-&gt;7
  <br>5-&gt;7
  <br>6-&gt;8
  <br>7-&gt;8
  <br>7-&gt;13
  <br>11-&gt;12
 </div> 
 <p>&nbsp;点击插入按钮，数据就从jgraph导入到drawio了，实现了可视化。</p> 
 <p>&nbsp;</p> 
 <p>可能导入之后的图形布局看着不是很舒服，可以进行调整。进入菜单“调整图形”-&gt;“布局”-&gt;"垂直流" ，可以调整布局。也可以在这里进行其他方式的布局调整。</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>