#启动和停止springboot程序的shell
###发表时间：2019-02-22
###分类：Spring,springboot,java,shell,Linux,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2437954" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2437954</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>启动脚本：</p> 
 <pre name="code" class="java">#! /bin/bash

# example: sh start.sh -Dspring.profiles.active=dev
program_name=helloWorld
JAVA_OPTS="-Duser.timezone=GMT+8 -server -Xms2048m -Xmx2048m -Dspring.profiles.active=test"
JAVA_OPTS="$JAVA_OPTS $@"

nohup $JAVA_HOME/bin/java $JAVA_OPTS -jar helloWorld-0.0.1.jar &gt;/dev/null 2&gt;&amp;1 &amp;
pid=$!
exit_code=$?
echo $pid &gt; PID

echo "pid: $pid"

if [ $exit_code -eq 0 ];
then
    echo "execute $program_name successfully!"
else
    echo "execute $program_name failed!"
fi</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>停止脚本：</p> 
 <pre name="code" class="java">#! /bin/bash
program_name=helloWorld
pid=`cat PID`
echo "start to kill pid:$pid" 
kill $pid
if [ $? -eq 0 ];
then
    echo "shutdown $program_name successfully!"
else
    echo "shutdown $program_name failed!"
fi</pre> 
 <p>&nbsp;</p> 
</div>