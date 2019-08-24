#使用Spring的JdbcTemplate调用Oracle的存储过程
###发表时间：2011-12-14
###分类：Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1311020" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1311020</a>

---

<p style="text-align: left;"><span><span style="font-size: 14px; line-height: 25px;"> </span></span></p>
<p>Spring的SimpleJdbcTemplate将存储过程的调用进行了良好的封装，但可惜只能用于jdk1.5的环境，无法再jdk1.4环境下使用，而JdbcTemplate则完全适用于jdk1.4下的环境，下面列出使用JdbcTemplate调用Oracle存储过程的一些方法：</p>
<p>一) 无返回值的存储过程调用</p>
<p>存储过程： &nbsp;</p>
<p>CREATE OR REPLACE PROCEDURE TESTPRO(PARAM1 IN VARCHAR2,PARAM2 IN VARCHAR2) AS</p>
<p>BEGIN</p>
<p>&nbsp; &nbsp; INSERT INTO TESTTABLE (ID,NAME) VALUES (PARAM1, PARAM2);</p>
<p>END TESTPRO;</p>
<p>&nbsp;</p>
<p>Java代码： &nbsp;&nbsp;</p>
<p>package com.dragon.test;</p>
<p>import org.springframework.jdbc.core.JdbcTemplate;</p>
<p>public class JdbcTemplateTest {</p>
<p>&nbsp; &nbsp; private JdbcTemplate jdbcTemplate;</p>
<p>&nbsp; &nbsp; public void setJdbcTemplate(JdbcTemplate jdbcTemplate) {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; this.jdbcTemplate = jdbcTemplate;</p>
<p>&nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; public void test(){</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; this.jdbcTemplate.execute("call testpro('p1','p2')");</p>
<p>&nbsp; &nbsp; }</p>
<p>}</p>
<p>注:存储过程TESTPRO中用到了表TESTTABLE(ID, NAME),需事先建好.</p>
<p>&nbsp;</p>
<p>二)有返回值的存储过程（非结果集） &nbsp;&nbsp;</p>
<p>存储过程： &nbsp;&nbsp;</p>
<p>CREATE OR REPLACE PROCEDURE TESTPRO(PARAM1 IN VARCHAR2,PARAM2 OUT VARCHAR2) AS &nbsp;&nbsp;</p>
<p>BEGIN &nbsp; &nbsp;</p>
<p>&nbsp; &nbsp; SELECT INTO PARAM2 FROM TESTTABLE WHERE ID= PARAM1; &nbsp; &nbsp;</p>
<p>END TESTPRO;</p>
<p>&nbsp;</p>
<p>Java代码：</p>
<p>public void test() {</p>
<p>&nbsp; &nbsp; String param2Value = (String) jdbcTemplate.execute(</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; new CallableStatementCreator() {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; public CallableStatement createCallableStatement(Connection con) throws SQLException {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; String storedProc = "{call testpro(?,?)}";// 调用的sql</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; CallableStatement cs = con.prepareCall(storedProc);</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cs.setString(1, "p1");// 设置输入参数的值</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cs.registerOutParameter(2, OracleTypes.VARCHAR);// 注册输出参数的类型</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return cs;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; }, new CallableStatementCallback() {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; public Object doInCallableStatement(CallableStatement cs) throws SQLException, DataAccessException {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cs.execute();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return cs.getString(2);// 获取输出参数的值</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; });</p>
<p>}</p>
<p>注：cs.getString(2)中的数值2是存储过程中的out列对应的索引值(第一个参数索引为1,如此类推)&nbsp;</p>
<p>&nbsp;</p>
<p>三)有返回值的存储过程（结果集） &nbsp; &nbsp;&nbsp;</p>
<p>因oracle存储过程所有返回值都是通过out参数返回的,列表同样也不例外,但由于是集合,所以不能用一般的参数,必须要用pagkage,分两部分: &nbsp;&nbsp;</p>
<p>1.建一个程序包,如下：</p>
<p>CREATE OR REPLACE PACKAGE TESTPACKAGE AS</p>
<p>&nbsp; &nbsp; TYPE TEST_CURSOR IS REF CURSOR;</p>
<p>END TESTPACKAGE;</p>
<p>2.建立存储过程,如下：</p>
<p>CREATE OR REPLACE PROCEDURE TESTPRO(PARAM1 IN VARCHAR2,test_cursor out TESTPACKAGE.TEST_CURSOR) IS</p>
<p>BEGIN</p>
<p>&nbsp; &nbsp; &nbsp;OPEN test_cursor FOR SELECT * FROM TESTTABLE;</p>
<p>END TESTPRO;</p>
<p>可以看到，列表是通过把游标作为一个out参数来返回的。 &nbsp;&nbsp;</p>
<p>&nbsp;</p>
<p>Java代码：</p>
<p>public void test() {</p>
<p>&nbsp; &nbsp; List resultList = (List) jdbcTemplate.execute(</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; new CallableStatementCreator() {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; public CallableStatement createCallableStatement(Connection con) throws SQLException {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; String storedProc = "{call testpro(?,?)}";// 调用的sql</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; CallableStatement cs = con.prepareCall(storedProc);</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cs.setString(1, "p1");// 设置输入参数的值</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cs.registerOutParameter(2, OracleTypes.CURSOR);// 注册输出参数的类型</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return cs;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; }, new CallableStatementCallback() {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; public Object doInCallableStatement(CallableStatement cs) throws SQLException,DataAccessException {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; List resultsMap = new ArrayList();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; cs.execute();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ResultSet rs = (ResultSet) cs.getObject(2);// 获取游标一行的值</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; while (rs.next()) {// 转换每行的返回值到Map中</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Map rowMap = new HashMap();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; rowMap.put("id", rs.getString("id"));</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; rowMap.put("name", rs.getString("name"));</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; resultsMap.add(rowMap);</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; rs.close();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; return resultsMap;</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; }</p>
<p>&nbsp; &nbsp; });</p>
<p>&nbsp; &nbsp; for (int i = 0; i &lt; resultList.size(); i++) {</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; Map rowMap = (Map) resultList.get(i);</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; String id = rowMap.get("id").toString();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; String name = rowMap.get("name").toString();</p>
<p>&nbsp; &nbsp; &nbsp; &nbsp; System.out.println("id=" + id + ";name=" + name);</p>
<p>&nbsp; &nbsp; }</p>
<p>}</p>
<p>&nbsp;</p>
<p>//----------- &nbsp;备注：引用自：&nbsp;<a style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: normal;" href="http://rongjih.blog.163.com/blog/static/335744612010313019317/">http://rongjih.blog.163.com/blog/static/335744612010313019317/</a></p>
<p>--&nbsp;<a href="http://hi.baidu.com/air6355/blog/item/6874fe1c408f886ef624e4ae.html">http://hi.baidu.com/air6355/blog/item/6874fe1c408f886ef624e4ae.html</a></p>
<p>&nbsp;</p>