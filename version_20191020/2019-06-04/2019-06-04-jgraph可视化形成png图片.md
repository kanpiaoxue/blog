#jgraph可视化形成png图片
###发表时间：2019-06-04
###分类：jgrapht,java,graph
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2441612" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2441612</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>pom.xml</p> 
 <pre name="code" class="xml">&lt;jgrapht.version&gt;1.3.1&lt;/jgrapht.version&gt;

&lt;!-- https://mvnrepository.com/artifact/org.jgrapht/jgrapht-ext --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.jgrapht&lt;/groupId&gt;
    &lt;artifactId&gt;jgrapht-ext&lt;/artifactId&gt;
    &lt;version&gt;${jgrapht.version}&lt;/version&gt;
&lt;/dependency&gt;

&lt;dependency&gt;
    &lt;groupId&gt;org.jgrapht&lt;/groupId&gt;
    &lt;artifactId&gt;jgrapht-io&lt;/artifactId&gt;
    &lt;version&gt;${jgrapht.version}&lt;/version&gt;
&lt;/dependency&gt;

&lt;dependency&gt;
    &lt;groupId&gt;org.jgrapht&lt;/groupId&gt;
    &lt;artifactId&gt;jgrapht-core&lt;/artifactId&gt;
    &lt;version&gt;${jgrapht.version}&lt;/version&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>自定义Edge</p> 
 <pre name="code" class="java">public class UDFEdge extends DefaultEdge{
    
    /**
     * 
     */
    private static final long serialVersionUID = 8239849745413195857L;

    /**
     * 
     */
    public UDFEdge() {
        super();
    }

    @Override
    public String toString()
    {
        return StringUtils.EMPTY;
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>jgraph的图形化，画出png的图片。</p> 
 <pre name="code" class="java">   public static void drawGraph() throws Exception {

        File imgFile = new File(
                "temp/jgrapht/hello1.png");
        if (imgFile.exists()) {
            imgFile.delete();
        }
        imgFile.createNewFile();

        DefaultDirectedGraph&lt;String, UDFEdge&gt; g = new DefaultDirectedGraph&lt;String, UDFEdge&gt;(UDFEdge.class);

        List&lt;String&gt; vertices = IntStream.rangeClosed(1, 20).mapToObj(i -&gt; {
            return String.format("v%d", i);
        }).collect(Collectors.toList());

        Graphs.addAllVertices(g, vertices);

   

        
          g.addEdge("v1", "v2");
          g.addEdge("v2", "v3");
          g.addEdge("v2", "v4");
          g.addEdge("v3", "v5");
          g.addEdge("v2", "v5");
          
          g.addEdge("v5", "v6");
          g.addEdge("v6", "v7");
          g.addEdge("v6", "v8");
          g.addEdge("v6", "v9");
          g.addEdge("v6", "v10");
          g.addEdge("v8", "v11");
          g.addEdge("v8", "v12");
          g.addEdge("v8", "v13");
          g.addEdge("v14", "v13");
          g.addEdge("v15", "v13");
          g.addEdge("v13", "v16");
          g.addEdge("v16", "v17");
          g.addEdge("v16", "v18");
          g.addEdge("v16", "v19");
          g.addEdge("v20", "v19");
          g.addEdge("v4", "v13");
          g.addEdge("v4", "v20");
         

        JGraphXAdapter&lt;String, UDFEdge&gt; graphAdapter = new JGraphXAdapter&lt;String, UDFEdge&gt;(g);
        // mxIGraphLayout layout = new mxCircleLayout(graphAdapter);
        mxIGraphLayout layout = new mxHierarchicalLayout(graphAdapter);
        layout.execute(graphAdapter.getDefaultParent());

        BufferedImage image =
                mxCellRenderer.createBufferedImage(graphAdapter, null, 2, Color.WHITE, true, null);
        ImageIO.write(image, "PNG", imgFile);

    }</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>