#WalkFolder
###发表时间：2013-01-08
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1766126" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1766126</a>

---

<p>用于遍历文件夹里面所有的文件</p>
<p> </p>
<pre name="code" class="java">	public void walkFolder(File folder, List&lt;File&gt; files){
		File[] tempFiles = folder.listFiles();
		if(null == tempFiles){
			return;
		}else{
			for(File f : tempFiles){
				if(f.isFile()){
					files.add(f);
				}else{
					walkFolder(f, files);
				}
			}
		}
	}</pre>