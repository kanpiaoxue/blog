#javascript数组partition的分隔功能
###发表时间：2018-06-27
###分类：javascript,经验,array
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2425742" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2425742</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="text-align: left;">在JavaScript中会遇到想将大的数组切割为小数组的情况。</p> 
 <p style="text-align: left;">&nbsp;</p> 
 <pre name="code" class="html">function partition(arr, length) {
    var result = [];
    for (var i = 0, j = arr.length; i &lt; j; i++) {
        if (i % length === 0){
            result.push([]);
        }
        result[result.length - 1].push(arr[i]);
    }
    return result;
};


var arr = [];
for(var i = 0; i&lt;100;i++){
    arr.push(i);
}


console.log('length:7',partition(arr,7));
/*
0:(7) [0, 1, 2, 3, 4, 5, 6]
1:(7) [7, 8, 9, 10, 11, 12, 13]
2:(7) [14, 15, 16, 17, 18, 19, 20]
3:(7) [21, 22, 23, 24, 25, 26, 27]
4:(7) [28, 29, 30, 31, 32, 33, 34]
5:(7) [35, 36, 37, 38, 39, 40, 41]
6:(7) [42, 43, 44, 45, 46, 47, 48]
7:(7) [49, 50, 51, 52, 53, 54, 55]
8:(7) [56, 57, 58, 59, 60, 61, 62]
9:(7) [63, 64, 65, 66, 67, 68, 69]
10:(7) [70, 71, 72, 73, 74, 75, 76]
11:(7) [77, 78, 79, 80, 81, 82, 83]
12:(7) [84, 85, 86, 87, 88, 89, 90]
13:(7) [91, 92, 93, 94, 95, 96, 97]
14:(2) [98, 99]
*/

console.log('length:7',partition(arr,11));
/*
0:(11) [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
1:(11) [11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21]
2:(11) [22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32]
3:(11) [33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43]
4:(11) [44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54]
5:(11) [55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65]
6:(11) [66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76]
7:(11) [77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87]
8:(11) [88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98]
9:[99]
*/
</pre> 
 <p style="text-align: left;">&nbsp;</p> 
 <p style="text-align: left;">&nbsp;</p> 
</div>