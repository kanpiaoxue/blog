#linux zip 和 unzip命令
###发表时间：2018-01-03
###分类：Linux,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2406525" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2406525</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"><strong>参考地址：</strong></p> 
 <p style="margin-bottom: 25px; line-height: 28px;"><a href="http://man.linuxde.net/zip"><span style="color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"><strong>http://man.linuxde.net/zip</strong></span></a></p> 
 <p style="margin-bottom: 25px; line-height: 28px;"><a href="http://man.linuxde.net/unzip"><span style="color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"><strong>http://man.linuxde.net/unzip</strong></span></a></p> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"><strong>zip命令：</strong></p> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"><strong>zip命令</strong>可以用来解压缩文件，或者对文件进行打包操作。zip是个使用广泛的压缩程序，文件经它压缩后会另外产生具有“.zip”扩展名的压缩文件。</p> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">语法</h3> 
 <pre>zip(选项)(参数)</pre> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">选项</h3> 
 <pre>-A：调整可执行的自动解压缩文件；
-b&lt;工作目录&gt;：指定暂时存放文件的目录；
-c：替每个被压缩的文件加上注释；
-d：从压缩文件内删除指定的文件；
-D：压缩文件内不建立目录名称；
-f：此参数的效果和指定“-u”参数类似，但不仅更新既有文件，如果某些文件原本不存在于压缩文件内，使用本参数会一并将其加入压缩文件中；
-F：尝试修复已损坏的压缩文件；
-g：将文件压缩后附加在已有的压缩文件之后，而非另行建立新的压缩文件；
-h：在线帮助；
-i&lt;范本样式&gt;：只压缩符合条件的文件；
-j：只保存文件名称及其内容，而不存放任何目录名称；
-J：删除压缩文件前面不必要的数据；
-k：使用MS-DOS兼容格式的文件名称；
-l：压缩文件时，把LF字符置换成LF+CR字符；
-ll：压缩文件时，把LF+<span class="wp_keywordlink"><a style="border: none;" title="cp命令" href="http://man.linuxde.net/cp" target="_blank">cp</a></span>字符置换成LF字符；
-L：显示版权信息；
-m：将文件压缩并加入压缩文件后，删除原始文件，即把文件移到压缩文件中；
-n&lt;字尾字符串&gt;：不压缩具有特定字尾字符串的文件；
-o：以压缩文件内拥有最新更改时间的文件为准，将压缩文件的更改时间设成和该文件相同；
-q：不显示指令执行过程；
-r：递归处理，将指定目录下的所有文件和子目录一并处理；
-S：包含系统和隐藏文件；
-t&lt;日期时间&gt;：把压缩文件的日期设成指定的日期；
-T：检查备份文件内的每个文件是否正确无误；
-u：更换较新的文件到压缩文件内；
-v：显示指令执行过程或显示版本信息；
-V：保存VMS操作系统的文件属性；
-<span class="wp_keywordlink"><a style="border: none;" title="w命令" href="http://man.linuxde.net/w" target="_blank">w</a></span>：在文件名称里假如版本编号，本参数仅在VMS操作系统下有效；
-x&lt;范本样式&gt;：压缩时排除符合条件的文件；
-X：不保存额外的文件属性；
-y：直接保存符号连接，而非该链接所指向的文件，本参数仅在UNIX之类的系统下有效；
-z：替压缩文件加上注释；
-$：保存第一个被压缩文件所在磁盘的卷册名称；
-&lt;压缩效率&gt;：压缩效率是一个介于1~9的数值。</pre> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">参数</h3> 
 <ul style="margin-bottom: 25px; line-height: 26px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"> 
  <li style="margin-bottom: 10px;">zip压缩包：指定要创建的zip压缩包；</li> 
  <li style="margin-bottom: 10px;">文件列表：指定要压缩的文件列表。</li> 
 </ul> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">实例</h3> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">将<code style="border: 1px solid #d4d7db; border-radius: 2px; color: #666666; margin: 0px 2px; padding: 2px 3px 1px;">/home/Blinux/html/</code>这个目录下所有文件和文件夹打包为当前目录下的html.zip：</p> 
 <pre>zip -q -r html.zip /home/Blinux/html</pre> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">上面的命令操作是将绝对地址的文件及文件夹进行压缩，以下给出压缩相对路径目录，比如目前在Bliux这个目录下，执行以下操作可以达到以上同样的效果：</p> 
 <pre>zip -q -r html.zip html</pre> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">比如现在我的html目录下，我操作的zip压缩命令是：</p> 
 <pre>zip -q -r html.zip *</pre> 
 <p><strong style="color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">unzip命令：</strong></p> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;"><strong>unzip命令</strong>用于解压缩由<span class="wp_keywordlink"><a style="border: none;" title="zip命令" href="http://man.linuxde.net/zip" target="_blank">zip</a></span>命令压缩的“.zip”压缩包。</p> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">语法</h3> 
 <pre>unzip(选项)(参数)</pre> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">选项</h3> 
 <pre>-c：将解压缩的结果显示到屏幕上，并对字符做适当的转换；
-f：更新现有的文件；
-l：显示压缩文件内所包含的文件；
-p：与-c参数类似，会将解压缩的结果显示到屏幕上，但不会执行任何的转换；
-t：检查压缩文件是否正确；
-u：与-f参数类似，但是除了更新现有的文件外，也会将压缩文件中的其他文件解压缩到目录中；
-v：执行时显示详细的信息；
-z：仅显示压缩文件的备注文字；
-a：对文本文件进行必要的字符转换；
-b：不要对文本文件进行字符转换；
-C：压缩文件中的文件名称区分大小写；
-j：不处理压缩文件中原有的目录路径；
-L：将压缩文件中的全部文件名改为小写；
-M：将输出结果送到<span class="wp_keywordlink"><a style="border: none;" title="more命令" href="http://man.linuxde.net/more" target="_blank">more</a></span>程序处理；
-n：解压缩时不要覆盖原有的文件；
-o：不必先询问用户，unzip执行后覆盖原有的文件；
-P&lt;密码&gt;：使用zip的密码选项；
-q：执行时不显示任何信息；
-s：将文件名中的空白字符转换为底线字符；
-V：保留VMS的文件版本信息；
-X：解压缩时同时回存文件原来的UID/GID；
-d&lt;目录&gt;：指定文件解压缩后所要存储的目录；
-x&lt;文件&gt;：指定不要处理.zip压缩文件中的哪些文件；
-Z：unzip-Z等于执行<span class="wp_keywordlink"><a style="border: none;" title="zipinfo命令" href="http://man.linuxde.net/zipinfo" target="_blank">zipinfo</a></span>指令。</pre> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">参数</h3> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">压缩包：指定要解压的“.zip”压缩包。</p> 
 <h3 style="margin-bottom: 25px; overflow: hidden; font-size: 16px; display: table; padding: 5px 8px; background: #2d2d2d; color: #ffffff; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">实例</h3> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">将压缩文件text.zip在当前目录下解压缩。</p> 
 <pre>unzip <span class="wp_keywordlink"><a style="border: none;" title="test命令" href="http://man.linuxde.net/test" target="_blank">test</a></span>.zip</pre> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">将压缩文件text.zip在指定目录<code style="border: 1px solid #d4d7db; border-radius: 2px; color: #666666; margin: 0px 2px; padding: 2px 3px 1px;">/tmp</code>下解压缩，如果已有相同的文件存在，要求unzip命令不覆盖原先的文件。</p> 
 <pre>unzip -n test.zip -d /tmp</pre> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">查看压缩文件目录，但不解压。</p> 
 <pre>unzip -v test.zip</pre> 
 <p style="margin-bottom: 25px; line-height: 28px; color: #444444; font-family: Verdana, Geneva, 'Helvetica Neue', 微软雅黑, 'Microsoft Yahei', Helvetica, Arial, sans-serif;">将压缩文件test.zip在指定目录<code style="border: 1px solid #d4d7db; border-radius: 2px; color: #666666; margin: 0px 2px; padding: 2px 3px 1px;">/tmp</code>下解压缩，如果已有相同的文件存在，要求unzip命令覆盖原先的文件。</p> 
 <pre>unzip -o test.zip -d tmp/</pre> 
</div>