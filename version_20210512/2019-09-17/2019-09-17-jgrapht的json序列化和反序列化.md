#jgrapht的json序列化和反序列化
###发表时间：2019-09-17
###分类：jgrapht,java,graph
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2464029" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2464029</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public static void test025() throws Exception {
        /**
         * &lt;pre&gt;
         *          1
         *        |    |
         *        2    3
         *          |
         *          4
         *          |
         *          7
         * &lt;/pre&gt;
         */
        Graph&lt;Integer, DefaultEdge&gt; g = new DirectedAcyclicGraph&lt;Integer, DefaultEdge&gt;(DefaultEdge.class);
        g.addVertex(1);
        g.addVertex(2);
        g.addVertex(3);
        g.addVertex(4);
        g.addVertex(7);

        g.addEdge(1, 2);
        g.addEdge(1, 3);
        g.addEdge(2, 4);
        g.addEdge(3, 4);
        g.addEdge(4, 7);

        ComponentNameProvider&lt;Integer&gt; vertexIdProvider = new ComponentNameProvider&lt;Integer&gt;() {
            public String getName(Integer i) {
                return String.valueOf(i);
            }
        };

        GraphExporter&lt;Integer, DefaultEdge&gt; exporter =
                new JSONExporter&lt;Integer, DefaultEdge&gt;(vertexIdProvider);
        Writer writer = new StringWriter();
        exporter.exportGraph(g, writer);
        IOUtils.closeQuietly(writer);
        String json = writer.toString();
        System.out.println(json);
        // {"creator":"JGraphT JSON
        // Exporter","version":"1","nodes":[{"id":"1"},{"id":"2"},{"id":"3"},{"id":"4"},{"id":"7"}],"edges":[{"id":"1","source":"1","target":"2"},{"id":"2","source":"1","target":"3"},{"id":"3","source":"2","target":"4"},{"id":"4","source":"3","target":"4"},{"id":"5","source":"4","target":"7"}]}

        VertexProvider&lt;Integer&gt; vertexProvider = new VertexProvider&lt;Integer&gt;() {

            @Override
            public Integer buildVertex(String id, Map&lt;String, Attribute&gt; attributes) {
                return Integer.valueOf(id);
            }
        };
        EdgeProvider&lt;Integer, DefaultEdge&gt; edgeProvider = new EdgeProvider&lt;Integer, DefaultEdge&gt;() {

            @Override
            public DefaultEdge buildEdge(Integer from, Integer to, String label,
                    Map&lt;String, Attribute&gt; attributes) {
                Graph&lt;Integer, DefaultEdge&gt; tmpGraph =
                        new DirectedAcyclicGraph&lt;Integer, DefaultEdge&gt;(DefaultEdge.class);
                tmpGraph.addVertex(from);
                tmpGraph.addVertex(to);
                tmpGraph.addEdge(from, to);
                return tmpGraph.edgeSet().iterator().next();
            }
        };

        GraphImporter&lt;Integer, DefaultEdge&gt; importer =
                new JSONImporter&lt;Integer, DefaultEdge&gt;(vertexProvider, edgeProvider);

        Graph&lt;Integer, DefaultEdge&gt; g1 = new DirectedAcyclicGraph&lt;Integer, DefaultEdge&gt;(DefaultEdge.class);
        Reader reader = new StringReader(json);
        importer.importGraph(g1, reader);
        IOUtils.closeQuietly(reader);
        System.out.println(g1);
        // ([1, 2, 3, 4, 7], [(1,2), (1,3), (2,4), (3,4), (4,7)])

    }</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>