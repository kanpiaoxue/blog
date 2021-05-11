#SpringMVC中创建新线程引起的Null错误
###发表时间：2013-11-18
###分类：经验,Spring,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1976469" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1976469</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;">今天在一个现有的SpringMVC的Web程序中添加新功能，引起了NullPoint的错误。看了代码，找到了错误的发生点，怎么看，代码都是正确的。不知道为啥？</p> 
 <p style="font-size: 14px;">起因是这样的：</p> 
 <p style="font-size: 14px;">我在SpringMVC中添加到了controller，然后写了service类。里面涉及了同事的dao类。在service类中的一个查询方法中，调用了2个dao中的查询数据的方法。因为数据量大，为了加快程序的运行速度，提高程序的运行效率，我在servcie的这个查询方法中对这个2个dao的查询分别写了Callable 接口的并行查询操作。写好之后，发现了上面说的空指针的错误。当我把它们修改为线性的单线程查询的时候（一个查询方法执行完毕，再去执行另一个查询方法），发现没有空指针的错误。百思不得其解。我查看了同事的dao类，发现这个null的空指针错误就是代码里面调用了spring security的一个用户权限检查的方法引起的。我又再次尝试单线程调用，是没有问题，采用多线程调用就有问题。（我在servcie类里面用ExecutorService exec = Executors.newCachedThreadPool(); 生成的新的线程池）。想了想，明白了。同事的dao类，调用spring security的权限检查，里面的spring应该是把当前运行的线程（tomcat产生的线程） 和一个用户的权限绑定了在一起，采用ThreadLocal。我利用自己的线程，造成ThreadLocal找不到新线程的用户组绑定内容，出现了空指针。</p> 
 <p style="font-size: 14px;">解决方案：</p> 
 <p style="font-size: 14px;">&nbsp; &nbsp; 我调用同事的dao类的2个查询方法，一个涉及到spring security，一个没有涉及到spring security。我把没有涉及到spring&nbsp;<span style="font-size: 12px; line-height: 1.5;">security的查询方法放在自己创建的线程池中调用，涉及到</span><span style="font-size: 12px; line-height: 1.5;">security的方法，保留在原有线程中（tomcat生成的线程），这样，即取到了并发查询的效果，也没有干涉到spring&nbsp;</span><span style="font-size: 12px; line-height: 1.5;">security 的本地线程变量绑定。</span></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;"><span style="font-size: 12px; line-height: 1.5;">思考：使用spring的时候，需要注意，尤其多线程的情况下，改变了当前线程环境的情况下，需要考虑spring的线程环境是否发生了改变。</span></p> 
 <p><span style="font-size: 12px; line-height: 18px;">修改后的代码：</span></p> 
 <pre name="code" class="java">	public String initQueryCondition(final Integer gameId) {
		try {
			Map&lt;String, Object&gt; dataMap = new HashMap&lt;String, Object&gt;();

			// 开始并行查询
			ExecutorService exec = Executors.newCachedThreadPool();
			Future&lt;List&lt;GameServerBean&gt;&gt; f1 = exec
					.submit(new Callable&lt;List&lt;GameServerBean&gt;&gt;() {

						@Override
						public List&lt;GameServerBean&gt; call() throws Exception {
							return gameServerDao.selectAll(gameId);
						}
					});
			exec.shutdown();
			/**
			 * 
			 * 这里没有用并行查询，因为这个查询里面涉及了ThreadLocal（由spring的security使用），
			 * 启动新的线程会造成线程环境改变，发生null的错误
			 */
			List&lt;GameProviderBean&gt; providerList = gameProviderDao
					.selectAll(gameId);

			List&lt;GameServerBean&gt; serverList = f1.get();

			dataMap.put("serverLsit", serverList);
			dataMap.put("providerList", providerList);
			return createJson(dataMap);
		} catch (Exception e) {
			LOGGER.error("Error:" + e.getMessage(), e);
		}
		return null;

	}</pre> 
 <p><span style="font-size: 12px; line-height: 18px;">&nbsp;</span></p> 
</div>