#javascript的base64操作
###发表时间：2018-04-08
###分类：javascript,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2415953" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2415953</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>有的时候我们也会遇到在js里面进行base64的操作。</p> 
 <pre name="code" class="js">function b64EncodeUnicode(str) {
    // first we use encodeURIComponent to get percent-encoded UTF-8,
    // then we convert the percent encodings into raw bytes which
    // can be fed into btoa.
    return btoa(encodeURIComponent(str).replace(/%([0-9A-F]{2})/g,
        function toSolidBytes(match, p1) {
            return String.fromCharCode('0x' + p1);
    }));
}


function b64DecodeUnicode(str) {
    // Going backwards: from bytestream, to percent-encoding, to original string.
    return decodeURIComponent(atob(str).split('').map(function(c) {
        return '%' + ('00' + c.charCodeAt(0).toString(16)).slice(-2);
    }).join(''));
}</pre> 
 <p>&nbsp;测试</p> 
 <pre name="code" class="js">var hello = '/usr/local/test/hello.txt';
console.log('original:%s',hello);
var b64EncodeUnicodeStr = b64EncodeUnicode(hello);
console.log('b64EncodeUnicode:%s',b64EncodeUnicodeStr);
console.log('b64DecodeUnicode:%s',b64DecodeUnicode(b64EncodeUnicodeStr));

// output:
// original:/usr/local/test/hello.txt
// untitled.html:50 b64EncodeUnicode:L3Vzci9sb2NhbC90ZXN0L2hlbGxvLnR4dA==
// untitled.html:51 b64DecodeUnicode:/usr/local/test/hello.txt</pre> 
 <p>&nbsp;</p> 
</div>