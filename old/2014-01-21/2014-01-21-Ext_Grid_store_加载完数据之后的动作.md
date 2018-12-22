#Ext Grid store 加载完数据之后的动作
###发表时间：2014-01-21
###分类：javascript,Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2007869" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2007869</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>有的时候我们需要明确的知道Ext中Grid的store加载完数据的那一刻。需要在加载完的这一刻来触发一些动作。</p> 
 <p>Ext提供了该动作的回调方法。</p> 
 <p>下面的这段描述摘自Ext3.1的文档描述：</p> 
 <pre name="code" class="js">load( Object options ) : Boolean 
采用配置好的Reader格式去加载Record缓存，具体请求的任务由配... 
采用配置好的Reader格式去加载Record缓存，具体请求的任务由配置好的Proxy对象完成。Loads the Record cache from the configured Proxy using the configured Reader. 
如果使用服务器分页，那么必须指定在options.params中start和limit两个参数。start参数表明了从记录集（dataset）的哪一个位置开始读取，limit是读取多少笔的记录。Proxy负责送出参数。If using remote paging, then the first load call must specify the start and limit properties in the options.params property to establish the initial position within the dataset, and the number of Records to cache on each read from the Proxy.

由于采用了异步加载，因此该方法执行完毕后，数据不是按照load()方法下一个语句的顺序可以获取得到的。应该登记一个回调函数，或者“load”的事件，登记一个处理函数。It is important to note that for remote data sources, loading is asynchronous, and this call will return before the new data has been loaded. Perform any post-processing in a callback function, or in a "load" event handler.

	参数项： 
		options : Object 
			传入以下属性的对象，传入的对象会影响加载的选项：An object containing properties which control loading options: 
			params :Object 
			送出的HTTP参数，格式是JS对象。An object containing properties to pass as HTTP parameters to a remote data source.
			
			callback : Function 
			回调函数，这个函数会有以下的参数传入：A function to be called after the Records have been loaded. The callback is passed the following arguments: 
			
			r : Ext.data.Record[] 
			options: 加载的配置项对象。Options object from the load call 
			success: 是否成功。Boolean success indicator
			
			scope : Object 
			回调函数的作用域（默认为Store对象）。Scope with which to call the callback (defaults to the Store object)
			
			add : Boolean 
			表示到底是追加数据，还是替换数据。Indicator to append loaded records rather than replace the current cache.
	
	返回值： 
		Boolean 
		是否执行了load（受beforeload的影响，参见源码）。Whether the load fired (if beforeload failed). </pre> 
 <p>&nbsp;这里可以看见，在store的load()方法里面，提供了一个&nbsp;callback 的回调函数。</p> 
 <p>下面是个例子：</p> 
 <pre name="code" class="js">	var store = new Ext.data.JsonStore({
		root : 'root',
		totalProperty : 'totalProperty',
		fields : fields,
		proxy : new Ext.data.HttpProxy({
			url : basePath + 'web/dataQuery/getSQLGridDatas'
		})
	});
store.baseParams.start = 0;
store.baseParams.limit = pageSize;
store.load({
		callback : function(record, options, success) {
		
		}
});</pre> 
 <p>&nbsp;</p> 
</div>