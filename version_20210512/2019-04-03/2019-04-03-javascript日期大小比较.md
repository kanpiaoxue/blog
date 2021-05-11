#javascript日期大小比较
###发表时间：2019-04-03
###分类：javascript,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439728" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439728</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">&lt;script&gt;
    // Source: http://stackoverflow.com/questions/497790
    var DateUtils = {
        convert: function(d) {
            // Converts the date in d to a date-object. The input can be:
            //   a date object: returned without modification
            //  an array      : Interpreted as [year,month,day]. NOTE: month is 0-11.
            //   a number     : Interpreted as number of milliseconds
            //                  since 1 Jan 1970 (a timestamp) 
            //   a string     : Any format supported by the javascript engine, like
            //                  "YYYY/MM/DD", "MM/DD/YYYY", "Jan 31 2009" etc.
            //  an object     : Interpreted as an object with year, month and date
            //                  attributes.  **NOTE** month is 0-11.
            return (
                d.constructor === Date ? d :
                d.constructor === Array ? new Date(d[0], d[1], d[2]) :
                d.constructor === Number ? new Date(d) :
                d.constructor === String ? new Date(d) :
                typeof d === "object" ? new Date(d.year, d.month, d.date) :
                NaN
            );
        },
        compare: function(a, b) {
            // Compare two dates (could be of any type supported by the convert
            // function above) and returns:
            //  -1 : if a &lt; b
            //   0 : if a = b
            //   1 : if a &gt; b
            // NaN : if a or b is an illegal date
            // NOTE: The code inside isFinite does an assignment (=).
            return (
                isFinite(a = this.convert(a).valueOf()) &amp;&amp;
                isFinite(b = this.convert(b).valueOf()) ?
                (a &gt; b) - (a &lt; b) :
                NaN
            );
        },
        inRange: function(d, start, end) {
            // Checks if date in d is between dates in start and end.
            // Returns a boolean or NaN:
            //    true  : if d is between start and end (inclusive)
            //    false : if d is before start or after end
            //    NaN   : if one or more of the dates is illegal.
            // NOTE: The code inside isFinite does an assignment (=).
            return (
                isFinite(d = this.convert(d).valueOf()) &amp;&amp;
                isFinite(start = this.convert(start).valueOf()) &amp;&amp;
                isFinite(end = this.convert(end).valueOf()) ?
                start &lt;= d &amp;&amp; d &lt;= end :
                NaN
            );
        }
    }

    var d1 = DateUtils.convert('2018-01-01');
    console.log(d1);
    var d2 = DateUtils.convert('2018-01-02');
    console.log(d2);
    var val = DateUtils.compare('2018-01-01', '2018-01-01');
    console.log(val);
    val = DateUtils.compare('2018-01-01', '2018-01-02');
    console.log(val);
    val = DateUtils.compare('2018-11-01', '2018-01-02');
    console.log(val);
&lt;/script&gt;</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>