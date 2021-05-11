#javascript克隆clone
###发表时间：2018-02-06
###分类：javascript,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2410364" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2410364</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>参考地址：<a href="https://www.cnblogs.com/zouhao/p/7278117.html">https://www.cnblogs.com/zouhao/p/7278117.html</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">function clone(obj) {
    // Handle the 3 simple types, and null or undefined
    if (null == obj || 'object' != typeof obj) {
        return obj
    };

    // Handle Date
    if (obj instanceof Date) {
        var copy = new Date();
        copy.setTime(obj.getTime());
        return copy;
    }

    // Handle Array
    if (obj instanceof Array) {
        var copy = [];
        for (var i = 0, len = obj.length; i &lt; len; i++) {
            copy[i] = clone(obj[i]);
        }
        return copy;
    }

    // Handle Object
    if (obj instanceof Object) {
        var copy = {};
        for (var attr in obj) {
            if (obj.hasOwnProperty(attr)){
                copy[attr] = clone(obj[attr]);
            }
        }
        return copy;
    }

    throw new Error('Unable to copy obj! Its type isn\'t supported.');
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>