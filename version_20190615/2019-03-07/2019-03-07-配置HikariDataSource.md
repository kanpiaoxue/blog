#配置HikariDataSource
###发表时间：2019-03-07
###分类：Spring,java,DataSource,jdbc
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2438546" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2438546</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    public DataSource dataSource() {
        HikariConfig jdbcConfig = new HikariConfig();
        jdbcConfig.setPoolName(getClass().getName());
        jdbcConfig.setDriverClassName(driverClassName);
        jdbcConfig.setJdbcUrl(url);
        jdbcConfig.setUsername(username);
        jdbcConfig.setPassword(password);
        jdbcConfig.setMaximumPoolSize(maximumPoolSize);
        jdbcConfig.setMaxLifetime(maxLifetime);
        jdbcConfig.setConnectionTimeout(connectionTimeout);
        jdbcConfig.setIdleTimeout(idleTimeout);

        return new HikariDataSource(jdbcConfig);
    }</pre> 
 <p>&nbsp;</p> 
</div>