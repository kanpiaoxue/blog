#Guava中Graph的操作说明（Guava 23）
###发表时间：2017-08-11
###分类：java,guava
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2389382" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2389382</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <h1 style="">来源：&nbsp;<a href="https://github.com/google/guava/wiki/GraphsExplained">https://github.com/google/guava/wiki/GraphsExplained</a> </h1> 
 <h1 style="">Graphs, Explained</h1> 
 <p style="">Guava's&nbsp;<code style="">common.graph</code>&nbsp;is a library for modeling&nbsp;<a style="background-color: transparent; color: #0366d6;" href="https://en.wikipedia.org/wiki/Graph_(discrete_mathematics)">graph</a>-structured data, that is, entities and the relationships between them. Examples include webpages and hyperlinks; scientists and the papers that they write; airports and the routes between them; and people and their family ties (family trees). Its purpose is to provide a common and extensible language for working with such data.</p> 
 <h2 style=""> <a id="user-content-definitions" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#definitions"></a>Definitions</h2> 
 <p style="">A graph consists of a set of&nbsp;<span style="font-weight: 600;">nodes</span>&nbsp;(also called vertices) and a set of&nbsp;<span style="font-weight: 600;">edges</span>&nbsp;(also called links, or arcs); each edge connects nodes to each other. The nodes incident to an edge are called its&nbsp;<span style="font-weight: 600;">endpoints</span>.</p> 
 <p style="">(While we introduce an interface called&nbsp;<code style="">Graph</code>&nbsp;below, we will use "graph" (lower case "g") as a general term referring to this type of data structure. When we want to refer to a specific type in this library, we capitalize it.)</p> 
 <p style="">An edge is&nbsp;<span style="font-weight: 600;">directed</span>&nbsp;if it has a defined start (its&nbsp;<span style="font-weight: 600;">source</span>) and end (its&nbsp;<span style="font-weight: 600;">target</span>, also called its destination). Otherwise, it is&nbsp;<span style="font-weight: 600;">undirected</span>. Directed edges are suitable for modeling asymmetric relations ("descended from", "links to", "authored by"), while undirected edges are suitable for modeling symmetric relations ("coauthored a paper with", "distance between", "sibling of").</p> 
 <p style="">A graph is directed if each of its edges are directed, and undirected if each of its edges are undirected. (<code style="">common.graph</code>&nbsp;does not support graphs that have both directed and undirected edges.)</p> 
 <p style="">Given this example:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre>graph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeU, nodeV, edgeUV);</pre> 
 </div> 
 <ul style=""> 
  <li style=""> <code style="">nodeU</code>&nbsp;and&nbsp;<code style="">nodeV</code>&nbsp;are mutually&nbsp;<span style="font-weight: 600;">adjacent</span> </li> 
  <li style="margin-top: 0.25em;"> <code style="">edgeUV</code>&nbsp;is&nbsp;<span style="font-weight: 600;">incident</span>&nbsp;to&nbsp;<code style="">nodeU</code>&nbsp;and to&nbsp;<code style="">nodeV</code>&nbsp;(and vice versa)</li> 
 </ul> 
 <p style="">If&nbsp;<code style="">graph</code>&nbsp;is directed, then:</p> 
 <ul style=""> 
  <li style=""> <code style="">nodeU</code>&nbsp;is a&nbsp;<span style="font-weight: 600;">predecessor</span>&nbsp;of&nbsp;<code style="">nodeV</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">nodeV</code>&nbsp;is a&nbsp;<span style="font-weight: 600;">successor</span>&nbsp;of&nbsp;<code style="">nodeU</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">edgeUV</code>&nbsp;is an&nbsp;<span style="font-weight: 600;">outgoing</span>&nbsp;edge (or out-edge) of&nbsp;<code style="">nodeU</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">edgeUV</code>&nbsp;is an&nbsp;<span style="font-weight: 600;">incoming</span>&nbsp;edge (or in-edge) of&nbsp;<code style="">nodeV</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">nodeU</code>&nbsp;is a&nbsp;<span style="font-weight: 600;">source</span>&nbsp;of&nbsp;<code style="">edgeUV</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">nodeV</code>&nbsp;is a&nbsp;<span style="font-weight: 600;">target</span>&nbsp;of&nbsp;<code style="">edgeUV</code> </li> 
 </ul> 
 <p style="">If&nbsp;<code style="">graph</code>&nbsp;is undirected, then:</p> 
 <ul style=""> 
  <li style=""> <code style="">nodeU</code>&nbsp;is a predecessor and a successor of&nbsp;<code style="">nodeV</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">nodeV</code>&nbsp;is a predecessor and a successor of&nbsp;<code style="">nodeU</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">edgeUV</code>&nbsp;is both an incoming and an outgoing edge of&nbsp;<code style="">nodeU</code> </li> 
  <li style="margin-top: 0.25em;"> <code style="">edgeUV</code>&nbsp;is both an incoming and an outgoing edge of&nbsp;<code style="">nodeV</code> </li> 
 </ul> 
 <p style="">All of these relationships are with respect to&nbsp;<code style="">graph</code>.</p> 
 <p style="">A&nbsp;<span style="font-weight: 600;">self-loop</span>&nbsp;is an edge that connects a node to itself; equivalently, it is an edge whose endpoints are the same node. If a self-loop is directed, it is both an outgoing and incoming edge of its incident node, and its incident node is both a source and a target of the self-loop edge.</p> 
 <p style="">Two edges are&nbsp;<span style="font-weight: 600;">parallel</span>&nbsp;if they connect the same nodes in the same order (if any), and&nbsp;<span style="font-weight: 600;">antiparallel</span>&nbsp;if they connect the same nodes in the opposite order. (Undirected edges cannot be antiparallel.)</p> 
 <p style="">Given this example:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre>directedGraph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeU, nodeV, edgeUV_a);
directedGraph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeU, nodeV, edgeUV_b);
directedGraph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeV, nodeU, edgeVU);

undirectedGraph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeU, nodeV, edgeUV_a);
undirectedGraph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeU, nodeV, edgeUV_b);
undirectedGraph<span class="pl-k" style="color: #d73a49;">.</span>addEdge(nodeV, nodeU, edgeVU);
</pre> 
 </div> 
 <p style="">In&nbsp;<code style="">directedGraph</code>,&nbsp;<code style="">edgeUV_a</code>&nbsp;and&nbsp;<code style="">edgeUV_b</code>&nbsp;are mutually parallel, and each is antiparallel with&nbsp;<code style="">edgeVU</code>.</p> 
 <p style="">In&nbsp;<code style="">undirectedGraph</code>, each of&nbsp;<code style="">edgeUV_a</code>,&nbsp;<code style="">edgeUV_b</code>, and&nbsp;<code style="">edgeVU</code>&nbsp;is mutually parallel with the other two.</p> 
 <h2 style=""> <a id="user-content-capabilities" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#capabilities"></a>Capabilities</h2> 
 <p style=""><code style="">common.graph</code>&nbsp;is focused on providing interfaces and classes to support working with graphs. It does not provide functionality such as I/O or visualization support, and it has a very limited selection of utilities. See the&nbsp;<a style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/wiki/GraphsExplained#faq">FAQ</a>&nbsp;for more on this topic.</p> 
 <p style="">As a whole,&nbsp;<code style="">common.graph</code>&nbsp;supports graphs of the following varieties:</p> 
 <ul style=""> 
  <li style="">directed graphs</li> 
  <li style="margin-top: 0.25em;">undirected graphs</li> 
  <li style="margin-top: 0.25em;">nodes and/or edges with associated values (weights, labels, etc.)</li> 
  <li style="margin-top: 0.25em;">graphs that do/don't allow self-loops</li> 
  <li style="margin-top: 0.25em;">graphs that do/don't allow parallel edges (graphs with parallel edges are sometimes called multigraphs)</li> 
  <li style="margin-top: 0.25em;">graphs whose nodes/edges are insertion-ordered, sorted, or unordered</li> 
 </ul> 
 <p style="">The kinds of graphs supported by a particular&nbsp;<code style="">common.graph</code>&nbsp;type are specified in its Javadoc. The kinds of graphs supported by the built-in implementations of each graph type are specified in the Javadoc for its associated&nbsp;<code style="">Builder</code>&nbsp;type. Specific&nbsp;<em style="">implementations</em>&nbsp;of the types in this library (especially third-party implementations) are not required to support all of these varieties, and may support others in addition.</p> 
 <p style="">The library is agnostic as to the choice of underlying data structures: relationships can be stored as matrices, adjacency lists, adjacency maps, etc. depending on what use cases the implementor wants to optimize for.</p> 
 <p style=""><code style="">common.graph</code>&nbsp;does not (at this time) include&nbsp;<em style="">explicit</em>&nbsp;support for the following graph variants, although they can be modeled using the existing types:</p> 
 <ul style=""> 
  <li style="">trees, forests</li> 
  <li style="margin-top: 0.25em;">graphs with elements of the same kind (nodes or edges) that have different types (for example: bipartite/k-partite graphs, multimodal graphs)</li> 
  <li style="margin-top: 0.25em;">hypergraphs</li> 
 </ul> 
 <p style=""><code style="">common.graph</code>&nbsp;does not allow graphs with both directed and undirected edges.</p> 
 <p style="">The&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Graphs.html"><code style="">Graphs</code></a>&nbsp;class provides some basic utilities (for example, copying and comparing graphs).</p> 
 <h2 style=""> <a id="user-content-graph-types" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#graph-types"></a>Graph Types</h2> 
 <p style="">There are three top-level graph interfaces, that are distinguished by their representation of edges:&nbsp;<code style="">Graph</code>,&nbsp;<code style="">ValueGraph</code>, and&nbsp;<code style="">Network</code>. These are sibling types, i.e., none is a subtype of any of the others.</p> 
 <p style="">Each of these "top-level" interfaces extends&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/SuccessorsFunction.html"><code style="">SuccessorsFunction</code></a>&nbsp;and&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/PredecessorsFunction.html"><code style="">PredecessorsFunction</code></a>. These interfaces are meant to be used as the type of a parameter to graph algorithms (such as breadth first traversal) that only need a way of accessing the successors/predecessors of a node in a graph. This is especially useful in cases where the owner of a graph already has a representation that works for them and doesn't particularly want to serialize their representation into a&nbsp;<code style="">common.graph</code>&nbsp;type just to run one graph algorithm.</p> 
 <h3 style=""> <a id="user-content-graph" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#graph"></a>Graph</h3> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Graph.html"><code style="">Graph</code></a>&nbsp;is the simplest and most fundamental graph type. It defines the low-level operators for dealing with node-to-node relationships, such as&nbsp;<code style="">successors(node)</code>,&nbsp;<code style="">adjacentNodes(node)</code>, and&nbsp;<code style="">inDegree(node)</code>. Its nodes are first-class unique objects; you can think of them as analogous to&nbsp;<code style="">Map</code>&nbsp;keys into the&nbsp;<code style="">Graph</code>&nbsp;internal data structures.</p> 
 <p style="">The edges of a&nbsp;<code style="">Graph</code>&nbsp;are completely anonymous; they are defined only in terms of their endpoints.</p> 
 <p style="">Example use case:&nbsp;<code style="">Graph&lt;Airport&gt;</code>, whose edges connect the airports between which one can take a direct flight.</p> 
 <h3 style=""> <a id="user-content-valuegraph" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#valuegraph"></a>ValueGraph</h3> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/ValueGraph.html"><code style="">ValueGraph</code></a>&nbsp;has all the node-related methods that&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Graph.html"><code style="">Graph</code></a>&nbsp;does, but adds a couple of methods that retrieve a value for a specified edge.</p> 
 <p style="">The edges of a&nbsp;<code style="">ValueGraph</code>&nbsp;each have an associated user-specified value. These values need not be unique (as nodes are); the relationship between a&nbsp;<code style="">ValueGraph</code>&nbsp;and a&nbsp;<code style="">Graph</code>&nbsp;is analogous to that between a&nbsp;<code style="">Map</code>&nbsp;and a&nbsp;<code style="">Set</code>; a&nbsp;<code style="">Graph</code>'s edges are a set of pairs of endpoints, and a&nbsp;<code style="">ValueGraph</code>'s edges are a map from pairs of endpoints to values.)</p> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/ValueGraph.html"><code style="">ValueGraph</code></a>&nbsp;provides an&nbsp;<code style="">asGraph()</code>&nbsp;method which returns a&nbsp;<code style="">Graph</code>&nbsp;view of the&nbsp;<code style="">ValueGraph</code>. This allows methods which operate on&nbsp;<code style="">Graph</code>&nbsp;instances to function for&nbsp;<code style="">ValueGraph</code>&nbsp;instances as well.</p> 
 <p style="">Example use case:&nbsp;<code style="">ValueGraph&lt;Airport, Integer&gt;</code>, whose edges values represent the time required to travel between the two&nbsp;<code style="">Airport</code>s that the edge connects.</p> 
 <h3 style=""> <a id="user-content-network" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#network"></a>Network</h3> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Network.html"><code style="">Network</code></a>&nbsp;has all the node-related methods that&nbsp;<code style="">Graph</code>&nbsp;does, but adds methods that work with edges and node-to-edge relationships, such as&nbsp;<code style="">outEdges(node)</code>,&nbsp;<code style="">incidentNodes(edge)</code>, and&nbsp;<code style="">edgesConnecting(nodeU, nodeV)</code>.</p> 
 <p style="">The edges of a&nbsp;<code style="">Network</code>&nbsp;are first-class (unique) objects, just as nodes are in all graph types. The uniqueness constraint for edges allows&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Network.html"><code style="">Network</code></a>&nbsp;to natively support parallel edges, as well as the methods relating to edges and node-to-edge relationships.</p> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Network.html"><code style="">Network</code></a>&nbsp;provides an&nbsp;<code style="">asGraph()</code>&nbsp;method which returns a&nbsp;<code style="">Graph</code>&nbsp;view of the&nbsp;<code style="">Network</code>. This allows methods which operate on&nbsp;<code style="">Graph</code>&nbsp;instances to function for&nbsp;<code style="">Network</code>&nbsp;instances as well.</p> 
 <p style="">Example use case:&nbsp;<code style="">Network&lt;Airport, Flight&gt;</code>, in which the edges represent the specific flights that one can take to get from one airport to another.</p> 
 <h3 style=""> <a id="user-content-choosing-the-right-graph-type" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#choosing-the-right-graph-type"></a>Choosing the right graph type</h3> 
 <p style="">The essential distinction between the three graph types is in their representation of edges.</p> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Graph.html"><code style="">Graph</code></a>&nbsp;has edges which are anonymous connections between nodes, with no identity or properties of their own. You should use&nbsp;<code style="">Graph</code>&nbsp;if each pair of nodes is connected by at most one edge, and you don't need to associate any information with edges.</p> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/ValueGraph.html"><code style="">ValueGraph</code></a>&nbsp;has edges which have values (e.g., edge weights or labels) that may or may not be unique. You should use&nbsp;<code style="">ValueGraph</code>&nbsp;if each pair of nodes is connected by at most one edge, and you need to associate information with edges that may be the same for different edges (for example, edge weights).</p> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Network.html"><code style="">Network</code></a>&nbsp;has edges which are first-class unique objects, just as nodes are. You should use&nbsp;<code style="">Network</code>&nbsp;if your edge objects are unique, and you want to be able to issue queries that reference them. (Note that this uniqueness allows&nbsp;<code style="">Network</code>&nbsp;to support parallel edges.)</p> 
 <h2 style=""> <a id="user-content-building-graph-instances" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#building-graph-instances"></a>Building graph instances</h2> 
 <p style="">The implementation classes that&nbsp;<code style="">common.graph</code>&nbsp;provides are not public, by design. This reduces the number of public types that users need to know about, and makes it easier to navigate the various capabilities that the built-implementations provide, without overwhelming users that just want to create a graph.</p> 
 <p style="">To create an instance of one of the built-in implementations of a graph type, use the corresponding&nbsp;<code style="">Builder</code>&nbsp;class:&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/GraphBuilder.html"><code style="">GraphBuilder</code></a>,&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/ValueGraphBuilder.html"><code style="">ValueGraphBuilder</code></a>, or&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/NetworkBuilder.html"><code style="">NetworkBuilder</code></a>. Examples:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">MutableGraph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> graph <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">GraphBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>undirected()<span class="pl-k" style="color: #d73a49;">.</span>build();

<span class="pl-k" style="color: #d73a49;">MutableValueGraph&lt;<span class="pl-smi" style="color: #24292e;">City</span>, <span class="pl-smi" style="color: #24292e;">Distance</span>&gt;</span> roads <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">ValueGraphBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>directed()<span class="pl-k" style="color: #d73a49;">.</span>build();

<span class="pl-k" style="color: #d73a49;">MutableNetwork&lt;<span class="pl-smi" style="color: #24292e;">Webpage</span>, <span class="pl-smi" style="color: #24292e;">Link</span>&gt;</span> webSnapshot <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">NetworkBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>directed()
    .allowsParallelEdges(<span class="pl-c1" style="color: #005cc5;">true</span>)
    .nodeOrder(<span class="pl-smi" style="color: #24292e;">ElementOrder</span><span class="pl-k" style="color: #d73a49;">.</span>natural())
    .expectedNodeCount(<span class="pl-c1" style="color: #005cc5;">100000</span>)
    .expectedEdgeCount(<span class="pl-c1" style="color: #005cc5;">1000000</span>)
    .build();
</pre> 
 </div> 
 <ul style=""> 
  <li style="">You can get an instance of a graph&nbsp;<code style="">Builder</code>&nbsp;in one of two ways: 
   <ul style="padding-left: 2em; margin-bottom: 0px;"> 
    <li style="">calling the static methods&nbsp;<code style="">directed()</code>&nbsp;or&nbsp;<code style="">undirected()</code>. Each Graph instance that the&nbsp;<code style="">Builder</code>&nbsp;provides will be directed or undirected.</li> 
    <li style="margin-top: 0.25em;">calling the static method&nbsp;<code style="">from()</code>, which gives you a&nbsp;<code style="">Builder</code>&nbsp;based on an existing graph instance.</li> 
   </ul> </li> 
  <li style="margin-top: 0.25em;">After you've created your&nbsp;<code style="">Builder</code>&nbsp;instance, you can optionally specify other characteristics and capabilities.</li> 
  <li style="margin-top: 0.25em;">You can call&nbsp;<code style="">build()</code>&nbsp;on the same&nbsp;<code style="">Builder</code>&nbsp;instance multiple times to build multiple graph instances.</li> 
  <li style="margin-top: 0.25em;">You don't need to specify the node and edge types on the&nbsp;<code style="">Builder</code>; specifying them on the graph type itself is sufficient.</li> 
  <li style="margin-top: 0.25em;">The&nbsp;<code style="">build()</code>&nbsp;method returns a&nbsp;<code style="">Mutable</code>&nbsp;subtype of the associated graph type, which provides mutation methods; more on this in&nbsp;<a style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/wiki/GraphsExplained#mutable-and-immutable-graphs">"<code style="">Mutable</code>&nbsp;and&nbsp;<code style="">Immutable</code>&nbsp;graphs"</a>, below.</li> 
 </ul> 
 <h3 style=""> <a id="user-content-builder-constraints-vs-optimization-hints" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#builder-constraints-vs-optimization-hints"></a>Builder constraints vs. optimization hints</h3> 
 <p style="">The&nbsp;<code style="">Builder</code>&nbsp;types generally provide two types of options: constraints and optimization hints.</p> 
 <p style="">Constraints specify behaviors and properties that graphs created by a given&nbsp;<code style="">Builder</code>instance must satisfy, such as:</p> 
 <ul style=""> 
  <li style="">whether the graph is directed</li> 
  <li style="margin-top: 0.25em;">whether this graph allows self-loops</li> 
  <li style="margin-top: 0.25em;">whether this graph's edges are sorted</li> 
 </ul> 
 <p style="">and so forth.</p> 
 <p style="">Optimization hints may optionally be used by the implementation class to increase efficiency, for example, to determine the type or initial size of internal data structures. They are not guaranteed to have any effect.</p> 
 <p style="">Each graph type provides accessors corresponding to its&nbsp;<code style="">Builder</code>-specified constraints, but does not provide accessors for optimization hints.</p> 
 <h2 style=""> <a id="user-content-mutable-and-immutable-graphs" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#mutable-and-immutable-graphs"></a><code style="">Mutable</code>&nbsp;and&nbsp;<code style="">Immutable</code>&nbsp;graphs</h2> 
 <h3 style=""> <a id="user-content-mutable-types" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#mutable-types"></a><code style="">Mutable*</code>&nbsp;types</h3> 
 <p style="">Each graph type has a corresponding&nbsp;<code style="">Mutable*</code>&nbsp;subtype:&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/MutableGraph.html"><code style="">MutableGraph</code></a>,&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/MutableValueGraph.html"><code style="">MutableValueGraph</code></a>, and&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/MutableNetwork.html"><code style="">MutableNetwork</code></a>. These subtypes define the mutation methods:</p> 
 <ul style=""> 
  <li style="">methods for adding and removing nodes: 
   <ul style="padding-left: 2em; margin-bottom: 0px;"> 
    <li style=""> <code style="">addNode(node)</code>&nbsp;and&nbsp;<code style="">removeNode(node)</code> </li> 
   </ul> </li> 
  <li style="margin-top: 0.25em;">methods for adding and removing edges: 
   <ul style="padding-left: 2em; margin-bottom: 0px;"> 
    <li style=""> <a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/MutableGraph.html"><code style="">MutableGraph</code></a> 
     <ul style="padding-left: 2em; margin-bottom: 0px;"> 
      <li style=""><code style="">putEdge(nodeU, nodeV)</code></li> 
      <li style="margin-top: 0.25em;"><code style="">removeEdge(nodeU, nodeV)</code></li> 
     </ul> </li> 
    <li style="margin-top: 0.25em;"> <a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/MutableValueGraph.html"><code style="">MutableValueGraph</code></a> 
     <ul style="padding-left: 2em; margin-bottom: 0px;"> 
      <li style=""><code style="">putEdgeValue(nodeU, nodeV, value)</code></li> 
      <li style="margin-top: 0.25em;"><code style="">removeEdge(nodeU, nodeV)</code></li> 
     </ul> </li> 
    <li style="margin-top: 0.25em;"> <a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/MutableNetwork.html"><code style="">MutableNetwork</code></a> 
     <ul style="padding-left: 2em; margin-bottom: 0px;"> 
      <li style=""><code style="">addEdge(nodeU, nodeV, edge)</code></li> 
      <li style="margin-top: 0.25em;"><code style="">removeEdge(edge)</code></li> 
     </ul> </li> 
   </ul> </li> 
 </ul> 
 <p style="">This is a departure from the way that the Java Collections Framework--and Guava's new collection types--have historically worked; each of those types includes signatures for (optional) mutation methods. We chose to break out the mutable methods into subtypes in part to encourage defensive programming: generally speaking, if your code only examines or traverses a graph and does not mutate it, its input should be specified as on&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Graph.html"><code style="">Graph</code></a>,&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/ValueGraph.html"><code style="">ValueGraph</code></a>, or&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Network.html"><code style="">Network</code></a>&nbsp;rather than their mutable subtypes. On the other hand, if your code does need to mutate an object, it's helpful for your code to have to call attention to that fact by working with a type that labels itself "Mutable".</p> 
 <p style="">Since&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Graph.html"><code style="">Graph</code></a>, etc. are interfaces, even though they don't include mutation methods, providing an instance of this interface to a caller&nbsp;<em style="">does not guarantee</em>&nbsp;that it will not be mutated by the caller, as (if it is in fact a&nbsp;<code style="">Mutable*</code>&nbsp;subtype) the caller could cast it to that subtype. If you want to provide a contractual guarantee that a graph which is a method parameter or return value cannot be modified, you should use the&nbsp;<code style="">Immutable</code>implementations; more on this below.</p> 
 <h3 style=""> <a id="user-content-immutable-implementations" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#immutable-implementations"></a><code style="">Immutable*</code>&nbsp;implementations</h3> 
 <p style="">Each graph type also has a corresponding&nbsp;<code style="">Immutable</code>&nbsp;implementation. These classes are analogous to Guava's&nbsp;<code style="">ImmutableSet</code>,&nbsp;<code style="">ImmutableList</code>,&nbsp;<code style="">ImmutableMap</code>, etc.: once constructed, they cannot be modified, and they use efficient immutable data structures internally.</p> 
 <p style="">Unlike the other Guava&nbsp;<code style="">Immutable</code>&nbsp;types, however, these implementations do not have any method signatures for mutation methods, so they don't need to throw<code style="">UnsupportedOperationException</code>&nbsp;for attempted mutates.</p> 
 <p style="">You create an instance of an&nbsp;<code style="">ImmutableGraph</code>, etc. by calling its static&nbsp;<code style="">copyOf()</code>&nbsp;method:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">ImmutableGraph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> immutableGraph <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">ImmutableGraph</span><span class="pl-k" style="color: #d73a49;">.</span>copyOf(graph);</pre> 
 </div> 
 <h4 style=""> <a id="user-content-guarantees" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#guarantees"></a>Guarantees</h4> 
 <p style="">Each&nbsp;<code style="">Immutable*</code>&nbsp;type makes the following guarantees:</p> 
 <ul style=""> 
  <li style=""> <span style="font-weight: 600;">shallow immutability</span>: elements can never be added, removed or replaced (these classes do not implement the&nbsp;<code style="">Mutable*</code>&nbsp;interfaces)</li> 
  <li style="margin-top: 0.25em;"> <span style="font-weight: 600;">deterministic iteration</span>: the iteration orders are always the same as those of the input graph</li> 
  <li style="margin-top: 0.25em;"> <a style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/wiki/GraphsExplained#synchronization"><span style="font-weight: 600;">thread safety</span></a>: it is safe to access this graph concurrently from multiple threads</li> 
  <li style="margin-top: 0.25em;"> <span style="font-weight: 600;">integrity</span>: this type cannot be subclassed outside this package (which would allow these guarantees to be violated)</li> 
 </ul> 
 <h4 style=""> <a id="user-content-treat-these-classes-as-interfaces-not-implementations" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#treat-these-classes-as-interfaces-not-implementations"></a>Treat these classes as "interfaces", not implementations</h4> 
 <p style="">Each of the&nbsp;<code style="">Immutable*</code>&nbsp;classes is a type offering meaningful behavioral guarantees -- not merely a specific implementation. You should treat them as interfaces in every important sense of the word.</p> 
 <p style="">Fields and method return values that store an&nbsp;<code style="">Immutable*</code>&nbsp;instance (such as&nbsp;<code style="">ImmutableGraph</code>) should be declared to be of the&nbsp;<code style="">Immutable*</code>&nbsp;type rather than the corresponding interface type (such as&nbsp;<code style="">Graph</code>). This communicates to callers all of the semantic guarantees listed above, which is almost always very useful information.</p> 
 <p style="">On the other hand, a parameter type of&nbsp;<code style="">ImmutableGraph</code>&nbsp;is generally a nuisance to callers. Instead, accept&nbsp;<code style="">Graph</code>.</p> 
 <p style=""><span style="font-weight: 600;">Warning</span>: as noted&nbsp;<a style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/wiki/GraphsExplained#graph-elements-nodes-and-edges">elsewhere</a>, it is almost always a bad idea to modify an element (in a way that affects its&nbsp;<code style="">equals()</code>&nbsp;behavior) while it is contained in a collection. Undefined behavior and bugs will result. It's generally best to avoid using mutable objects as elements of an&nbsp;<code style="">Immutable*</code>&nbsp;instance at all, as many users may expect your "immutable" object to be deeply immutable.</p> 
 <h2 style=""> <a id="user-content-graph-elements-nodes-and-edges" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#graph-elements-nodes-and-edges"></a>Graph elements (nodes and edges)</h2> 
 <p style=""><span style="font-weight: 600;">Nodes (and, in&nbsp;<code style="">Network</code>, edges) must be useable as&nbsp;<code style="">Map</code>&nbsp;keys</span>. That is:</p> 
 <ul style=""> 
  <li style="">they must be unique in a graph: nodes&nbsp;<code style="">nodeA</code>&nbsp;and&nbsp;<code style="">nodeB</code>&nbsp;are considered different if and only if&nbsp;<code style="">nodeA.equals(nodeB) == false</code>.</li> 
  <li style="margin-top: 0.25em;">they must have appropriate (and consistent) implementations of&nbsp;<code style="">equals()</code>&nbsp;and&nbsp;<code style="">hashCode()</code>.</li> 
  <li style="margin-top: 0.25em;">If elements are sorted (for example, via&nbsp;<code style="">GraphBuilder.orderNodes()</code>), the ordering must be consistent with equals (as defined by the&nbsp;<code style="">Comparator</code>&nbsp;and&nbsp;<code style="">Comparable</code>&nbsp;interfaces).</li> 
 </ul> 
 <p style="">If graph elements have mutable state:</p> 
 <ul style=""> 
  <li style="">the mutable state must not be reflected in the&nbsp;<code style="">equals()/hashCode()</code>&nbsp;methods (this is discussed in the&nbsp;<code style="">Map</code>&nbsp;documentation in detail)</li> 
  <li style="margin-top: 0.25em;">don't construct multiple elements that are equal to each other and expect them to be interchangeable. In particular, when adding such elements to a graph, you should create them once and store the reference if you will need to refer to those elements more than once during creation (rather than passing&nbsp;<code style="">new MyMutableNode(id)</code>&nbsp;to each&nbsp;<code style="">add*()</code>&nbsp;call).</li> 
 </ul> 
 <p style="">If you need to store mutable per-element state, one option is to use immutable elements and store the mutable state in a separate data structure (e.g. an element-to-state map).</p> 
 <p style="">Graph elements must be non-null.</p> 
 <h2 style=""> <a id="user-content-library-contracts-and-behaviors" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#library-contracts-and-behaviors"></a>Library contracts and behaviors</h2> 
 <p style="">This section discusses behaviors of the built-in implementations of the&nbsp;<code style="">common.graph</code>&nbsp;types.</p> 
 <h3 style=""> <a id="user-content-mutation" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#mutation"></a>Mutation</h3> 
 <p style="">You can add an edge whose incident nodes have not previously been added to the graph. If they're not already present, they're silently added to the graph:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">Graph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> graph <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">GraphBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>directed()<span class="pl-k" style="color: #d73a49;">.</span>build();  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> graph is empty</span>
graph<span class="pl-k" style="color: #d73a49;">.</span>putEdge(<span class="pl-c1" style="color: #005cc5;">1</span>, <span class="pl-c1" style="color: #005cc5;">2</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> this adds 1 and 2 as nodes of this graph, and puts</span>
                      <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> an edge between them</span>
<span class="pl-k" style="color: #d73a49;">if</span> (graph<span class="pl-k" style="color: #d73a49;">.</span>nodes()<span class="pl-k" style="color: #d73a49;">.</span>contains(<span class="pl-c1" style="color: #005cc5;">1</span>)) {  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> evaluates to "true"</span>
  <span class="pl-c1" style="color: #005cc5;">...</span>
}</pre> 
 </div> 
 <h3 style=""> <a id="user-content-graph-equals-and-graph-equivalence" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#graph-equals-and-graph-equivalence"></a>Graph&nbsp;<code style="">equals()</code>&nbsp;and graph equivalence</h3> 
 <p style="">As of Guava 22,&nbsp;<code style="">common.graph</code>'s graph types each define&nbsp;<code style="">equals()</code>&nbsp;in a way that makes sense for the particular type:</p> 
 <ul style=""> 
  <li style=""> <code style="">Graph.equals()</code>&nbsp;defines two&nbsp;<code style="">Graph</code>s to be equal if they have the same node and edge sets (that is, each edge has the same endpoints and same direction in both graphs).</li> 
  <li style="margin-top: 0.25em;"> <code style="">ValueGraph.equals()</code>&nbsp;defines two&nbsp;<code style="">ValueGraph</code>s to be equal if they have the same node and edge sets, and equal edges have equal values.</li> 
  <li style="margin-top: 0.25em;"> <code style="">Network.equals()</code>&nbsp;defines two&nbsp;<code style="">Network</code>s to be equal if they have the same node and edge sets, and each edge object has connects the same nodes in the same direction (if any).</li> 
 </ul> 
 <p style="">In addition, for each graph type, two graphs can be equal only if their edges have the same directedness (both graphs are directed or both are undirected).</p> 
 <p style="">Of course,&nbsp;<code style="">hashCode()</code>&nbsp;is defined consistently with&nbsp;<code style="">equals()</code>&nbsp;for each graph type.</p> 
 <p style="">If you want to compare two&nbsp;<code style="">Network</code>s or two&nbsp;<code style="">ValueGraph</code>s based only on connectivity, or to compare a&nbsp;<code style="">Network</code>&nbsp;or a&nbsp;<code style="">ValueGraph</code>&nbsp;to a&nbsp;<code style="">Graph</code>, you can use the&nbsp;<code style="">Graph</code>&nbsp;view that&nbsp;<code style="">Network</code>and&nbsp;<code style="">ValueGraph</code>&nbsp;provide:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">Graph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> graph1, graph2;
<span class="pl-k" style="color: #d73a49;">ValueGraph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>, <span class="pl-smi" style="color: #24292e;">Double</span>&gt;</span> valueGraph1, valueGraph2;
<span class="pl-k" style="color: #d73a49;">Network&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>, <span class="pl-smi" style="color: #24292e;">MyEdge</span>&gt;</span> network1, network2;

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> compare based on nodes and node relationships only</span>
<span class="pl-k" style="color: #d73a49;">if</span> (graph1<span class="pl-k" style="color: #d73a49;">.</span>equals(graph2)) { <span class="pl-c1" style="color: #005cc5;">...</span> }
<span class="pl-k" style="color: #d73a49;">if</span> (valueGraph1<span class="pl-k" style="color: #d73a49;">.</span>asGraph()<span class="pl-k" style="color: #d73a49;">.</span>equals(valueGraph2<span class="pl-k" style="color: #d73a49;">.</span>asGraph())) { <span class="pl-c1" style="color: #005cc5;">...</span> }
<span class="pl-k" style="color: #d73a49;">if</span> (network1<span class="pl-k" style="color: #d73a49;">.</span>asGraph()<span class="pl-k" style="color: #d73a49;">.</span>equals(graph1<span class="pl-k" style="color: #d73a49;">.</span>asGraph())) { <span class="pl-c1" style="color: #005cc5;">...</span> }

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> compare based on nodes, node relationships, and edge values</span>
<span class="pl-k" style="color: #d73a49;">if</span> (valueGraph1<span class="pl-k" style="color: #d73a49;">.</span>equals(valueGraph2)) { <span class="pl-c1" style="color: #005cc5;">...</span> }

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> compare based on nodes, node relationships, and edge identities</span>
<span class="pl-k" style="color: #d73a49;">if</span> (network1<span class="pl-k" style="color: #d73a49;">.</span>equals(network2)) { <span class="pl-c1" style="color: #005cc5;">...</span> }</pre> 
 </div> 
 <h3 style=""> <a id="user-content-accessor-methods" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#accessor-methods"></a>Accessor methods</h3> 
 <p style="">Accessors which return collections:</p> 
 <ul style=""> 
  <li style="">may return views of the graph; modifications to the graph which affect a view (for example, calling&nbsp;<code style="">addNode(n)</code>&nbsp;or&nbsp;<code style="">removeNode(n)</code>&nbsp;while iterating through&nbsp;<code style="">nodes()</code>) are not supported and may result in throwing&nbsp;<code style="">ConcurrentModificationException</code>.</li> 
  <li style="margin-top: 0.25em;">will return empty collections if their inputs are valid but no elements satisfy the request (for example:&nbsp;<code style="">adjacentNodes(node)</code>&nbsp;will return an empty collection if&nbsp;<code style="">node</code>&nbsp;has no adjacent nodes).</li> 
 </ul> 
 <p style="">Accessors will throw&nbsp;<code style="">IllegalArgumentException</code>&nbsp;if passed an element that is not in the graph.</p> 
 <p style="">While some Java Collection Framework methods such as&nbsp;<code style="">contains()</code>&nbsp;take&nbsp;<code style="">Object</code>parameters rather than the appropriate generic type specifier, as of Guava 22, the&nbsp;<code style="">common.graph</code>&nbsp;methods take the generic type specifiers to improve type safety.</p> 
 <h3 style=""> <a id="user-content-synchronization" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#synchronization"></a>Synchronization</h3> 
 <p style="">It is up to each graph implementation to determine its own synchronization policy. By default, undefined behavior may result from the invocation of any method on a graph that is being mutated by another thread.</p> 
 <p style="">Generally speaking, the built-in mutable implementations provide no synchronization guarantees, but the&nbsp;<code style="">Immutable*</code>&nbsp;classes (by virtue of being immutable) are thread-safe.</p> 
 <h3 style=""> <a id="user-content-element-objects" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#element-objects"></a>Element objects</h3> 
 <p style="">The node, edge, and value objects that you add to your graphs are irrelevant to the built-in implementations; they're just used as keys to internal data structures. This means that nodes/edges may be shared among graph instances.</p> 
 <p style="">By default, node and edge objects are insertion-ordered (that is, are visited by the&nbsp;<code style="">Iterator</code>s for&nbsp;<code style="">nodes()</code>&nbsp;and&nbsp;<code style="">edges()</code>&nbsp;in the order in which they were added to the graph, as with&nbsp;<code style="">LinkedHashSet</code>).</p> 
 <h2 style=""> <a id="user-content-notes-for-implementors" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#notes-for-implementors"></a>Notes for implementors</h2> 
 <h3 style=""> <a id="user-content-storage-models" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#storage-models"></a>Storage models</h3> 
 <p style=""><code style="">common.graph</code>&nbsp;supports multiple mechanisms for storing the topology of a graph, including:</p> 
 <ul style=""> 
  <li style="">the graph implementation stores the topology (for example, by storing a&nbsp;<code style="">Map&lt;N, Set&lt;N&gt;&gt;</code>that maps nodes onto their adjacent nodes); this implies that the nodes are just keys, and can be shared among graphs</li> 
  <li style="margin-top: 0.25em;">the nodes store the topology (for example, by storing a&nbsp;<code style="">List&lt;E&gt;</code>&nbsp;of adjacent nodes); this (usually) implies that nodes are graph-specific</li> 
  <li style="margin-top: 0.25em;">a separate data repository (for example, a database) stores the topology</li> 
 </ul> 
 <p style="">Note:&nbsp;<code style="">Multimap</code>s are not sufficient internal data structures for Graph implementations that support isolated nodes (nodes that have no incident edges), due to their restriction that a key either maps to at least one value, or is not present in the&nbsp;<code style="">Multimap</code>.</p> 
 <h3 style=""> <a id="user-content-accessor-behavior" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#accessor-behavior"></a>Accessor behavior</h3> 
 <p style="">For accessors that return a collection, there are several options for the semantics, including:</p> 
 <ol style=""> 
  <li style="">Collection is an immutable copy (e.g.&nbsp;<code style="">ImmutableSet</code>): attempts to modify the collection in any way will throw an exception, and modifications to the graph will&nbsp;<span style="font-weight: 600;">not</span>&nbsp;be reflected in the collection.</li> 
  <li style="margin-top: 0.25em;">Collection is an unmodifiable view (e.g.&nbsp;<code style="">Collections.unmodifiableSet()</code>): attempts to modify the collection in any way will throw an exception, and modifications to the graph will be reflected in the collection.</li> 
  <li style="margin-top: 0.25em;">Collection is a mutable copy: it may be modified, but modifications to the collection will&nbsp;<span style="font-weight: 600;">not</span>&nbsp;be reflected in the graph, and vice versa.</li> 
  <li style="margin-top: 0.25em;">Collection is a modifiable view: it may be modified, and modifications to the collection will be reflected in the graph, and vice versa.</li> 
 </ol> 
 <p style="">(In theory one could return a collection which passes through writes in one direction but not the other (collection-to-graph or vice-versa), but this is basically never going to be useful or clear, so please don't. :) )</p> 
 <p style="">(1) and (2) are generally preferred; as of this writing, the built-in implementations generally use (2).</p> 
 <p style="">(3) is a workable option, but may be confusing to users if they expect that modifications will affect the graph, or that modifications to the graph would be reflected in the set.</p> 
 <p style="">(4) is a hazardous design choice and should be used only with extreme caution, because keeping the internal data structures consistent can be tricky.</p> 
 <h3 style=""> <a id="user-content-abstract-classes" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#abstract-classes"></a><code style="">Abstract*</code>&nbsp;classes</h3> 
 <p style="">Each graph type has a corresponding&nbsp;<code style="">Abstract</code>&nbsp;class:&nbsp;<code style="">AbstractGraph</code>, etc.</p> 
 <p style="">Implementors of the graph interfaces should, if possible, extend the appropriate abstract class rather than implementing the interface directly. The abstract classes provide implementations of several key methods that can be tricky to do correctly, or for which it's helpful to have consistent implementations, such as:</p> 
 <ul style=""> 
  <li style=""><code style="">*degree()</code></li> 
  <li style="margin-top: 0.25em;"><code style="">toString()</code></li> 
  <li style="margin-top: 0.25em;"><code style="">Graph.edges()</code></li> 
  <li style="margin-top: 0.25em;"><code style="">Network.asGraph()</code></li> 
 </ul> 
 <h2 style=""> <a id="user-content-code-examples" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#code-examples"></a>Code examples</h2> 
 <h3 style=""> <a id="user-content-is-node-in-the-graph" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#is-node-in-the-graph"></a>Is&nbsp;<code style="">node</code>&nbsp;in the graph?</h3> 
 <div class="highlight highlight-source-java" style=""> 
  <pre>graph<span class="pl-k" style="color: #d73a49;">.</span>nodes()<span class="pl-k" style="color: #d73a49;">.</span>contains(node);</pre> 
 </div> 
 <h3 style=""> <a id="user-content-is-there-an-edge-between-nodes-u-and-v-that-are-known-to-be-in-the-graph" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#is-there-an-edge-between-nodes-u-and-v-that-are-known-to-be-in-the-graph"></a>Is there an edge between nodes&nbsp;<code style="">u</code>&nbsp;and&nbsp;<code style="">v</code>&nbsp;(that are known to be in the graph)?</h3> 
 <p style="">In the case where the graph is undirected, the ordering of the arguments&nbsp;<code style="">u</code>&nbsp;and&nbsp;<code style="">v</code>&nbsp;in the examples below is irrelevant.</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> This is the preferred syntax since 23.0 for all graph types.</span>
graphs<span class="pl-k" style="color: #d73a49;">.</span>hasEdgeConnecting(u, v);

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> These are equivalent (to each other and to the above expression).</span>
graph<span class="pl-k" style="color: #d73a49;">.</span>successors(u)<span class="pl-k" style="color: #d73a49;">.</span>contains(v);
graph<span class="pl-k" style="color: #d73a49;">.</span>predecessors(v)<span class="pl-k" style="color: #d73a49;">.</span>contains(u);

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> This is equivalent to the expressions above if the graph is undirected.</span>
graph<span class="pl-k" style="color: #d73a49;">.</span>adjacentNodes(u)<span class="pl-k" style="color: #d73a49;">.</span>contains(v);

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> This works only for Networks.</span>
<span class="pl-k" style="color: #d73a49;">!</span>network<span class="pl-k" style="color: #d73a49;">.</span>edgesConnecting(u, v)<span class="pl-k" style="color: #d73a49;">.</span>isEmpty();

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> This works only if "network" has at most a single edge connecting u to v.</span>
network<span class="pl-k" style="color: #d73a49;">.</span>edgeConnecting(u, v)<span class="pl-k" style="color: #d73a49;">.</span>isPresent();  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> Java 8 only</span>
network<span class="pl-k" style="color: #d73a49;">.</span>edgeConnectingOrNull(u, v) <span class="pl-k" style="color: #d73a49;">!=</span> <span class="pl-c1" style="color: #005cc5;">null</span>;

<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> These work only for ValueGraphs.</span>
valueGraph<span class="pl-k" style="color: #d73a49;">.</span>edgeValue(u, v)<span class="pl-k" style="color: #d73a49;">.</span>isPresent();  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> Java 8 only</span>
valueGraph<span class="pl-k" style="color: #d73a49;">.</span>edgeValueOrDefault(u, v, <span class="pl-c1" style="color: #005cc5;">null</span>) <span class="pl-k" style="color: #d73a49;">!=</span> <span class="pl-c1" style="color: #005cc5;">null</span>;</pre> 
 </div> 
 <h3 style=""> <a id="user-content-basic-graph-example" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#basic-graph-example"></a>Basic&nbsp;<code style="">Graph</code>&nbsp;example</h3> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">MutableGraph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> graph <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">GraphBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>directed()<span class="pl-k" style="color: #d73a49;">.</span>build();
graph<span class="pl-k" style="color: #d73a49;">.</span>addNode(<span class="pl-c1" style="color: #005cc5;">1</span>);
graph<span class="pl-k" style="color: #d73a49;">.</span>putEdge(<span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> also adds nodes 2 and 3 if not already present</span>

<span class="pl-k" style="color: #d73a49;">Set&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> successorsOfTwo <span class="pl-k" style="color: #d73a49;">=</span> graph<span class="pl-k" style="color: #d73a49;">.</span>successors(<span class="pl-c1" style="color: #005cc5;">2</span>); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> returns {3}</span>

graph<span class="pl-k" style="color: #d73a49;">.</span>putEdge(<span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> no effect; Graph does not support parallel edges</span></pre> 
 </div> 
 <h3 style=""> <a id="user-content-basic-valuegraph-example" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#basic-valuegraph-example"></a>Basic&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/ValueGraph.html"><code style="">ValueGraph</code></a>&nbsp;example</h3> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">MutableValueGraph&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>, <span class="pl-smi" style="color: #24292e;">Double</span>&gt;</span> weightedGraph <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">ValueGraphBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>directed()<span class="pl-k" style="color: #d73a49;">.</span>build();
weightedGraph<span class="pl-k" style="color: #d73a49;">.</span>addNode(<span class="pl-c1" style="color: #005cc5;">1</span>);
weightedGraph<span class="pl-k" style="color: #d73a49;">.</span>putEdgeValue(<span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>, <span class="pl-c1" style="color: #005cc5;">1.5</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> also adds nodes 2 and 3 if not already present</span>
weightedGraph<span class="pl-k" style="color: #d73a49;">.</span>putEdgeValue(<span class="pl-c1" style="color: #005cc5;">3</span>, <span class="pl-c1" style="color: #005cc5;">5</span>, <span class="pl-c1" style="color: #005cc5;">1.5</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> edge values (like Map values) need not be unique</span>
<span class="pl-c1" style="color: #005cc5;">...</span>
weightedGraph<span class="pl-k" style="color: #d73a49;">.</span>putEdgeValue(<span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>, <span class="pl-c1" style="color: #005cc5;">2.0</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> updates the value for (2,3) to 2.0</span></pre> 
 </div> 
 <h3 style=""> <a id="user-content-basic-network-example" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#basic-network-example"></a>Basic&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/graph/Network.html"><code style="">Network</code></a>&nbsp;example</h3> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">MutableNetwork&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>, <span class="pl-smi" style="color: #24292e;">String</span>&gt;</span> network <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">NetworkBuilder</span><span class="pl-k" style="color: #d73a49;">.</span>directed()<span class="pl-k" style="color: #d73a49;">.</span>build();
network<span class="pl-k" style="color: #d73a49;">.</span>addNode(<span class="pl-c1" style="color: #005cc5;">1</span>);
network<span class="pl-k" style="color: #d73a49;">.</span>addEdge(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>2-&gt;3<span class="pl-pds" style="">"</span></span>, <span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> also adds nodes 2 and 3 if not already present</span>

<span class="pl-k" style="color: #d73a49;">Set&lt;<span class="pl-smi" style="color: #24292e;">Integer</span>&gt;</span> successorsOfTwo <span class="pl-k" style="color: #d73a49;">=</span> network<span class="pl-k" style="color: #d73a49;">.</span>successors(<span class="pl-c1" style="color: #005cc5;">2</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> returns {3}</span>
<span class="pl-k" style="color: #d73a49;">Set&lt;<span class="pl-smi" style="color: #24292e;">String</span>&gt;</span> outEdgesOfTwo <span class="pl-k" style="color: #d73a49;">=</span> network<span class="pl-k" style="color: #d73a49;">.</span>outEdges(<span class="pl-c1" style="color: #005cc5;">2</span>);   <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> returns {"2-&gt;3"}</span>

network<span class="pl-k" style="color: #d73a49;">.</span>addEdge(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>2-&gt;3 too<span class="pl-pds" style="">"</span></span>, <span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> throws; Network disallows parallel edges</span>
                                    <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> by default</span>
network<span class="pl-k" style="color: #d73a49;">.</span>addEdge(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>2-&gt;3<span class="pl-pds" style="">"</span></span>, <span class="pl-c1" style="color: #005cc5;">2</span>, <span class="pl-c1" style="color: #005cc5;">3</span>);  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> no effect; this edge is already present</span>
                                <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> and connecting these nodes in this order</span>

<span class="pl-k" style="color: #d73a49;">Set&lt;<span class="pl-smi" style="color: #24292e;">String</span>&gt;</span> inEdgesOfFour <span class="pl-k" style="color: #d73a49;">=</span> network<span class="pl-k" style="color: #d73a49;">.</span>inEdges(<span class="pl-c1" style="color: #005cc5;">4</span>); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> throws; node not in graph</span></pre> 
 </div> 
 <h3 style=""> <a id="user-content-traversing-an-undirected-graph-node-wise" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#traversing-an-undirected-graph-node-wise"></a>Traversing an undirected graph node-wise</h3> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> Return all nodes reachable by traversing 2 edges starting from "node"</span>
<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> (ignoring edge direction and edge weights, if any, and not including "node").</span>
<span class="pl-k" style="color: #d73a49;">Set&lt;<span class="pl-smi" style="color: #24292e;">N</span>&gt;</span> getTwoHopNeighbors(<span class="pl-k" style="color: #d73a49;">Graph&lt;<span class="pl-smi" style="color: #24292e;">N</span>&gt;</span> graph, <span class="pl-smi" style="color: #24292e;">N</span> node) {
  <span class="pl-k" style="color: #d73a49;">Set&lt;<span class="pl-smi" style="color: #24292e;">N</span>&gt;</span> twoHopNeighbors <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-k" style="color: #d73a49;">HashSet&lt;&gt;</span>();
  <span class="pl-k" style="color: #d73a49;">for</span> (<span class="pl-smi" style="color: #24292e;">N</span> neighbor <span class="pl-k" style="color: #d73a49;">:</span> graph<span class="pl-k" style="color: #d73a49;">.</span>adjacentNodes(node)) {
    twoHopNeighbors<span class="pl-k" style="color: #d73a49;">.</span>addAll(graph<span class="pl-k" style="color: #d73a49;">.</span>adjacentNodes(neighbor));
  }
  twoHopNeighbors<span class="pl-k" style="color: #d73a49;">.</span>remove(node);
  <span class="pl-k" style="color: #d73a49;">return</span> twoHopNeighbors;
}</pre> 
 </div> 
 <h3 style=""> <a id="user-content-traversing-a-directed-graph-edge-wise" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#traversing-a-directed-graph-edge-wise"></a>Traversing a directed graph edge-wise</h3> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> Update the shortest-path weighted distances of the successors to "node"</span>
<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> in a directed Network (inner loop of Dijkstra's algorithm)</span>
<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> given a known distance for {@code node} stored in a {@code Map&lt;N, Double&gt;},</span>
<span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> and a {@code Function&lt;E, Double&gt;} for retrieving a weight for an edge.</span>
<span class="pl-k" style="color: #d73a49;">void</span> updateDistancesFrom(<span class="pl-k" style="color: #d73a49;">Network&lt;<span class="pl-smi" style="color: #24292e;">N</span>, <span class="pl-smi" style="color: #24292e;">E</span>&gt;</span> network, <span class="pl-smi" style="color: #24292e;">N</span> node) {
  <span class="pl-k" style="color: #d73a49;">double</span> nodeDistance <span class="pl-k" style="color: #d73a49;">=</span> distances<span class="pl-k" style="color: #d73a49;">.</span>get(node);
  <span class="pl-k" style="color: #d73a49;">for</span> (<span class="pl-smi" style="color: #24292e;">E</span> outEdge <span class="pl-k" style="color: #d73a49;">:</span> network<span class="pl-k" style="color: #d73a49;">.</span>outEdges(node)) {
    <span class="pl-smi" style="color: #24292e;">N</span> target <span class="pl-k" style="color: #d73a49;">=</span> network<span class="pl-k" style="color: #d73a49;">.</span>target(outEdge);
    <span class="pl-k" style="color: #d73a49;">double</span> targetDistance <span class="pl-k" style="color: #d73a49;">=</span> nodeDistance <span class="pl-k" style="color: #d73a49;">+</span> edgeWeights<span class="pl-k" style="color: #d73a49;">.</span>apply(outEdge);
    <span class="pl-k" style="color: #d73a49;">if</span> (targetDistance <span class="pl-k" style="color: #d73a49;">&lt;</span> distances<span class="pl-k" style="color: #d73a49;">.</span>getOrDefault(target, <span class="pl-smi" style="color: #24292e;">Double</span><span class="pl-c1" style="color: #005cc5;"><span class="pl-k" style="color: #d73a49;">.</span>MAX_VALUE</span>)) {
      distances<span class="pl-k" style="color: #d73a49;">.</span>put(target, targetDistance);
    }
  }
}</pre> 
 </div> 
 <h2 style=""> <a id="user-content-faq" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#faq"></a>FAQ</h2> 
 <h3 style=""> <a id="user-content-why-did-guava-introduce-commongraph" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#why-did-guava-introduce-commongraph"></a>Why did Guava introduce&nbsp;<code style="">common.graph</code>?</h3> 
 <p style="">The same arguments apply to graphs as to many other things that Guava does:</p> 
 <ul style=""> 
  <li style="">code reuse/interoperability/unification of paradigms: lots of things relate to graph processing</li> 
  <li style="margin-top: 0.25em;">efficiency: how much code is using inefficient graph representations? too much space (e.g. matrix representations)?</li> 
  <li style="margin-top: 0.25em;">correctness: how much code is doing graph analysis wrong?</li> 
  <li style="margin-top: 0.25em;">promotion of use of graph as ADT: how many people would be working with graphs if it were easy?</li> 
  <li style="margin-top: 0.25em;">simplicity: code which deals with graphs is easier to understand if it’s explicitly using that metaphor.</li> 
 </ul> 
 <h3 style=""> <a id="user-content-what-kinds-of-graphs-does-commongraph-support" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#what-kinds-of-graphs-does-commongraph-support"></a>What kinds of graphs does&nbsp;<code style="">common.graph</code>&nbsp;support?</h3> 
 <p style="">This is answered in the&nbsp;<a style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/wiki/GraphsExplained#capabilities">"Capabilities"</a>&nbsp;section, above.</p> 
 <h3 style=""> <a id="user-content-commongraph-doesnt-have-featurealgorithm-x-can-you-add-it" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#commongraph-doesnt-have-featurealgorithm-x-can-you-add-it"></a><code style="">common.graph</code>&nbsp;doesn’t have feature/algorithm X, can you add it?</h3> 
 <p style="">Maybe. You can email us at&nbsp;<code style="">guava-discuss@googlegroups.com</code>&nbsp;or&nbsp;<a style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/issues">open an issue on GitHub</a>.</p> 
 <p style="">Our philosophy is that something should only be part of Guava if (a) it fits in with Guava’s core mission and (b) there is good reason to expect that it will be reasonably widely used.</p> 
 <p style=""><code style="">common.graph</code>&nbsp;will probably never have capabilities like visualization and I/O; those would be projects unto themselves and don’t fit well with Guava’s mission.</p> 
 <p style="">Capabilities like traversal, filtering, or transformation are better fits, and thus more likely to be included, although ultimately we expect that other graph libraries will provide most capabilities.</p> 
 <h3 style=""> <a id="user-content-does-it-support-very-large-graphs-ie-mapreduce-scale" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#does-it-support-very-large-graphs-ie-mapreduce-scale"></a>Does it support very large graphs (i.e., MapReduce scale)?</h3> 
 <p style="">Not at this time. Graphs in the low millions of nodes should be workable, but you should think of this library as analogous to the Java Collections Framework types (<code style="">Map</code>,&nbsp;<code style="">List</code>,&nbsp;<code style="">Set</code>, and so on).</p> 
 <h3 style=""> <a id="user-content-why-should-i-use-it-instead-of-something-else" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#why-should-i-use-it-instead-of-something-else"></a>Why should I use it instead of something else?</h3> 
 <p style=""><span style="font-weight: 600;">tl;dr</span>: you should use whatever works for you, but please let us know what you need if this library doesn't support it!</p> 
 <p style="">The main competitors to this library (for Java) are:&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://jung.sf.net/">JUNG</a>&nbsp;and&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://jgrapht.org/">JGraphT</a>.</p> 
 <p style=""><code style="">JUNG</code>&nbsp;was co-created by Joshua O'Madadhain (the&nbsp;<code style="">common.graph</code>&nbsp;lead) in 2003, and he still maintains it. JUNG is fairly mature and full-featured and is widely used, but has a lot of cruft and inefficiencies. Now that&nbsp;<code style="">common.graph</code>&nbsp;has been released externally, he plans to create a new version of&nbsp;<code style="">JUNG</code>&nbsp;which uses&nbsp;<code style="">common.graph</code>&nbsp;for its data model.</p> 
 <p style=""><code style="">JGraphT</code>&nbsp;is another third-party Java graph library that’s been around for a while. We're not as familiar with it, so we can’t comment on it in detail, but it has at least some things in common with&nbsp;<code style="">JUNG</code>.</p> 
 <p style="">Rolling your own solution is sometimes the right answer if you have very specific requirements. But just as you wouldn’t normally implement your own hash table in Java (instead of using&nbsp;<code style="">HashMap</code>&nbsp;or&nbsp;<code style="">ImmutableMap</code>), you should consider using&nbsp;<code style="">common.graph</code>&nbsp;(or, if necessary, another existing graph library) for all the reasons listed above.</p> 
 <h2 style=""> <a id="user-content-major-contributors" class="anchor" style="" href="https://github.com/google/guava/wiki/GraphsExplained#major-contributors"></a>Major Contributors</h2> 
 <p style=""><code style="">common.graph</code>&nbsp;has been a team effort, and we've had help from a number of people both inside and outside Google, but these are the people that have had the greatest impact.</p> 
 <ul style=""> 
  <li style=""> <span style="font-weight: 600;">Omar Darwish</span>&nbsp;did a lot of the early implementations, and set the standard for the test coverage.</li> 
  <li style="margin-top: 0.25em;"> <a style="background-color: transparent; color: #0366d6;" href="https://github.com/bezier89"><span style="font-weight: 600;">James Sexton</span></a>&nbsp;has been the single most prolific contributor to the project and has had a significant influence on its direction and its designs. He's responsible for some of the key features, and for the efficiency of the implementations that we provide.</li> 
  <li style="margin-top: 0.25em;"> <a style="background-color: transparent; color: #0366d6;" href="https://github.com/jrtom"><span style="font-weight: 600;">Joshua O'Madadhain</span></a>&nbsp;started the&nbsp;<code style="">common.graph</code>&nbsp;project after reflecting on the strengths and weaknesses of&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://jung.sf.net/">JUNG</a>, which he also helped to create. He leads the project, and has reviewed or written virtually every aspect of the design and the code.</li> 
 </ul> 
</div>