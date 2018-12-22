#guava的Graph示例
###发表时间：2017-08-11
###分类：java,guava
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2389411" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2389411</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public interface Node&lt;T&gt; {
    T get();
}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public interface Edge&lt;T&gt; {
    T get();
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class DataEntity implements Node&lt;DataEntity&gt; {

    private final String nameSpace;
    private final String entityName;

    public DataEntity(String nameSpace, String entityName) {
        super();
        this.nameSpace = nameSpace;
        this.entityName = entityName;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        DataEntity other = (DataEntity) obj;
        if (entityName == null) {
            if (other.entityName != null) {
                return false;
            }
        } else if (!entityName.equals(other.entityName)) {
            return false;
        }
        if (nameSpace == null) {
            if (other.nameSpace != null) {
                return false;
            }
        } else if (!nameSpace.equals(other.nameSpace)) {
            return false;
        }
        return true;
    }

    @Override
    public DataEntity get() {
        return this;
    }

    public String getEntityName() {
        return entityName;
    }

    public String getNameSpace() {
        return nameSpace;
    }

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((entityName == null) ? 0 : entityName.hashCode());
        result = prime * result + ((nameSpace == null) ? 0 : nameSpace.hashCode());
        return result;
    }

    @Override
    public String toString() {
        return "DataEntity [nameSpace=" + nameSpace + ", entityName=" + entityName + "]";
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class DataRelationShip implements Edge&lt;DataRelationShip&gt; {

    private final String sourceColumn;
    private final String targetColumn;

    public DataRelationShip(String sourceColumn, String targetColumn) {
        super();
        this.sourceColumn = sourceColumn;
        this.targetColumn = targetColumn;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        DataRelationShip other = (DataRelationShip) obj;
        if (sourceColumn == null) {
            if (other.sourceColumn != null) {
                return false;
            }
        } else if (!sourceColumn.equals(other.sourceColumn)) {
            return false;
        }
        if (targetColumn == null) {
            if (other.targetColumn != null) {
                return false;
            }
        } else if (!targetColumn.equals(other.targetColumn)) {
            return false;
        }
        return true;
    }

    @Override
    public DataRelationShip get() {
        return this;
    }

    public String getSourceColumn() {
        return sourceColumn;
    }

    public String getTargetColumn() {
        return targetColumn;
    }

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((sourceColumn == null) ? 0 : sourceColumn.hashCode());
        result = prime * result + ((targetColumn == null) ? 0 : targetColumn.hashCode());
        return result;
    }

    @Override
    public String toString() {
        return "DataRelationShip [sourceColumn=" + sourceColumn + ", targetColumn=" + targetColumn + "]";
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class LearnGraphs {

    public static void main(String[] args) {
        test();
    }

    static void test() {

        /**
         * &lt;pre&gt;
         * Graph
         *           a  -&gt; c
         *              -&gt; b -&gt; d -&gt; e
         * &lt;/pre&gt;
         */
        MutableValueGraph&lt;Node&lt;DataEntity&gt;, Edge&lt;DataRelationShip&gt;&gt; graph =
                ValueGraphBuilder.directed().build();
        String nameSpace = "nameSpace";
        Node&lt;DataEntity&gt; a = new DataEntity(nameSpace, "a");
        Node&lt;DataEntity&gt; b = new DataEntity(nameSpace, "b");
        Node&lt;DataEntity&gt; c = new DataEntity(nameSpace, "c");
        Node&lt;DataEntity&gt; d = new DataEntity(nameSpace, "d");
        Node&lt;DataEntity&gt; e = new DataEntity(nameSpace, "e");

        Node&lt;DataEntity&gt; eClone = new DataEntity(nameSpace, "e");

        Edge&lt;DataRelationShip&gt; ab = new DataRelationShip("a", "b");
        Edge&lt;DataRelationShip&gt; ac = new DataRelationShip("a", "c");
        Edge&lt;DataRelationShip&gt; bd = new DataRelationShip("b", "d");
        Edge&lt;DataRelationShip&gt; de = new DataRelationShip("d", "e");
        // Edge&lt;DataRelationShip&gt; ea = new DataRelationShip("e", "a");

        putEdgeValue(graph, a, b, ab);
        putEdgeValue(graph, a, c, ac);
        putEdgeValue(graph, b, d, bd);
        putEdgeValue(graph, d, e, de);
        // putEdgeValue(graph, e, a, ea);

        System.out.println(graph.toString());
        System.out.println(Graphs.hasCycle(graph.asGraph()));
        System.out.println(graph.adjacentNodes(b));
        System.out.println(StringUtils.repeat("-", 100));
        System.out.println(graph.predecessors(a));
        System.out.println(graph.successors(a));
        System.out.println(StringUtils.repeat("-", 100));
        System.out.println(graph.predecessors(b));
        System.out.println(graph.successors(b));
        System.out.println(StringUtils.repeat("-", 100));
        System.out.println(graph.predecessors(eClone));
        System.out.println(graph.successors(eClone));

        /**
         * 
         * output:
         * 
         * &lt;pre&gt;
         * isDirected: true, allowsSelfLoops: false, nodes: [DataEntity [nameSpace=nameSpace, entityName=a], DataEntity [nameSpace=nameSpace, entityName=b], DataEntity [nameSpace=nameSpace, entityName=c], DataEntity [nameSpace=nameSpace, entityName=d], DataEntity [nameSpace=nameSpace, entityName=e]], edges: {&lt;DataEntity [nameSpace=nameSpace, entityName=a] -&gt; DataEntity [nameSpace=nameSpace, entityName=c]&gt;=DataRelationShip [sourceColumn=a, targetColumn=c], &lt;DataEntity [nameSpace=nameSpace, entityName=a] -&gt; DataEntity [nameSpace=nameSpace, entityName=b]&gt;=DataRelationShip [sourceColumn=a, targetColumn=b], &lt;DataEntity [nameSpace=nameSpace, entityName=b] -&gt; DataEntity [nameSpace=nameSpace, entityName=d]&gt;=DataRelationShip [sourceColumn=b, targetColumn=d], &lt;DataEntity [nameSpace=nameSpace, entityName=d] -&gt; DataEntity [nameSpace=nameSpace, entityName=e]&gt;=DataRelationShip [sourceColumn=d, targetColumn=e]}
         * false
         * [DataEntity [nameSpace=nameSpace, entityName=d], DataEntity [nameSpace=nameSpace, entityName=a]]
         * ----------------------------------------------------------------------------------------------------
         * []
         * [DataEntity [nameSpace=nameSpace, entityName=c], DataEntity [nameSpace=nameSpace, entityName=b]]
         * ----------------------------------------------------------------------------------------------------
         * [DataEntity [nameSpace=nameSpace, entityName=a]]
         * [DataEntity [nameSpace=nameSpace, entityName=d]]
         * ----------------------------------------------------------------------------------------------------
         * [DataEntity [nameSpace=nameSpace, entityName=d]]
         * []
         * 
         * &lt;/pre&gt;
         */

    }

    static void putEdgeValue(MutableValueGraph&lt;Node&lt;DataEntity&gt;, Edge&lt;DataRelationShip&gt;&gt; graph,
            Node&lt;DataEntity&gt; a, Node&lt;DataEntity&gt; b, Edge&lt;DataRelationShip&gt; ab) {
        graph.putEdgeValue(a, b, ab);
        Preconditions.checkArgument(!Graphs.hasCycle(graph.asGraph()),
                "from node:%s to node:%s with the edge:%s will form the cycle.", a, b, ab);
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>