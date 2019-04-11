#Jointjs 在Chrome浏览器升级到v.48版本之后报错Uncaught TypeError: this.node.getTransformToEleme
###发表时间：2016-02-25
###分类：javascript,jointjs
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2278719" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2278719</a>

---

<div class="iteye-blog-content-contain"> 
 <p style="font-size: 14px;">[现象]</p> 
 <p style="font-size: 14px;">近期发现使用Chrome（版本v.48)浏览器访问dmap.xxx.com的时候发现异常情况，表现为图形界面报错，不能正常使用。</p> 
 <p style="font-size: 14px;">Chrome的报错信息如下：</p> 
 <p style="font-size: 14px;">Uncaught TypeError: this.node.getTransformToElement is not a function</p> 
 <p style="font-size: 14px;">[原因]</p> 
 <p style="font-size: 14px;">经过CDC RD同学的定位，发现Chrome v.48的版本进行大幅度的更新。其中一条更新内容如下：</p> 
 <p style="font-size: 14px;">原文如下：SVGGraphicsElement.getTransformToElement has been removed to match the SVG spec.</p> 
 <p style="font-size: 14px;">译文如下：移除了 SVGGraphicsElement.getTransformToElement，以符合 SVG 规范。</p> 
 <p style="font-size: 14px;">地址如下：http://blog.chromium.org/2015/12/chrome-48-beta-present-to-cast-devices_91.html</p> 
 <p style="font-size: 14px;">dmap.xxx.com依赖的开源SVG框架jointjs依赖于该方法的实现，所以引起程序异常，无法查看图形功能模块。</p> 
 <p style="font-size: 14px;">[临时解决方案]</p> 
 <p style="font-size: 14px;">方法1：请大家使用Chrome v.47或更低的版本来访问dmap.xxx.com</p> 
 <p style="font-size: 14px;">方法2：请大家使用百度浏览器来访问dmap.xxx.com</p> 
 <p style="font-size: 14px;">[终极解决方案]</p> 
 <p style="font-size: 14px;">会对jointjs框架进行升级，支持Chrome浏览器全部版本。</p> 
 <p style="font-size: 14px;">[终极解决方案时间]</p> 
 <p style="font-size: 14px;">近期对该问题进行修复，进度会在HI群中进行及时更新通知。</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">官网解决问题： http://jointjs.com/blog/get-transform-to-element-polyfill.html</p> 
 <p style="font-size: 14px;">谢谢！</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p>=========== [ http://jointjs.com/blog/get-transform-to-element-polyfill.html ] ====================&nbsp;</p> 
 <p>Announcement: getTransformToElement() polyfill Nov 12th, 2015</p> 
 <p>&nbsp;</p> 
 <p>Unfortunately, a new version of Chrome (48) removes a feature that is core to JointJS/Rappid. This feature is theSVGGraphicsElement.getTransformToElement() function. The motivation behind removing the method is - according to the Chrome team - open issues about how this method is supposed to behave.</p> 
 <p>To overcome compatibility issues with future versions of Chrome, we prepared a polyfill that makes sure this method exists. Before a new version of JointJS/Rappid is released (or if you, for any reason, don't want to upgrade), include the following code before you load your application JavaScript:</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">SVGElement.prototype.getTransformToElement = SVGElement.prototype.getTransformToElement || function(toElement) {
    return toElement.getScreenCTM().inverse().multiply(this.getScreenCTM());
};</pre> 
 <p>David Durman</p> 
 <p>===========================================================</p> 
</div>