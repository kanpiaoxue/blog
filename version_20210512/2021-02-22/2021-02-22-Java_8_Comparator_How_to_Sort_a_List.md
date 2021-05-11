#Java 8 Comparator: How to Sort a List
###发表时间：2021-02-22
###分类：经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519252" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519252</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>文章地址：&nbsp;<a href="https://dzone.com/articles/java-8-comparator-how-to-sort-a-list">https://dzone.com/articles/java-8-comparator-how-to-sort-a-list</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In this article,&nbsp;we’re going to see several examples on how to sort a List in Java 8.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Sort a List of Strings Alphabetically</h2> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 397.078px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">List</span><span class="cm-operator" style="">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator" style="">&gt;</span> <span class="cm-variable" style="">cities</span> <span class="cm-operator" style="">=</span> <span class="cm-variable" style="">Arrays</span>.<span class="cm-variable" style="">asList</span>(</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">       <span class="cm-string" style="color: #aa1111;">"Milan"</span>,</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">       <span class="cm-string" style="color: #aa1111;">"london"</span>,</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">       <span class="cm-string" style="color: #aa1111;">"San Francisco"</span>,</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">       <span class="cm-string" style="color: #aa1111;">"Tokyo"</span>,</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">       <span class="cm-string" style="color: #aa1111;">"New Delhi"</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">println</span>(<span class="cm-variable" style="">cities</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">//[Milan, london, San Francisco, Tokyo, New Delhi]</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">cities</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-type" style="color: #008855;">String</span>.<span class="cm-variable" style="">CASE_INSENSITIVE_ORDER</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">println</span>(<span class="cm-variable" style="">cities</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">//[london, Milan, New Delhi, San Francisco, Tokyo]</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            14
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            15
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">cities</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">naturalOrder</span>());</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            16
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">println</span>(<span class="cm-variable" style="">cities</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            17
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-comment" style="color: #aa5500;">//[Milan, New Delhi, San Francisco, Tokyo, london]</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 344px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We’ve written London with a lowercase "L" to better highlight differences between&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#naturalOrder--" target="_blank">Comparator.naturalOrder()</a>, which&nbsp;returns a&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html" target="_blank">Comparator</a>&nbsp;that sorts&nbsp;by placing capital letters first, and&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="http://docs.oracle.com/javase/8/docs/api/java/lang/String.html#CASE_INSENSITIVE_ORDER" rel="nofollow" target="_blank">String.CASE_INSENSITIVE_ORDER</a>, which returns a case-insensitive Comparator.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Basically, in Java 7, we were using Collections.sort() that was accepting a List and, eventually, a Comparator – &nbsp;in Java 8 we have&nbsp;the new&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="http://docs.oracle.com/javase/8/docs/api/java/util/List.html#sort-java.util.Comparator-" target="_blank">List.sort()</a>, which accepts&nbsp;a Comparator.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Sort a List of Integers</h2> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 420.672px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">List</span><span class="cm-operator" style="">&lt;</span><span class="cm-type" style="color: #008855;">Integer</span><span class="cm-operator" style="">&gt;</span> <span class="cm-variable" style="">numbers</span> <span class="cm-operator" style="">=</span> <span class="cm-variable" style="">Arrays</span>.<span class="cm-variable" style="">asList</span>(<span class="cm-number" style="color: #116644;">6</span>, <span class="cm-number" style="color: #116644;">2</span>, <span class="cm-number" style="color: #116644;">1</span>, <span class="cm-number" style="color: #116644;">4</span>, <span class="cm-number" style="color: #116644;">9</span>);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">println</span>(<span class="cm-variable" style="">numbers</span>); <span class="cm-comment" style="color: #aa5500;">//[6, 2, 1, 4, 9]</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">numbers</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">naturalOrder</span>());</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>.<span class="cm-variable" style="">println</span>(<span class="cm-variable" style="">numbers</span>); <span class="cm-comment" style="color: #aa5500;">//[1, 2, 4, 6, 9]</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 128px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Sort a List by String Field</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Let’s suppose we have our Movie class and we want to sort our List&nbsp;by title.&nbsp;We can use&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#comparing-java.util.function.Function-" rel="nofollow" target="_blank">Comparator.comparing()</a>&nbsp;and pass a function that extracts the field to use&nbsp;for sorting&nbsp;– title, in this example.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 404.969px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">List</span><span class="cm-operator" style="">&lt;</span><span class="cm-variable" style="">Movie</span><span class="cm-operator" style="">&gt;</span> <span class="cm-variable" style="">movies</span> <span class="cm-operator" style="">=</span> <span class="cm-variable" style="">Arrays</span>.<span class="cm-variable" style="">asList</span>(</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Lord of the rings"</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Back to the future"</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Carlito's way"</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Pulp fiction"</span>));</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">comparing</span>(<span class="cm-variable" style="">Movie</span>::<span class="cm-variable" style="">getTitle</span>));</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">forEach</span>(<span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>::<span class="cm-variable" style="">println</span>);</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 200px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The output will be:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 264.453px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{title='Back to the future'}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{title='Carlito's way'}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{title='Lord of the rings'}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{title='Pulp fiction'}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 110px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As you’ve probably noticed, we haven’t passed a Comparator, but the&nbsp;List is correctly sorted. That’s because title, the extracted field, is a String, and a String implements a&nbsp;Comparable interface. If you peek at the&nbsp;Comparator.comparing() implementation, you will see that it calls&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">compareTo</code>&nbsp;on the extracted key.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 654.688px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">return</span> (<span class="cm-variable" style="">Comparator</span><span class="cm-operator" style="">&lt;</span><span class="cm-variable" style="">T</span><span class="cm-operator" style="">&gt;</span> <span class="cm-operator" style="">&amp;</span> <span class="cm-variable" style="">Serializable</span>)</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">            (<span class="cm-variable" style="">c1</span>, <span class="cm-variable" style="">c2</span>) <span class="cm-operator" style="">-&gt;</span> <span class="cm-variable" style="">keyExtractor</span>.<span class="cm-variable" style="">apply</span>(<span class="cm-variable" style="">c1</span>).<span class="cm-variable" style="">compareTo</span>(<span class="cm-variable" style="">keyExtractor</span>.<span class="cm-variable" style="">apply</span>(<span class="cm-variable" style="">c2</span>));  </span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 74px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Sort a List by Double&nbsp;Field</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In a similar way, we can use&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#comparingDouble-java.util.function.ToDoubleFunction-" target="_blank">Comparator.comparingDouble()</a>&nbsp;for comparing double value. In the example, we want to order our List of movies by rating, from the highest to the lowest.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 443.984px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">List</span><span class="cm-operator" style="">&lt;</span><span class="cm-variable" style="">Movie</span><span class="cm-operator" style="">&gt;</span> <span class="cm-variable" style="">movies</span> <span class="cm-operator" style="">=</span> <span class="cm-variable" style="">Arrays</span>.<span class="cm-variable" style="">asList</span>(</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Lord of the rings"</span>, <span class="cm-number" style="color: #116644;">8.8</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Back to the future"</span>, <span class="cm-number" style="color: #116644;">8.5</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Carlito's way"</span>, <span class="cm-number" style="color: #116644;">7.9</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Pulp fiction"</span>, <span class="cm-number" style="color: #116644;">8.9</span>));</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">comparingDouble</span>(<span class="cm-variable" style="">Movie</span>::<span class="cm-variable" style="">getRating</span>)</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">                      .<span class="cm-variable" style="">reversed</span>());</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">forEach</span>(<span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>::<span class="cm-variable" style="">println</span>);</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 218px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We used the&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html#reversed--" target="_blank">reversed</a>&nbsp;function on the Comparator&nbsp;in order to invert default natural order; that is, from lowest to highest. Comparator.comparingDouble() uses Double.compare() under the hood.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">If you need to compare int or long, you can use&nbsp;comparingInt() and&nbsp;comparingLong() respectively.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Sort a List&nbsp;With a Custom Comparator</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In the previous examples, we haven’t specified any Comparator since it wasn’t necessary, but let’s see an example in which we define our own&nbsp;Comparator. Our Movie class has a new&nbsp;field – “starred” –&nbsp;set using the third constructor parameter. In the example, we want to sort the list so that we&nbsp;have starred movies at the top of the List.&nbsp;</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 412.75px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">List</span><span class="cm-operator" style="">&lt;</span><span class="cm-variable" style="">Movie</span><span class="cm-operator" style="">&gt;</span> <span class="cm-variable" style="">movies</span> <span class="cm-operator" style="">=</span> <span class="cm-variable" style="">Arrays</span>.<span class="cm-variable" style="">asList</span>(</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Lord of the rings"</span>, <span class="cm-number" style="color: #116644;">8.8</span>, <span class="cm-atom" style="color: #221199;">true</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Back to the future"</span>, <span class="cm-number" style="color: #116644;">8.5</span>, <span class="cm-atom" style="color: #221199;">false</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Carlito's way"</span>, <span class="cm-number" style="color: #116644;">7.9</span>, <span class="cm-atom" style="color: #221199;">true</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Pulp fiction"</span>, <span class="cm-number" style="color: #116644;">8.9</span>, <span class="cm-atom" style="color: #221199;">false</span>));</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Comparator</span><span class="cm-operator" style="">&lt;</span><span class="cm-variable" style="">Movie</span><span class="cm-operator" style="">&gt;</span>() {</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-meta" style="color: #555555;">@Override</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable" style="">compare</span>(<span class="cm-variable" style="">Movie</span> <span class="cm-variable" style="">m1</span>, <span class="cm-variable" style="">Movie</span> <span class="cm-variable" style="">m2</span>) {</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">if</span>(<span class="cm-variable" style="">m1</span>.<span class="cm-variable" style="">getStarred</span>() <span class="cm-operator" style="">==</span> <span class="cm-variable" style="">m2</span>.<span class="cm-variable" style="">getStarred</span>()){</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">            <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-number" style="color: #116644;">0</span>;</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        }</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable" style="">m1</span>.<span class="cm-variable" style="">getStarred</span>() <span class="cm-operator" style="">?</span> <span class="cm-operator" style="">-</span><span class="cm-number" style="color: #116644;">1</span> : <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            14
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">     }</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            15
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">});</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            16
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            17
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">forEach</span>(<span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>::<span class="cm-variable" style="">println</span>);</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 344px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The result will be:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 475.078px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{starred=true, title='Lord of the rings', rating=8.8}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{starred=true, title='Carlito's way', rating=7.9}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{starred=false, title='Back to the future', rating=8.5}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">Movie{starred=false, title='Pulp fiction', rating=8.9}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 110px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We can, of course, use a lambda expression instead of Anonymous class, as follows:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 342.562px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">sort</span>((<span class="cm-variable" style="">m1</span>, <span class="cm-variable" style="">m2</span>) <span class="cm-operator" style="">-&gt;</span> {</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">if</span>(<span class="cm-variable" style="">m1</span>.<span class="cm-variable" style="">getStarred</span>() <span class="cm-operator" style="">==</span> <span class="cm-variable" style="">m2</span>.<span class="cm-variable" style="">getStarred</span>()){</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-number" style="color: #116644;">0</span>;</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable" style="">m1</span>.<span class="cm-variable" style="">getStarred</span>() <span class="cm-operator" style="">?</span> <span class="cm-operator" style="">-</span><span class="cm-number" style="color: #116644;">1</span> : <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">});</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 146px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">We can also use Comparator.comparing() again:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 561.031px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">comparing</span>(<span class="cm-variable" style="">Movie</span>::<span class="cm-variable" style="">getStarred</span>, (<span class="cm-variable" style="">star1</span>, <span class="cm-variable" style="">star2</span>) <span class="cm-operator" style="">-&gt;</span> {</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">if</span>(<span class="cm-variable" style="">star1</span> <span class="cm-operator" style="">==</span> <span class="cm-variable" style="">star2</span>){</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">         <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-number" style="color: #116644;">0</span>;</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable" style="">star1</span> <span class="cm-operator" style="">?</span> <span class="cm-operator" style="">-</span><span class="cm-number" style="color: #116644;">1</span> : <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}));</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 146px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In the last example, Comparator.comparing() takes the function to extract the key to use&nbsp;for sorting as the first parameter, and a Comparator as the&nbsp;second parameter. This Comparator uses the extracted keys for comparison; star1 and star2&nbsp;are boolean&nbsp;and represent m1.getStarred() and m2.getStarred()&nbsp;respectively.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Sort a List&nbsp;With Chain of&nbsp;Comparators</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In the last example, we want to have starred movie at the top and then sort by rating.</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 592.188px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">List</span><span class="cm-operator" style="">&lt;</span><span class="cm-variable" style="">Movie</span><span class="cm-operator" style="">&gt;</span> <span class="cm-variable" style="">movies</span> <span class="cm-operator" style="">=</span> <span class="cm-variable" style="">Arrays</span>.<span class="cm-variable" style="">asList</span>(</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Lord of the rings"</span>, <span class="cm-number" style="color: #116644;">8.8</span>, <span class="cm-atom" style="color: #221199;">true</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Back to the future"</span>, <span class="cm-number" style="color: #116644;">8.5</span>, <span class="cm-atom" style="color: #221199;">false</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Carlito's way"</span>, <span class="cm-number" style="color: #116644;">7.9</span>, <span class="cm-atom" style="color: #221199;">true</span>),</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable" style="">Movie</span>(<span class="cm-string" style="color: #aa1111;">"Pulp fiction"</span>, <span class="cm-number" style="color: #116644;">8.9</span>, <span class="cm-atom" style="color: #221199;">false</span>));</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">sort</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">comparing</span>(<span class="cm-variable" style="">Movie</span>::<span class="cm-variable" style="">getStarred</span>)</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">                      .<span class="cm-variable" style="">reversed</span>()</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">                      .<span class="cm-variable" style="">thenComparing</span>(<span class="cm-variable" style="">Comparator</span>.<span class="cm-variable" style="">comparing</span>(<span class="cm-variable" style="">Movie</span>::<span class="cm-variable" style="">getRating</span>)</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">                      .<span class="cm-variable" style="">reversed</span>())</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">);</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span style="">​</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">movies</span>.<span class="cm-variable" style="">forEach</span>(<span class="cm-variable" style="">System</span>.<span class="cm-variable" style="">out</span>::<span class="cm-variable" style="">println</span>);</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 272px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">And the output is:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll" style=""> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 475.188px; padding-right: 0px; padding-bottom: 0px;"> 
     <div style=""> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div style=""> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors" style="">
         &nbsp;
        </div> 
        <div class="CodeMirror-code" style=""> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">Movie</span>{<span class="cm-variable" style="">starred</span><span class="cm-operator" style="">=</span><span class="cm-atom" style="color: #221199;">true</span>, <span class="cm-variable" style="">title</span><span class="cm-operator" style="">=</span><span class="cm-string" style="color: #aa1111;">'Lord of the rings'</span>, <span class="cm-variable" style="">rating</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">8.8</span>}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">Movie</span>{<span class="cm-variable" style="">starred</span><span class="cm-operator" style="">=</span><span class="cm-atom" style="color: #221199;">true</span>, <span class="cm-variable" style="">title</span><span class="cm-operator" style="">=</span><span class="cm-string" style="color: #aa1111;">'Carlito'</span><span class="cm-variable" style="">s</span> <span class="cm-variable" style="">way</span><span class="cm-string" style="color: #aa1111;">', rating=7.9}</span></span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">Movie</span>{<span class="cm-variable" style="">starred</span><span class="cm-operator" style="">=</span><span class="cm-atom" style="color: #221199;">false</span>, <span class="cm-variable" style="">title</span><span class="cm-operator" style="">=</span><span class="cm-string" style="color: #aa1111;">'Pulp fiction'</span>, <span class="cm-variable" style="">rating</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">8.9</span>}</span></pre> 
         </div> 
         <div style=""> 
          <div class="CodeMirror-gutter-wrapper" style=""> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable" style="">Movie</span>{<span class="cm-variable" style="">starred</span><span class="cm-operator" style="">=</span><span class="cm-atom" style="color: #221199;">false</span>, <span class="cm-variable" style="">title</span><span class="cm-operator" style="">=</span><span class="cm-string" style="color: #aa1111;">'Back to the future'</span>, <span class="cm-variable" style="">rating</span><span class="cm-operator" style="">=</span><span class="cm-number" style="color: #116644;">8.5</span>}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 110px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As you’ve seen, we first sort by starred&nbsp;and then by rating – both reversed because we want highest value and true first.</p> 
</div>