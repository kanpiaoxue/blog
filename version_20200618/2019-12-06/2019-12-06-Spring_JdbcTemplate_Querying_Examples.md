#Spring JdbcTemplate Querying Examples
###发表时间：2019-12-06
###分类：Spring,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2510843" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2510843</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>Spring JdbcTemplate Querying Examples</p> 
 <p>参考地址：&nbsp;<a href="https://www.mkyong.com/spring/spring-jdbctemplate-querying-examples/">https://www.mkyong.com/spring/spring-jdbctemplate-querying-examples/</a></p> 
 <p>&nbsp;</p> 
 <p style="">Here are a few examples to show you how to use Spring&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">JdbcTemplate</code>&nbsp;to query or extract data from database.</p> 
 <p style="">Technologies used :</p> 
 <ul style=""> 
  <li style="">Spring Boot 2.1.2.RELEASE</li> 
  <li style="">Spring JDBC 5.1.4.RELEASE</li> 
  <li style="">Maven 3</li> 
  <li style="">Java 8</li> 
 </ul> 
 <p style="">In Short:</p> 
 <ul style=""> 
  <li style=""> <code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">jdbcTemplate.queryForObject</code>&nbsp;for single row or value</li> 
  <li style=""> <code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">jdbcTemplate.query</code>&nbsp;for multiple rows or list</li> 
 </ul> 
 <div class="note" style=""> 
  <span style="font-weight: bolder;">Note</span>
  <br style="">The article is updated from Spring core 2.5.x to Spring Boot 2.1.x
 </div> 
 <p style=""><em style="">P.S You may also interested in this&nbsp;<a style="color: #0056b3; background-color: transparent;" href="https://www.mkyong.com/spring-boot/spring-boot-jdbc-examples/" rel="noopener noreferrer" target="_blank">Spring Boot JDBC Examples</a></em></p> 
 <h2 style="">1. Query for Single Row</h2> 
 <p style="">In Spring, we can use&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">jdbcTemplate.queryForObject()</code>&nbsp;to query a single row record from database, and convert the row into an object via row mapper.</p> 
 <p style="">1.1 Custom RowMapper</p> 
 <div class="filename" style="">
  CustomerRowMapper.java
 </div> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;"><span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>jdbc<span class="token punctuation" style="color: #999999;">.</span>core<span class="token punctuation" style="color: #999999;">.</span>RowMapper<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>sql<span class="token punctuation" style="color: #999999;">.</span>ResultSet<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>sql<span class="token punctuation" style="color: #999999;">.</span>SQLException<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">class</span> <span class="token class-name" style="">CustomerRowMapper</span> <span class="token keyword" style="color: #0077aa;">implements</span> <span class="token class-name" style="">RowMapper</span><span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> <span class="token punctuation" style="color: #999999;">{</span>

    <span class="token annotation punctuation" style="color: #999999;">@Override</span>
    <span class="token keyword" style="color: #0077aa;">public</span> Customer <span class="token function" style="color: #dd4a68;">mapRow</span><span class="token punctuation" style="color: #999999;">(</span>ResultSet rs<span class="token punctuation" style="color: #999999;">,</span> <span class="token keyword" style="color: #0077aa;">int</span> rowNum<span class="token punctuation" style="color: #999999;">)</span> <span class="token keyword" style="color: #0077aa;">throws</span> SQLException <span class="token punctuation" style="color: #999999;">{</span>

        Customer customer <span class="token operator" style="">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        customer<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setID</span><span class="token punctuation" style="color: #999999;">(</span>rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getLong</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"ID"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        customer<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setName</span><span class="token punctuation" style="color: #999999;">(</span>rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"NAME"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        customer<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setAge</span><span class="token punctuation" style="color: #999999;">(</span>rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getInt</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"AGE"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        customer<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setCreatedDate</span><span class="token punctuation" style="color: #999999;">(</span>rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getTimestamp</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"created_date"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toLocalDateTime</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> customer<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>
<span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;"><span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>jdbc<span class="token punctuation" style="color: #999999;">.</span>core<span class="token punctuation" style="color: #999999;">.</span>JdbcTemplate<span class="token punctuation" style="color: #999999;">;</span>

	<span class="token annotation punctuation" style="color: #999999;">@Autowired</span>
    <span class="token keyword" style="color: #0077aa;">private</span> JdbcTemplate jdbcTemplate<span class="token punctuation" style="color: #999999;">;</span>
	
	<span class="token keyword" style="color: #0077aa;">public</span> Customer <span class="token function" style="color: #dd4a68;">findByCustomerId</span><span class="token punctuation" style="color: #999999;">(</span>Long id<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER WHERE ID = ?"</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">queryForObject</span><span class="token punctuation" style="color: #999999;">(</span>sql<span class="token punctuation" style="color: #999999;">,</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Object</span><span class="token punctuation" style="color: #999999;">[</span><span class="token punctuation" style="color: #999999;">]</span><span class="token punctuation" style="color: #999999;">{</span>id<span class="token punctuation" style="color: #999999;">}</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">CustomerRowMapper</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">1.2 Spring&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">BeanPropertyRowMapper</code>, this class saves you a lot of time for the mapping.</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;"><span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>jdbc<span class="token punctuation" style="color: #999999;">.</span>core<span class="token punctuation" style="color: #999999;">.</span>BeanPropertyRowMapper<span class="token punctuation" style="color: #999999;">;</span>
	
    <span class="token keyword" style="color: #0077aa;">public</span> Customer <span class="token function" style="color: #dd4a68;">findByCustomerId2</span><span class="token punctuation" style="color: #999999;">(</span>Long id<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER WHERE ID = ?"</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> <span class="token punctuation" style="color: #999999;">(</span>Customer<span class="token punctuation" style="color: #999999;">)</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">queryForObject</span><span class="token punctuation" style="color: #999999;">(</span>
			sql<span class="token punctuation" style="color: #999999;">,</span> 
			<span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Object</span><span class="token punctuation" style="color: #999999;">[</span><span class="token punctuation" style="color: #999999;">]</span><span class="token punctuation" style="color: #999999;">{</span>id<span class="token punctuation" style="color: #999999;">}</span><span class="token punctuation" style="color: #999999;">,</span> 
			<span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">BeanPropertyRowMapper</span><span class="token punctuation" style="color: #999999;">(</span>Customer<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">1.3 In Java 8, we can map it directly:</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">    <span class="token keyword" style="color: #0077aa;">public</span> Customer <span class="token function" style="color: #dd4a68;">findByCustomerId3</span><span class="token punctuation" style="color: #999999;">(</span>Long id<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER WHERE ID = ?"</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">queryForObject</span><span class="token punctuation" style="color: #999999;">(</span>sql<span class="token punctuation" style="color: #999999;">,</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Object</span><span class="token punctuation" style="color: #999999;">[</span><span class="token punctuation" style="color: #999999;">]</span><span class="token punctuation" style="color: #999999;">{</span>id<span class="token punctuation" style="color: #999999;">}</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token punctuation" style="color: #999999;">(</span>rs<span class="token punctuation" style="color: #999999;">,</span> rowNum<span class="token punctuation" style="color: #999999;">)</span> <span class="token operator" style="">-</span><span class="token operator" style="">&gt;</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span>
                        rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getLong</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"id"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                        rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"name"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                        rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getInt</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"age"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                        rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getTimestamp</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"created_date"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toLocalDateTime</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span>
                <span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}




</span></code></pre> 
 <h2 style="">2. Query for Multiple Rows</h2> 
 <p style="">For multiple rows, we use&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">jdbcTemplate.query()</code></p> 
 <p style="">2.1 Custom RowMapper</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">	<span class="token keyword" style="color: #0077aa;">public</span> List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> <span class="token function" style="color: #dd4a68;">findAll</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
	
        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER"</span><span class="token punctuation" style="color: #999999;">;</span>

        List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> customers <span class="token operator" style="">=</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">query</span><span class="token punctuation" style="color: #999999;">(</span>
                sql<span class="token punctuation" style="color: #999999;">,</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">CustomerRowMapper</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> customers<span class="token punctuation" style="color: #999999;">;</span>
		
    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">2.2&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">BeanPropertyRowMapper</code></p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">    <span class="token keyword" style="color: #0077aa;">public</span> List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> <span class="token function" style="color: #dd4a68;">findAll</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER"</span><span class="token punctuation" style="color: #999999;">;</span>

        List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> customers <span class="token operator" style="">=</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">query</span><span class="token punctuation" style="color: #999999;">(</span>
                sql<span class="token punctuation" style="color: #999999;">,</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">BeanPropertyRowMapper</span><span class="token punctuation" style="color: #999999;">(</span>Customer<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> customers<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">2.3 Java 8</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">    <span class="token keyword" style="color: #0077aa;">public</span> List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> <span class="token function" style="color: #dd4a68;">findAll</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER"</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">query</span><span class="token punctuation" style="color: #999999;">(</span>
                sql<span class="token punctuation" style="color: #999999;">,</span>
                <span class="token punctuation" style="color: #999999;">(</span>rs<span class="token punctuation" style="color: #999999;">,</span> rowNum<span class="token punctuation" style="color: #999999;">)</span> <span class="token operator" style="">-</span><span class="token operator" style="">&gt;</span>
                        <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span>
                                rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getLong</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"id"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                                rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getString</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"name"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                                rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getInt</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"age"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                                rs<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getTimestamp</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"created_date"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toLocalDateTime</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span>
                        <span class="token punctuation" style="color: #999999;">)</span>
        <span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">2.4&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">jdbcTemplate.queryForList</code>, it works, but not recommend, the mapping in&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">Map</code>&nbsp;may not same as the object, need casting.</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">	<span class="token keyword" style="color: #0077aa;">public</span> List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> <span class="token function" style="color: #dd4a68;">findAll</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT * FROM CUSTOMER"</span><span class="token punctuation" style="color: #999999;">;</span>

        List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> customers <span class="token operator" style="">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">ArrayList</span><span class="token operator" style="">&lt;</span><span class="token operator" style="">&gt;</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        List<span class="token operator" style="">&lt;</span>Map<span class="token operator" style="">&lt;</span>String<span class="token punctuation" style="color: #999999;">,</span> Object<span class="token operator" style="">&gt;&gt;</span> rows <span class="token operator" style="">=</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">queryForList</span><span class="token punctuation" style="color: #999999;">(</span>sql<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">for</span> <span class="token punctuation" style="color: #999999;">(</span>Map row <span class="token operator" style="">:</span> rows<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
            Customer obj <span class="token operator" style="">=</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

            obj<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setID</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span>Integer<span class="token punctuation" style="color: #999999;">)</span> row<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">get</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"ID"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">longValue</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            obj<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setName</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span>String<span class="token punctuation" style="color: #999999;">)</span> row<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">get</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"NAME"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
			<span class="token comment" style="color: #708090;">// Spring returns BigDecimal, need convert</span>
            obj<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setAge</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span>BigDecimal<span class="token punctuation" style="color: #999999;">)</span> row<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">get</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"AGE"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">intValue</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span> 
            obj<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">setCreatedDate</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">(</span>Timestamp<span class="token punctuation" style="color: #999999;">)</span> row<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">get</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"CREATED_DATE"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">toLocalDateTime</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            customers<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">add</span><span class="token punctuation" style="color: #999999;">(</span>obj<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        <span class="token punctuation" style="color: #999999;">}</span>

        <span class="token keyword" style="color: #0077aa;">return</span> customers<span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <h2 style="">3. Query for a Single Value</h2> 
 <p style="">It’s same like query a single row from database, uses&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">jdbcTemplate.queryForObject()</code></p> 
 <p style="">3.1 Single column name</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">	<span class="token keyword" style="color: #0077aa;">public</span> String <span class="token function" style="color: #dd4a68;">findCustomerNameById</span><span class="token punctuation" style="color: #999999;">(</span>Long id<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT NAME FROM CUSTOMER WHERE ID = ?"</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token keyword" style="color: #0077aa;">return</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">queryForObject</span><span class="token punctuation" style="color: #999999;">(</span>
                sql<span class="token punctuation" style="color: #999999;">,</span> <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Object</span><span class="token punctuation" style="color: #999999;">[</span><span class="token punctuation" style="color: #999999;">]</span><span class="token punctuation" style="color: #999999;">{</span>id<span class="token punctuation" style="color: #999999;">}</span><span class="token punctuation" style="color: #999999;">,</span> String<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">3.2 Count</p> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">    <span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">int</span> <span class="token function" style="color: #dd4a68;">count</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        String sql <span class="token operator" style="">=</span> <span class="token string" style="color: #669900;">"SELECT COUNT(*) FROM CUSTOMER"</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token comment" style="color: #708090;">// queryForInt() is Deprecated</span>
        <span class="token comment" style="color: #708090;">// https://www.mkyong.com/spring/jdbctemplate-queryforint-is-deprecated/</span>
        <span class="token comment" style="color: #708090;">//int total = jdbcTemplate.queryForInt(sql);</span>

        <span class="token keyword" style="color: #0077aa;">return</span> jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">queryForObject</span><span class="token punctuation" style="color: #999999;">(</span>sql<span class="token punctuation" style="color: #999999;">,</span> Integer<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <h2 style="">4. Test</h2> 
 <p style="">Run a Spring Boot&nbsp;<code style="font-family: SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 14px; color: #e83e8c;">CommandLineRunner</code>&nbsp;application, create tables and test the APIs.</p> 
 <div class="filename" style="">
  pom.xml
 </div> 
 <pre class="language-markup code-toolbar"><code class=" language-markup" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">	<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;</span>dependency</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
		<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;</span>groupId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>org.springframework.boot<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;/</span>groupId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
		<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;</span>artifactId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>spring-boot-starter-jdbc<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;/</span>artifactId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
	<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;/</span>dependency</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>

	<span class="token comment" style="color: #708090;">&lt;!-- in-memory database --&gt;</span>
	<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;</span>dependency</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
		<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;</span>groupId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>com.h2database<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;/</span>groupId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
		<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;</span>artifactId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>h2<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;/</span>artifactId</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
	<span class="token tag" style="color: #990055;"><span class="token tag" style=""><span class="token punctuation" style="color: #999999;">&lt;/</span>dependency</span><span class="token punctuation" style="color: #999999;">&gt;</span></span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <div class="filename" style="">
  StartApplication.java
 </div> 
 <pre class="language-java code-toolbar"><code class=" language-java" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;"><span class="token keyword" style="color: #0077aa;">package</span> com<span class="token punctuation" style="color: #999999;">.</span>mkyong<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> com<span class="token punctuation" style="color: #999999;">.</span>mkyong<span class="token punctuation" style="color: #999999;">.</span>customer<span class="token punctuation" style="color: #999999;">.</span>Customer<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> com<span class="token punctuation" style="color: #999999;">.</span>mkyong<span class="token punctuation" style="color: #999999;">.</span>customer<span class="token punctuation" style="color: #999999;">.</span>CustomerRepository<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>slf4j<span class="token punctuation" style="color: #999999;">.</span>Logger<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>slf4j<span class="token punctuation" style="color: #999999;">.</span>LoggerFactory<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>beans<span class="token punctuation" style="color: #999999;">.</span>factory<span class="token punctuation" style="color: #999999;">.</span>annotation<span class="token punctuation" style="color: #999999;">.</span>Autowired<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>boot<span class="token punctuation" style="color: #999999;">.</span>CommandLineRunner<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>boot<span class="token punctuation" style="color: #999999;">.</span>SpringApplication<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>boot<span class="token punctuation" style="color: #999999;">.</span>autoconfigure<span class="token punctuation" style="color: #999999;">.</span>SpringBootApplication<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> org<span class="token punctuation" style="color: #999999;">.</span>springframework<span class="token punctuation" style="color: #999999;">.</span>jdbc<span class="token punctuation" style="color: #999999;">.</span>core<span class="token punctuation" style="color: #999999;">.</span>JdbcTemplate<span class="token punctuation" style="color: #999999;">;</span>

<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>math<span class="token punctuation" style="color: #999999;">.</span>BigDecimal<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>util<span class="token punctuation" style="color: #999999;">.</span>Arrays<span class="token punctuation" style="color: #999999;">;</span>
<span class="token keyword" style="color: #0077aa;">import</span> java<span class="token punctuation" style="color: #999999;">.</span>util<span class="token punctuation" style="color: #999999;">.</span>List<span class="token punctuation" style="color: #999999;">;</span>

<span class="token annotation punctuation" style="color: #999999;">@SpringBootApplication</span>
<span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">class</span> <span class="token class-name" style="">StartApplication</span> <span class="token keyword" style="color: #0077aa;">implements</span> <span class="token class-name" style="">CommandLineRunner</span> <span class="token punctuation" style="color: #999999;">{</span>

    <span class="token keyword" style="color: #0077aa;">private</span> <span class="token keyword" style="color: #0077aa;">static</span> <span class="token keyword" style="color: #0077aa;">final</span> Logger log <span class="token operator" style="">=</span> LoggerFactory<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getLogger</span><span class="token punctuation" style="color: #999999;">(</span>StartApplication<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@Autowired</span>
    JdbcTemplate jdbcTemplate<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token annotation punctuation" style="color: #999999;">@Autowired</span>
    CustomerRepository customerRepository<span class="token punctuation" style="color: #999999;">;</span>

    <span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">static</span> <span class="token keyword" style="color: #0077aa;">void</span> <span class="token function" style="color: #dd4a68;">main</span><span class="token punctuation" style="color: #999999;">(</span>String<span class="token punctuation" style="color: #999999;">[</span><span class="token punctuation" style="color: #999999;">]</span> args<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>
        SpringApplication<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">run</span><span class="token punctuation" style="color: #999999;">(</span>StartApplication<span class="token punctuation" style="color: #999999;">.</span><span class="token keyword" style="color: #0077aa;">class</span><span class="token punctuation" style="color: #999999;">,</span> args<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token annotation punctuation" style="color: #999999;">@Override</span>
    <span class="token keyword" style="color: #0077aa;">public</span> <span class="token keyword" style="color: #0077aa;">void</span> <span class="token function" style="color: #dd4a68;">run</span><span class="token punctuation" style="color: #999999;">(</span>String<span class="token punctuation" style="color: #999999;">.</span><span class="token punctuation" style="color: #999999;">.</span><span class="token punctuation" style="color: #999999;">.</span> args<span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"StartApplication..."</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        <span class="token function" style="color: #dd4a68;">startCustomerApp</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>

    <span class="token comment" style="color: #708090;">// Tested with H2 database</span>
    <span class="token keyword" style="color: #0077aa;">void</span> <span class="token function" style="color: #dd4a68;">startCustomerApp</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span> <span class="token punctuation" style="color: #999999;">{</span>

        jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">execute</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"DROP TABLE customer IF EXISTS"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        jdbcTemplate<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">execute</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"CREATE TABLE customer("</span> <span class="token operator" style="">+</span>
                <span class="token string" style="color: #669900;">"id SERIAL, name VARCHAR(255), age NUMERIC(2), created_date timestamp)"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        List<span class="token operator" style="">&lt;</span>Customer<span class="token operator" style="">&gt;</span> list <span class="token operator" style="">=</span> Arrays<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">asList</span><span class="token punctuation" style="color: #999999;">(</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Customer A"</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token number" style="color: #990055;">19</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Customer B"</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token number" style="color: #990055;">20</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Customer C"</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token number" style="color: #990055;">21</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">,</span>
                <span class="token keyword" style="color: #0077aa;">new</span> <span class="token class-name" style="">Customer</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Customer D"</span><span class="token punctuation" style="color: #999999;">,</span> <span class="token number" style="color: #990055;">22</span><span class="token punctuation" style="color: #999999;">)</span>
        <span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        list<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">forEach</span><span class="token punctuation" style="color: #999999;">(</span>x <span class="token operator" style="">-</span><span class="token operator" style="">&gt;</span> <span class="token punctuation" style="color: #999999;">{</span>
            log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"Saving...{}"</span><span class="token punctuation" style="color: #999999;">,</span> x<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">getName</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
            customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">save</span><span class="token punctuation" style="color: #999999;">(</span>x<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        <span class="token punctuation" style="color: #999999;">}</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"[FIND_BY_ID]"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findByCustomerId</span><span class="token punctuation" style="color: #999999;">(</span>1L<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findByCustomerId2</span><span class="token punctuation" style="color: #999999;">(</span>2L<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findByCustomerId3</span><span class="token punctuation" style="color: #999999;">(</span>3L<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"[FIND_ALL]"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findAll</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findAll2</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findAll3</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findAll4</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"[FIND_NAME_BY_ID]"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">findCustomerNameById</span><span class="token punctuation" style="color: #999999;">(</span>4L<span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"[COUNT]"</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>
        log<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">info</span><span class="token punctuation" style="color: #999999;">(</span><span class="token string" style="color: #669900;">"{}"</span><span class="token punctuation" style="color: #999999;">,</span> customerRepository<span class="token punctuation" style="color: #999999;">.</span><span class="token function" style="color: #dd4a68;">count</span><span class="token punctuation" style="color: #999999;">(</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">)</span><span class="token punctuation" style="color: #999999;">;</span>

    <span class="token punctuation" style="color: #999999;">}</span>

<span class="token punctuation" style="color: #999999;">}</span>
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <p style="">Output</p> 
 <pre class="language-bash code-toolbar"><code class=" language-bash" style="font-family: Consolas, Monaco, 'andale mono', 'ubuntu mono', monospace; font-size: inherit; background: 0px 0px; line-height: 1.5;">INFO  com.mkyong.StartApplication - Saving<span class="token punctuation" style="color: #999999;">..</span>.Customer A
INFO  com.mkyong.StartApplication - Saving<span class="token punctuation" style="color: #999999;">..</span>.Customer B
INFO  com.mkyong.StartApplication - Saving<span class="token punctuation" style="color: #999999;">..</span>.Customer C
INFO  com.mkyong.StartApplication - Saving<span class="token punctuation" style="color: #999999;">..</span>.Customer D
INFO  com.mkyong.StartApplication - <span class="token punctuation" style="color: #999999;">[</span>FIND_BY_ID<span class="token punctuation" style="color: #999999;">]</span>
INFO  com.mkyong.StartApplication - Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>1, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer A'</span>, age<span class="token operator" style="">=</span>19, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.950848<span class="token punctuation" style="color: #999999;">}</span>
INFO  com.mkyong.StartApplication - Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>2, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer B'</span>, age<span class="token operator" style="">=</span>20, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.961819<span class="token punctuation" style="color: #999999;">}</span>
INFO  com.mkyong.StartApplication - Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>3, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer C'</span>, age<span class="token operator" style="">=</span>21, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.961819<span class="token punctuation" style="color: #999999;">}</span>
INFO  com.mkyong.StartApplication - <span class="token punctuation" style="color: #999999;">[</span>FIND_ALL<span class="token punctuation" style="color: #999999;">]</span>
INFO  com.mkyong.StartApplication - <span class="token punctuation" style="color: #999999;">[</span>
	Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>1, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer A'</span>, age<span class="token operator" style="">=</span>19, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.950848<span class="token punctuation" style="color: #999999;">}</span>, 
	Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>2, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer B'</span>, age<span class="token operator" style="">=</span>20, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.961819<span class="token punctuation" style="color: #999999;">}</span>, 
	Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>3, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer C'</span>, age<span class="token operator" style="">=</span>21, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.961819<span class="token punctuation" style="color: #999999;">}</span>, 
	Customer<span class="token punctuation" style="color: #999999;">{</span>ID<span class="token operator" style="">=</span>4, name<span class="token operator" style="">=</span><span class="token string" style="color: #669900;">'Customer D'</span>, age<span class="token operator" style="">=</span>22, createdDate<span class="token operator" style="">=</span>2019-08-01T15:48:45.961819<span class="token punctuation" style="color: #999999;">}</span>
	<span class="token punctuation" style="color: #999999;">]</span>
//<span class="token punctuation" style="color: #999999;">..</span>.omitted, duplicate code
INFO  com.mkyong.StartApplication - <span class="token punctuation" style="color: #999999;">[</span>FIND_NAME_BY_ID<span class="token punctuation" style="color: #999999;">]</span>
INFO  com.mkyong.StartApplication - Customer D
INFO  com.mkyong.StartApplication - <span class="token punctuation" style="color: #999999;">[</span>COUNT<span class="token punctuation" style="color: #999999;">]</span>
INFO  com.mkyong.StartApplication - 4
</code></pre> 
 <div class="toolbar" style=""> 
  <div class="toolbar-item" style="display: inline-block;">
   <a style="">Copy</a>
  </div> 
 </div> 
 <h2 style="">Download Source Code</h2> 
 <div class="github" style="">
  $ git clone&nbsp;
  <a style="color: #0056b3; background-color: transparent;" href="https://github.com/mkyong/spring-boot.git" rel="noopener noreferrer" target="_blank">https://github.com/mkyong/spring-boot.git</a>
  <br style="">$ cd spring-jdbc
  <br style="">$ find com.mkyong.customer
 </div> 
 <h2 style="">References</h2> 
 <ul style=""> 
  <li style=""> <a style="color: #0056b3; background-color: transparent;" href="https://www.mkyong.com/spring-boot/spring-boot-jdbc-examples/" rel="noopener noreferrer" target="_blank">Spring Boot JDBC Examples</a>_</li> 
  <li style=""><a style="color: #0056b3; background-color: transparent;" href="https://www.h2database.com/html/main.html" rel="noopener noreferrer" target="_blank">H2 Database Engine</a></li> 
  <li style=""><a style="color: #0056b3; background-color: transparent;" href="https://docs.spring.io/spring/docs/current/spring-framework-reference/data-access.html#jdbc" rel="noopener noreferrer" target="_blank">Spring JDBC docs</a></li> 
  <li style=""><a style="color: #0056b3; background-color: transparent;" href="https://docs.spring.io/spring-boot/docs/2.1.3.RELEASE/reference/htmlsingle/#boot-features-sql" rel="noopener noreferrer" target="_blank">Working with SQL Databases</a></li> 
  <li style=""><a style="color: #0056b3; background-color: transparent;" href="https://www.mkyong.com/spring/jdbctemplate-queryforint-is-deprecated/" rel="noopener noreferrer" target="_blank">JdbcTemplate queryForInt() is Deprecated</a></li> 
  <li style=""><a style="color: #0056b3; background-color: transparent;" href="https://www.mkyong.com/tutorials/jdbc-tutorials/" rel="noopener noreferrer" target="_blank">Java JDBC Tutorial</a></li> 
 </ul> 
</div>