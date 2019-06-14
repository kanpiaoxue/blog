#Hibernate + MySQL 分页类的实现
###发表时间：2010-04-13
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/642985" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/642985</a>

---

<p><span style="color: #0000ff;">Hibernate 的hql不提供语句内部使用 limit 0, 2 。<br>&nbsp;&nbsp; 分页必须按照如下处理： （下面是Spring的 getHibernateTemplate() 的方法）</span></p>
<pre name="code" class="java">		 /**
		  * 使用 hql 语句进行操作
		  * @param hql HSQL 查询语句
		  * @param start 开始取数据的下标
		  * @param limit 读取数据记录数
		  * @return List 结果集
		  * 
		  */
		 public List getListForPage(final String hql, final int start, final int limit){
		 		List list = getHibernateTemplate().executeFind(new HibernateCallback(){
		 			public Object doInHibernate(Session session) throws HibernateException,SQLException {
		 					Query query = session.createQuery(hql);
		 					query.setFirstResult(start);
		 					query.setMaxResults(limit);
		 					List list = query.list();
		 					return list;
		 			}
		 		});
		 		return list;
		 }</pre>
<p>&nbsp;</p>