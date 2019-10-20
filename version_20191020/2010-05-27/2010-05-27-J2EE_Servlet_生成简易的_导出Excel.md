#J2EE Servlet 生成简易的 导出Excel
###发表时间：2010-05-27
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/677022" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/677022</a>

---

<pre name="code" class="java">	public void dayToDayExportExcel(String beginDate, String endDate,
			Integer gameId, String arr,HttpServletResponse response) {
		try {

			String[] paramsArr = arr.split(",");
			/**
			 * 计算数据
			 */
			StringBuilder builder = new StringBuilder();
			builder.append(" select * from game_kpi_day w where w.game_id =");
			builder.append(gameId);
			builder.append(" and w.log_date between to_date('");
			builder.append(beginDate);
			builder.append("','yyyy-mm-dd') and to_date('");
			builder.append(endDate);
			builder.append("','yyyy-mm-dd')  order by w.log_date asc  ");

			//System.out.println(builder.toString());
			
			String filename = beginDate + "-" + endDate + ".xls";
			filename = new String(filename.getBytes("GBK"),"ISO8859-1");

			response.setContentType("application/vnd.ms-excel");
			response.setHeader("Content-Disposition", "attachment;filename="
					+ filename);
			PrintWriter out = response.getWriter();
			
			//生成表头
			StringBuilder titleBuilder = new StringBuilder();
			titleBuilder.append(this.encode("统计区间"));
			titleBuilder.append("\t");
			for(String s : paramsArr){
				titleBuilder.append(this.encode(CommonXMLStr.mutiTargetAimMap.get(s.trim())));
				titleBuilder.append("\t");
			}
			out.println(titleBuilder.toString());
			
			//生成表格数据
			List list = jdbcTemplate.queryForList(builder.toString());
			StringBuilder tableBuilder = new StringBuilder();
			if (null != list) {
				for (int i = 0, j = list.size(); i &lt; j; i++) {
					
					Map map = (Map) list.get(i);
					String logDate = map.get("LOG_DATE").toString().substring(0, 10);
					tableBuilder.append(this.encode(logDate));
					tableBuilder.append("\t");
					for (int m = 0; m &lt; paramsArr.length; m++) {
						String value = nvl(map.get(paramsArr[m])).toString();
						tableBuilder.append(this.encode(value));
						tableBuilder.append("\t");
					}

					tableBuilder.append("\n");
				}
			}
			out.println(tableBuilder.toString());

			out.flush();
			out.close();
		} catch (Exception e) {
			logger.error("method: getMutiTargetAim error! ", e);
		}
		
	}</pre>
<p>&nbsp;</p>