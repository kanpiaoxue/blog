#Eclipse 更改为 Courier New字体
###发表时间：2011-12-23
###分类：java,eclipse
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1323506" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1323506</a>

---

<p><span style="font-family: Helvetica, Tahoma, Arial, sans-serif; font-size: 14px; line-height: 25px;"> </span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">Eclipse以前的默认字体一般是Courier New字体，这种字体看着习惯。但新版Eclipse安装后改变了字体，并且在字体设置的地方没有Courier New字体。</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">&nbsp;</span></p>
<p style="padding-top: 0px; padding-right: 0px; padding-bottom: 0px; padding-left: 30px; margin: 0px;"><span style="font-size: small;">解决办法如下：</span></p>
<p style="padding-top: 0px; padding-right: 0px; padding-bottom: 0px; padding-left: 30px; margin: 0px;"><span style="font-size: small;">&nbsp;</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">1、 找到jFace并用WinRAR打开之：</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; jFace的具体位置：$Eclipse目录$/plugins/org.eclipse.jface_3.7.0.I20110522-1430.jar，找到后，用WinRAR打开。</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">&nbsp;</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">2、 找到并修改字体属性：<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 打开后，依次展开：/org/eclipse/jface/resources，这里，你将看到不同操作系统的字体设置，比如jfacefonts_hp_ux,properties里保存了HP-UX系统的字体设置，jfacefonts_macosx.properties则保存了Mac X的字体设置。找到Windows 7/Vista的字体设置，双击，随便用一个文本编译器打开，找到org.eclipse.jface.textfont.0的配置项，将其设置成Courier New-regular即可，后面还可以设置字号。修改完成后，保存，WinRAR自动更新jar包。</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">&nbsp;</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">3、 启动Eclipse Indigo，如果你没有修改过字体，将看到字体已经改过来了，但如果你修改了，则Reset一下，字体就会改过来了。</span></p>
<p style="padding: 0px; margin: 0px;"><span style="font-size: small;">&nbsp;</span></p>
<p style="padding: 0px; margin: 0px;"><span><span style="font-size: small;"><strong style="font-weight: bold;">注意：</strong>&nbsp;如果字体没有改变过来，可能是因为Eclipse已经运行过，此时以命令行的方式启动eclipse，启动时加参数 -clean</span></span></p>
<p style="padding: 0px; margin: 0px;">&nbsp;</p>
<p style="padding: 0px; margin: 0px;">------- 引自：&nbsp;<span style="font-family: Verdana, Arial, Helvetica, sans-serif; font-size: 12px; line-height: normal;"><a href="http://wmljava.iteye.com/blog/1158575">http://wmljava.iteye.com/blog/1158575</a></span></p>
<p></p>