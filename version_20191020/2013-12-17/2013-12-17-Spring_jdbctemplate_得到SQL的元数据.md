#Spring jdbctemplate 得到SQL的元数据
###发表时间：2013-12-17
###分类：java,sql,经验,Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1990891" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1990891</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">	public static void testFind() {
		DataSource dataSource = getDataSource();
		JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
		String sql = "select * from (select * from qpf_data_source) where 1=0";
		List&lt;KeyValue&lt;String, String&gt;&gt; list = jdbcTemplate.query(sql,
				new ResultSetExtractor&lt;List&lt;KeyValue&lt;String, String&gt;&gt;&gt;() {

					@Override
					public List&lt;KeyValue&lt;String, String&gt;&gt; extractData(
							ResultSet rs) throws SQLException,
							DataAccessException {
						ResultSetMetaData metaData = rs.getMetaData();
						int count = metaData.getColumnCount();
						List&lt;KeyValue&lt;String, String&gt;&gt; l = new ArrayList&lt;KeyValue&lt;String, String&gt;&gt;();
						for (int i = 0; i &lt; count; i++) {
							String fieldName = metaData.getColumnName(i + 1).toLowerCase();
							int type = metaData.getColumnType(i + 1);
							String typeName = metaData.getColumnTypeName(i + 1).toLowerCase();
							System.out.println(fieldName + " : " + type + " : "
									+ typeName);
							l.add(new KeyValue&lt;String, String&gt;(fieldName,
									typeName));
						}
						return l;
					}
				});

		for (KeyValue&lt;String, String&gt; obj : list) {
			System.out.println(obj);
		}
	}</pre> 
 <p>&nbsp;输出：</p> 
 <p>&nbsp;</p> 
 <p>id : 2 : number</p> 
 <p>data_source_name : 12 : varchar2</p> 
 <p>data_source_text : 12 : varchar2</p> 
 <p>driver_class_name : 12 : varchar2</p> 
 <p>url : 12 : varchar2</p> 
 <p>user_name : 12 : varchar2</p> 
 <p>user_password : 12 : varchar2</p> 
 <p>validation_query : 12 : varchar2</p> 
 <p>create_time : 93 : date</p> 
 <p>KeyValue [key=id, value=number]</p> 
 <p>KeyValue [key=data_source_name, value=varchar2]</p> 
 <p>KeyValue [key=data_source_text, value=varchar2]</p> 
 <p>KeyValue [key=driver_class_name, value=varchar2]</p> 
 <p>KeyValue [key=url, value=varchar2]</p> 
 <p>KeyValue [key=user_name, value=varchar2]</p> 
 <p>KeyValue [key=user_password, value=varchar2]</p> 
 <p>KeyValue [key=validation_query, value=varchar2]</p> 
 <p>KeyValue [key=create_time, value=date]</p> 
</div>