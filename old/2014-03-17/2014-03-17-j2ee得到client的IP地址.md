#j2ee得到client的IP地址
###发表时间：2014-03-17
###分类：java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2032027" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2032027</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">	public static String getIp(HttpServletRequest req) {
		try {
			if (req == null) {
				return null;
			}
			String ip_for = req.getHeader(" x-forwarded-for ");
			String ip_client = req.getHeader(" http_client_ip ");
			String un = " unknown ";

			if (ip_for != null &amp;&amp; !ip_for.equalsIgnoreCase(un)
					&amp;&amp; ip_for.trim().length() &gt; 0) {
				return ip_for;
			} else if (ip_client != null &amp;&amp; !ip_client.equalsIgnoreCase(un)
					&amp;&amp; ip_client.trim().length() &gt; 0) {
				return ip_client;
			} else {
				return req.getRemoteAddr();
			}
		} catch (Exception e) {
			LOGGER.error("Error: get ip failure : " + e.getMessage());
		}
		return null;
	}</pre> 
 <p>&nbsp;</p> 
</div>