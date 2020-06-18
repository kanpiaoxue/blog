#jgraph快速生成drawio可绘制图(2):CSV格式
###发表时间：2020-02-26
###分类：jgrapht,java,graph,drawio
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2512637" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2512637</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>官方文档：<a href="https://drawio-app.com/import-from-csv-to-drawio/">https://drawio-app.com/import-from-csv-to-drawio/</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class BaseLineObj {
    /**
     * Builder to build {@link BaseLineObj}.
     */
    public static final class Builder {
        private Integer flowId;
        private Integer queueLevel;

        private Builder() {
        }

        /**
         * Builder method of the builder.
         * 
         * @return built class
         */
        public BaseLineObj build() {
            return new BaseLineObj(this);
        }

        /**
         * Builder method for flowId parameter.
         * 
         * @param flowId
         *            field to set
         * @return builder
         */
        public Builder withFlowId(Integer flowId) {
            this.flowId = flowId;
            return this;
        }

        /**
         * Builder method for queueLevel parameter.
         * 
         * @param queueLevel
         *            field to set
         * @return builder
         */
        public Builder withQueueLevel(Integer queueLevel) {
            this.queueLevel = queueLevel;
            return this;
        }
    }

    private Integer flowId;

    private Integer queueLevel;

    /**
     *
     */
    public BaseLineObj() {
        super();
    }

    private BaseLineObj(Builder builder) {
        this.flowId = builder.flowId;
        this.queueLevel = builder.queueLevel;
    }

    /**
     * Creates builder to build {@link BaseLineObj}.
     * 
     * @return created builder
     */
    public static Builder builder() {
        return new Builder();
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#equals(java.lang.Object)
     */
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
        BaseLineObj other = (BaseLineObj) obj;
        if (flowId == null) {
            if (other.flowId != null) {
                return false;
            }
        } else if (!flowId.equals(other.flowId)) {
            return false;
        }
        return true;
    }

    /**
     * @return the flowId
     */
    public Integer getFlowId() {
        return flowId;
    }

    /**
     * @return the queueLevel
     */
    public Integer getQueueLevel() {
        return queueLevel;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((flowId == null) ? 0 : flowId.hashCode());
        return result;
    }

    /**
     * @param flowId
     *            the flowId to set
     */
    public void setFlowId(Integer flowId) {
        this.flowId = flowId;
    }

    /**
     * @param queueLevel
     *            the queueLevel to set
     */
    public void setQueueLevel(Integer queueLevel) {
        this.queueLevel = queueLevel;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return GsonUtils.toJSON(this);
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class CSVFormatRecord {

    /**
     * Builder to build {@link CSVFormatRecord}.
     */
    public static final class Builder {
        private String id;
        private String step;
        private String fill;
        private String stroke;
        private String shape;
        private String refs;

        private Builder() {
        }

        /**
         * Builder method of the builder.
         *
         * @return built class
         */
        public CSVFormatRecord build() {
            return new CSVFormatRecord(this);
        }

        /**
         * Builder method for fill parameter.
         *
         * @param fill
         *            field to set
         * @return builder
         */
        public Builder withFill(String fill) {
            this.fill = fill;
            return this;
        }

        /**
         * Builder method for id parameter.
         *
         * @param id
         *            field to set
         * @return builder
         */
        public Builder withId(String id) {
            this.id = id;
            return this;
        }

        /**
         * Builder method for refs parameter.
         *
         * @param refs
         *            field to set
         * @return builder
         */
        public Builder withRefs(String refs) {
            this.refs = refs;
            return this;
        }

        /**
         * Builder method for shape parameter.
         *
         * @param shape
         *            field to set
         * @return builder
         */
        public Builder withShape(String shape) {
            this.shape = shape;
            return this;
        }

        /**
         * Builder method for step parameter.
         *
         * @param step
         *            field to set
         * @return builder
         */
        public Builder withStep(String step) {
            this.step = step;
            return this;
        }

        /**
         * Builder method for stroke parameter.
         *
         * @param stroke
         *            field to set
         * @return builder
         */
        public Builder withStroke(String stroke) {
            this.stroke = stroke;
            return this;
        }
    }

    private String id;

    private String step;
    private String fill;
    private String stroke;
    private String shape;
    private String refs;

    /**
     *
     */
    public CSVFormatRecord() {
        super();
    }

    private CSVFormatRecord(Builder builder) {
        this.id = builder.id;
        this.step = builder.step;
        this.fill = builder.fill;
        this.stroke = builder.stroke;
        this.shape = builder.shape;
        this.refs = builder.refs;
    }

    /**
     * Creates builder to build {@link CSVFormatRecord}.
     *
     * @return created builder
     */
    public static Builder builder() {
        return new Builder();
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#equals(java.lang.Object)
     */
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
        CSVFormatRecord other = (CSVFormatRecord) obj;
        if (fill == null) {
            if (other.fill != null) {
                return false;
            }
        } else if (!fill.equals(other.fill)) {
            return false;
        }
        if (id == null) {
            if (other.id != null) {
                return false;
            }
        } else if (!id.equals(other.id)) {
            return false;
        }
        if (refs == null) {
            if (other.refs != null) {
                return false;
            }
        } else if (!refs.equals(other.refs)) {
            return false;
        }
        if (shape == null) {
            if (other.shape != null) {
                return false;
            }
        } else if (!shape.equals(other.shape)) {
            return false;
        }
        if (step == null) {
            if (other.step != null) {
                return false;
            }
        } else if (!step.equals(other.step)) {
            return false;
        }
        if (stroke == null) {
            if (other.stroke != null) {
                return false;
            }
        } else if (!stroke.equals(other.stroke)) {
            return false;
        }
        return true;
    }

    /**
     * @return the fill
     */
    public String getFill() {
        return fill;
    }

    /**
     * @return the id
     */
    public String getId() {
        return id;
    }

    /**
     * @return the refs
     */
    public String getRefs() {
        return refs;
    }

    /**
     * @return the shape
     */
    public String getShape() {
        return shape;
    }

    /**
     * @return the step
     */
    public String getStep() {
        return step;
    }

    /**
     * @return the stroke
     */
    public String getStroke() {
        return stroke;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((fill == null) ? 0 : fill.hashCode());
        result = prime * result + ((id == null) ? 0 : id.hashCode());
        result = prime * result + ((refs == null) ? 0 : refs.hashCode());
        result = prime * result + ((shape == null) ? 0 : shape.hashCode());
        result = prime * result + ((step == null) ? 0 : step.hashCode());
        result = prime * result + ((stroke == null) ? 0 : stroke.hashCode());
        return result;
    }

    /**
     * @param fill
     *            the fill to set
     */
    public void setFill(String fill) {
        this.fill = fill;
    }

    /**
     * @param id
     *            the id to set
     */
    public void setId(String id) {
        this.id = id;
    }

    /**
     * @param refs
     *            the refs to set
     */
    public void setRefs(String refs) {
        this.refs = refs;
    }

    /**
     * @param shape
     *            the shape to set
     */
    public void setShape(String shape) {
        this.shape = shape;
    }

    /**
     * @param step
     *            the step to set
     */
    public void setStep(String step) {
        this.step = step;
    }

    /**
     * @param stroke
     *            the stroke to set
     */
    public void setStroke(String stroke) {
        this.stroke = stroke;
    }

    public String toGraphCSV() {
        Preconditions.checkNotNull(id, "id is null");
        Preconditions.checkNotNull(step, "step is null");
        Preconditions.checkNotNull(fill, "fill is null");
        Preconditions.checkNotNull(stroke, "stroke is null");
        Preconditions.checkNotNull(shape, "shape is null");
        Preconditions.checkNotNull(refs, "refs is null");
        return Joiner.on(",").join(id, step, fill, stroke, shape, refs);
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return GsonUtils.toJSON(this);
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package test;
import org.apache.commons.collections.CollectionUtils;
import org.jgrapht.Graphs;
import org.jgrapht.graph.DefaultEdge;
import org.jgrapht.graph.DirectedAcyclicGraph;
import org.kanpiaoxue.code.KeyValue;

import com.google.common.base.Joiner;
import com.google.common.collect.Lists;
import com.google.common.collect.Maps;


import java.util.List;
import java.util.Map;
import java.util.Objects;
import java.util.function.Function;
import java.util.stream.Collectors;

/**
 * @ClassName: Test1
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/11/11 20:17:31
 * @Description:
 */
public class Test1 {

    private static final KeyValue&lt;String, String&gt; CURRENT_NODE_COLOR =
            new KeyValue&lt;String, String&gt;("#fff2cc", "#d6b656");

    private static final KeyValue&lt;String, String&gt; DEFAULT_NODE_COLOR =
            new KeyValue&lt;String, String&gt;("#dae8fc", "#6c8ebf");

    private static final Map&lt;Integer, KeyValue&lt;String, String&gt;&gt; COLOR_MAP = Maps.newHashMap();

    static {
        COLOR_MAP.put(1, DEFAULT_NODE_COLOR);
        COLOR_MAP.put(2, new KeyValue&lt;String, String&gt;("#d5e8d4", "#82b366"));
        COLOR_MAP.put(3, new KeyValue&lt;String, String&gt;("#f8cecc", "#b85450"));
    }

    private static List&lt;String&gt; CSV_HEADER = Lists.newArrayList();

    static {
        CSV_HEADER.add("## Hello World");
        CSV_HEADER.add("# label: %step%");
        CSV_HEADER.add("# style: shape=%shape%;fillColor=%fill%;strokeColor=%stroke%;");
        CSV_HEADER.add("# namespace: csvimport-");
        CSV_HEADER.add(
                "# connect: {\"from\":\"refs\", \"to\":\"id\", \"invert\":true, \"style\":\"curved=0;endArrow=blockThin;endFill=1;\"}");
        CSV_HEADER.add("# width: auto");
        CSV_HEADER.add("# height: auto");
        CSV_HEADER.add("# padding: 15");
        CSV_HEADER.add("# ignore: id,shape,fill,stroke,refs");
        CSV_HEADER.add("# nodespacing: 40");
        CSV_HEADER.add("# levelspacing: 100");
        CSV_HEADER.add("# edgespacing: 40");
        CSV_HEADER.add("# layout: auto");
        CSV_HEADER.add("## CSV starts under this line");
    }

    private static final List&lt;String&gt; HEADER_LIST = Lists.newArrayList("id,step,fill,stroke,shape,refs");

    /**
     *
     * @param args
     * @author kanpiaoxue * @CreateTime: 2019/05/20 10:43:16
     */
    public static void main(String[] args) throws Exception {
        test07();
    }

    public static void test07() throws Exception {
        BaseLineObj currentNode = BaseLineObj.builder().withFlowId(4).withQueueLevel(3).build();
        List&lt;String&gt; datas = buildDatas(currentNode);

        List&lt;String&gt; list = Lists.newArrayList();
        list.addAll(CSV_HEADER);
        list.addAll(HEADER_LIST);
        list.addAll(datas);

        System.out.println(Joiner.on("\n").skipNulls().join(list));

    }

    private static DirectedAcyclicGraph&lt;BaseLineObj, DefaultEdge&gt; buildDAG() {
        DirectedAcyclicGraph&lt;BaseLineObj, DefaultEdge&gt; g =
                new DirectedAcyclicGraph&lt;BaseLineObj, DefaultEdge&gt;(DefaultEdge.class);
        BaseLineObj o1 = BaseLineObj.builder().withFlowId(1).withQueueLevel(3).build();
        BaseLineObj o2 = BaseLineObj.builder().withFlowId(2).withQueueLevel(3).build();
        BaseLineObj o3 = BaseLineObj.builder().withFlowId(3).withQueueLevel(3).build();
        BaseLineObj o4 = BaseLineObj.builder().withFlowId(4).withQueueLevel(2).build();
        BaseLineObj o5 = BaseLineObj.builder().withFlowId(5).withQueueLevel(2).build();
        BaseLineObj o6 = BaseLineObj.builder().withFlowId(6).withQueueLevel(1).build();
        BaseLineObj o7 = BaseLineObj.builder().withFlowId(7).withQueueLevel(1).build();
        g.addVertex(o1);
        g.addVertex(o2);
        g.addVertex(o3);
        g.addVertex(o4);
        g.addVertex(o5);
        g.addVertex(o6);
        g.addVertex(o7);

        g.addEdge(o1, o2);
        g.addEdge(o1, o3);
        g.addEdge(o2, o4);
        g.addEdge(o5, o4);
        g.addEdge(o4, o6);
        g.addEdge(o6, o7);
        g.addEdge(o1, o7);
        return g;
    }

    private static List&lt;String&gt; buildDatas(BaseLineObj current) {
        DirectedAcyclicGraph&lt;BaseLineObj, DefaultEdge&gt; g = buildDAG();

        List&lt;CSVFormatRecord&gt; datas = g.vertexSet().stream().map(o -&gt; {
            List&lt;BaseLineObj&gt; successorListOf = Graphs.successorListOf(g, o);
            String refs = processRefs(successorListOf, BaseLineObj::getFlowId);

            KeyValue&lt;String, String&gt; kv =
                    current.equals(o) ? CURRENT_NODE_COLOR : processBaseLineColor(o.getQueueLevel());
            String fill = kv.getKey();
            String stroke = kv.getValue();

            return CSVFormatRecord.builder().withId(o.getFlowId().toString())
                    .withStep(String.format("\"flowId:%s,level:%s\"", o.getFlowId(), o.getQueueLevel()))
                    .withFill(fill).withStroke(stroke).withShape("rectangle").withRefs(refs).build();
        }).collect(Collectors.toList());

        List&lt;String&gt; rs = datas.stream().map(CSVFormatRecord::toGraphCSV).collect(Collectors.toList());
        return rs;

    }

    private static KeyValue&lt;String, String&gt; processBaseLineColor(Integer queueLevel) {
        KeyValue&lt;String, String&gt; obj = COLOR_MAP.get(queueLevel);
        if (Objects.isNull(obj)) {
            return DEFAULT_NODE_COLOR;
        }
        return obj;
    }

    private static &lt;E&gt; String processRefs(List&lt;E&gt; list, Function&lt;? super E, ? extends Integer&gt; mapper) {
        if (CollectionUtils.isEmpty(list)) {
            return "";
        }
        String tmp = Joiner.on(",").skipNulls().join(list.stream().map(mapper).collect(Collectors.toList()));
        if (1 == list.size()) {
            return tmp;
        }
        return String.format("\"%s\"", tmp);
    }
}
</pre> 
 <p>&nbsp;</p> 
 <div class="quote_title">
  输出结果 写道
 </div> 
 <div class="quote_div">
  ## Hello World
  <br># label: %step%
  <br># style: shape=%shape%;fillColor=%fill%;strokeColor=%stroke%;
  <br># namespace: csvimport-
  <br># connect: {"from":"refs", "to":"id", "invert":true, "style":"curved=0;endArrow=blockThin;endFill=1;"}
  <br># width: auto
  <br># height: auto
  <br># padding: 15
  <br># ignore: id,shape,fill,stroke,refs
  <br># nodespacing: 40
  <br># levelspacing: 100
  <br># edgespacing: 40
  <br># layout: auto
  <br>## CSV starts under this line
  <br>id,step,fill,stroke,shape,refs
  <br>1,"flowId:1,level:3",#f8cecc,#b85450,rectangle,
  <br>2,"flowId:2,level:3",#f8cecc,#b85450,rectangle,1
  <br>3,"flowId:3,level:3",#f8cecc,#b85450,rectangle,1
  <br>4,"flowId:4,level:2",#fff2cc,#d6b656,rectangle,"2,5"
  <br>5,"flowId:5,level:2",#d5e8d4,#82b366,rectangle,
  <br>6,"flowId:6,level:1",#dae8fc,#6c8ebf,rectangle,4
  <br>7,"flowId:7,level:1",#dae8fc,#6c8ebf,rectangle,"6,1"
 </div> 
 <p>&nbsp;</p> 
 <p>按照官网&nbsp;<a href="https://drawio-app.com/import-from-csv-to-drawio/">https://drawio-app.com/import-from-csv-to-drawio/</a>&nbsp;的描述，将上面输出的内容到&nbsp;<a href="https://www.draw.io/">https://www.draw.io/</a>&nbsp;里面，</p> 
 <p><span style="color: #444444; font-family: Lato; font-size: 16px;">Click on 菜单：</span><span style="font-weight: bold; color: #444444; font-family: Lato; font-size: 16px;"><tt style="background-color: #eeeeee;">Arrange &gt; Insert &gt; Advanced &gt; CSV</tt></span><span style="color: #444444; font-family: Lato; font-size: 16px;">.</span></p> 
 <p><span style="color: #444444; font-family: Lato; font-size: 16px;">进行操作即可。</span></p> 
 <p><span style="color: #444444; font-family: Lato; font-size: 16px;">如果觉得图形布局不够好看，可以操作菜单：</span><span style="background-color: #eeeeee; color: #444444; font-family: Lato; font-size: 16px; font-weight: bold;">Arrange &gt; Layout</span></p> 
</div>