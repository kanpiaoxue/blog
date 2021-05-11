#Java Getter and Setter: Basics, Common Mistakes, and Best Practices
###发表时间：2021-02-22
###分类：经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519249" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519249</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>文章地址：&nbsp;<a href="https://dzone.com/articles/java-getter-and-setter-basics-common-mistakes-and">https://dzone.com/articles/java-getter-and-setter-basics-common-mistakes-and</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Getter and setter are widely used in Java. It is seemingly simple, but not every programmer understands and implements this kind of method properly. So in this article, I would like to deeply discuss getter and setter methods in Java — from the basics to common mistakes and best practices.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">If you are already good with the basics, jump directly to section 4 where I talk about common mistakes and best practices.</p> 
 <blockquote style="padding: 8px 35px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 725.047px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  You may also like:&nbsp;
  <a style="background-color: transparent; color: #29a8ff;" href="https://dzone.com/articles/why-should-i-write-getters-and-setters">Why Should I Write Getters and Setters?</a> 
 </blockquote> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">1. What Are Getter and Setter?</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In Java, getter and setter are two conventional methods that are used for retrieving and updating the value of a variable.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The following code is an example of a simple class with a private variable and a couple of getter/setter methods:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 287.891px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">class</span> <span class="cm-def" style="color: #0000ff;">SimpleGetterAndSetter</span> {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">number</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">getNumber</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">number</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">setNumber</span>(<span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">num</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">number</span> <span class="cm-operator">=</span> <span class="cm-variable">num</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 236px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The class declares a private variable, number. Since number is private, the code from the outside of this class cannot access the variable directly, as shown below:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 482.953px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">SimpleGetterAndSetter</span> <span class="cm-variable">obj</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">SimpleGetterAndSetter</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">obj</span>.<span class="cm-variable">number</span> <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">10</span>;    <span class="cm-comment" style="color: #aa5500;">// compile error, since number is private</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">num</span> <span class="cm-operator">=</span> <span class="cm-variable">obj</span>.<span class="cm-variable">number</span>; <span class="cm-comment" style="color: #aa5500;">// same as above</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Instead, the outside code has to invoke the getter, &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">getNumber()</code>, and the setter, &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">setNumber()</code>, in order to read or update the variable, for example:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 443.938px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">SimpleGetterAndSetter</span> <span class="cm-variable">obj</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">SimpleGetterAndSetter</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">obj</span>.<span class="cm-variable">setNumber</span>(<span class="cm-number" style="color: #116644;">10</span>);  <span class="cm-comment" style="color: #aa5500;">// OK</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">num</span> <span class="cm-operator">=</span> <span class="cm-variable">obj</span>.<span class="cm-variable">getNumber</span>();  <span class="cm-comment" style="color: #aa5500;">// fine</span></span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So, a setter is a method that updates the value of a variable. And a getter is a method that reads the value of a variable. Getter and setter are also known as&nbsp;<strong><em>accessor&nbsp;</em></strong>and&nbsp;<strong><em>mutator&nbsp;</em></strong>in Java.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">2. Why Do We Need Getter and Setter?</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">By using getter and setter, the programmer can control how their important variables are accessed and updated in the proper manner, such as changing the value of a variable within a specified range. Consider the following code of a setter method:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 358.109px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setNumber</span>(<span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">num</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">if</span> (<span class="cm-variable">num</span> <span class="cm-operator">&lt;</span> <span class="cm-number" style="color: #116644;">10</span> <span class="cm-operator">||</span> <span class="cm-variable">num</span> <span class="cm-operator">&gt;</span> <span class="cm-number" style="color: #116644;">100</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">throw</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">IllegalArgumentException</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">number</span> <span class="cm-operator">=</span> <span class="cm-variable">num</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This ensures that the value of the number is always set between 10 and 100. Suppose the variable number can be updated directly, the caller can set any arbitrary value to it:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 124.094px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">obj</span>.<span class="cm-variable">number</span> <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">3</span>;</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">And that violates the constraint for values ranging from 10 to 100 for that variable. Of course, we don’t expect that to happen. Thus, hiding the variable number as private and then using a setter comes to the rescue.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">On the other hand, a getter method is the only way for the outside world to read the variable’s value:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 194.281px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">int</span> <span class="cm-def" style="color: #0000ff;">getNumber</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">number</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The following picture illustrates the situation:</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><img class="fr-fin fr-dib" style="vertical-align: middle; max-width: 100%; height: auto; text-align: center; margin: auto; display: block; float: none !important;" title="Getter and setter visual" src="https://dzone.com/storage/temp/12536086-getter-and-setter.png" alt="Getter and setter visual" width="650"></p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So far, the setter and getter methods protect a variable’s value from unexpected changes by the outside world — the caller code.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">When a variable is hidden by the&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/java-core/the-java-language/private-keyword" target="_blank">private modifier</a>&nbsp;and can be accessed only through getter and setter, it is&nbsp;<em>encapsulated</em>.&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/java-core/the-java-language/what-is-encapsulation-in-java-the-what-why-and-how" target="_blank">Encapsulation</a>&nbsp;is one of the fundamental principles in object-oriented programming (OOP), thus implementing getter and setter is one of the ways to enforce encapsulation in the program’s code.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Some frameworks such as&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/frameworks/hibernate" target="_blank">Hibernate</a>,&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/frameworks/spring" target="_blank">Spring</a>, and&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/frameworks/struts" target="_blank">Struts</a>&nbsp;can inspect information or inject their utility code through getter and setter. So providing getter and setter is necessary when integrating your code with such frameworks.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">3. Naming Convention for Getter and Setter</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The naming scheme of setter and getter should follow the&nbsp;<em>Java bean naming convention</em>&nbsp;as &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">getXxx()</code>&nbsp;and &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">setXxx()</code>, where&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Xxx</code>&nbsp;is the name of the variable. For example, with the following variable name:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 163.078px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>;</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The appropriate setter and getter will be:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 287.938px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setName</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>) { }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-def" style="color: #0000ff;">getName</span>() { }</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">If the variable is of the type boolean, then the getter’s name can be either&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">isXXX()</code>&nbsp;or &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">getXXX()</code>, but the former naming is preferred. For example:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 225.484px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">boolean</span> <span class="cm-variable">single</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-def" style="color: #0000ff;">isSingle</span>() { }</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The following table shows some examples of getters and setters which qualified for the naming convention:</p> 
 <table style="border-collapse: collapse; border-spacing: 0px; width: 853px; margin-bottom: 10px; margin-top: 10px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; display: block; color: #222635; font-size: 19px;" border="1" cellspacing="0" cellpadding="0">
  <tbody> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="169"> <p style="margin-top: 5px; margin-bottom: 15px;"><strong>Variable declaration</strong></p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="192"> <p style="margin-top: 5px; margin-bottom: 15px;"><strong>Getter method</strong></p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="277"> <p style="margin-top: 5px; margin-bottom: 15px;"><strong>Setter method</strong></p> </td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="169"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">int quantity</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="192"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">int getQuantity()</code><span id="_tmp_pre_8">&nbsp;</span></p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="277"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">void setQuantity(int qty)</code><span id="_tmp_pre_9">&nbsp;</span></p> </td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="169"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">string firstName</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="192"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">String getFirstName()</code><span id="_tmp_pre_10">&nbsp;</span></p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="277"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">void setFirstName(String fname)</code><span id="_tmp_pre_11">&nbsp;</span></p> </td> 
   </tr> 
   <tr style="background-color: #e2e1e1;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="169"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">Date birthday</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="192"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Date getBirthday()</code><span id="_tmp_pre_12">&nbsp;</span></p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="277"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">void setBirthday(Date bornDate)</code><span id="_tmp_pre_13">&nbsp;</span></p> </td> 
   </tr> 
   <tr style="background-color: #f3f3f3;"> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="169"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">boolean rich</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="192"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">boolean isRich()</code><span id="_tmp_pre_15">&nbsp;</span></p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">boolean getRich()</code><span id="_tmp_pre_16">&nbsp;</span></p> </td> 
    <td style="padding: 5px 10px; border: 1px solid #cccccc; font-size: 14px; font-family: Cambira, Georgia, serif;" valign="top" width="277"> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;</p> <p style="margin-top: 5px; margin-bottom: 15px;">&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 12.6px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">void setRich(Boolean rich)</code><span id="_tmp_pre_14">&nbsp;</span></p> </td> 
   </tr> 
  </tbody>
 </table> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">4. Common Mistakes When Implementing Getter and Setter</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">People often make mistakes, and developers are no exception. This section describes the most common mistakes when implementing setters and getters in Java, as well as workarounds.</p> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong>Mistake #1: You have setter and getter, but the variable is declared in a less restricted scope.</strong></h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Consider the following code snippet:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 319.141px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">firstName</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setFirstName</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">fname</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">firstName</span> <span class="cm-operator">=</span> <span class="cm-variable">fname</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-def" style="color: #0000ff;">getFirstName</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">firstName</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The variable&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">firstName</code>&nbsp;is declared as&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/java-core/the-java-language/public-keyword" target="_blank">public</a>, so it can be accessed using the dot (.) operator directly, making the setter and getter useless. A workaround for this case is using more restricted access modifier such as&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/java-core/the-java-language/protected-keyword" target="_blank">protected</a>&nbsp;and&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://www.codejava.net/java-core/the-java-language/private-keyword" target="_blank">private</a>:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 202.078px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">firstName</span>;</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">In the book&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://amzn.to/2YibYrg" rel="nofollow" target="_blank">Effective Java</a>, Joshua Bloch points out this problem in item 14:</p> 
 <blockquote style="padding: 8px 35px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 725.047px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  "In public classes, use accessor methods, not public fields."
 </blockquote> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong>Mistake #2: Assign object reference directly in the setter</strong></h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Considering the following setter method:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 272.312px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">scores</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setScores</span>(<span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">scr</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span> <span class="cm-operator">=</span> <span class="cm-variable">scr</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The following code demonstrates this problem:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 288px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">myScores</span> <span class="cm-operator">=</span> {<span class="cm-number" style="color: #116644;">5</span>, <span class="cm-number" style="color: #116644;">5</span>, <span class="cm-number" style="color: #116644;">4</span>, <span class="cm-number" style="color: #116644;">3</span>, <span class="cm-number" style="color: #116644;">2</span>, <span class="cm-number" style="color: #116644;">4</span>};</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">setScores</span>(<span class="cm-variable">myScores</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">displayScores</span>();   </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">myScores</span>[<span class="cm-number" style="color: #116644;">1</span>] <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">displayScores</span>();</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">An array of integer numbers,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">myScores</code>, is initialized with 6 values (line 1) and the array is passed to the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">setScores()</code>&nbsp;method (line 2). The method&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">displayScores()</code>&nbsp;simply prints out all scores from the array:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 397.281px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">displayScores</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">for</span> (<span class="cm-type" style="color: #008855;">int</span> <span class="cm-variable">i</span> <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">0</span>; <span class="cm-variable">i</span> <span class="cm-operator">&lt;</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span>.<span class="cm-variable">length</span>; <span class="cm-variable">i</span><span class="cm-operator">++</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">print</span>(<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span>[<span class="cm-variable">i</span>] <span class="cm-operator">+</span> <span class="cm-string" style="color: #aa1111;">" "</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Line 3 will produce the following output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 92.9375px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">4</span> <span class="cm-number" style="color: #116644;">3</span> <span class="cm-number" style="color: #116644;">2</span> <span class="cm-number" style="color: #116644;">4</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">These are all the elements of the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">myScores</code>&nbsp;array. Now, in line 4, we can modify the value of the 2<span>nd</span>&nbsp;element in the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">myScores</code>&nbsp;array as follows:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 131.906px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">myScores</span>[<span class="cm-number" style="color: #116644;">1</span>] <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">What will happen if we call the method &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">displayScores()&nbsp;</code>again at line 5? Well, it will produce the following output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 92.9375px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">1</span> <span class="cm-number" style="color: #116644;">4</span> <span class="cm-number" style="color: #116644;">3</span> <span class="cm-number" style="color: #116644;">2</span> <span class="cm-number" style="color: #116644;">4</span></span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">You realize that the value of the 2<span>nd</span>&nbsp;element is changed from 5 to 1, as a result of the assignment in line 4. Why does it matter? Well, that means the data can be modified outside the scope of the setter method, which breaks the encapsulation purpose of the setter. And why does that happen? Let’s look at the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">setScores()</code>&nbsp; method again:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 272.312px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setScores</span>(<span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">scr</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span> <span class="cm-operator">=</span> <span class="cm-variable">scr</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The member variable scores are assigned to the method’s parameter variable&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scr</code>&nbsp;directly. That means both of the variables are referring to the same object in memory — the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">myScores</code>&nbsp;array object. So changes made to either the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>&nbsp;or&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">myScores</code>&nbsp;variables are actually made on the same object.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">A workaround for this situation is to copy elements from the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scr</code>&nbsp;array to the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>&nbsp;array, one by one. The modified version of the setter would look like this:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 451.828px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setScores</span>(<span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">scr</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-type" style="color: #008855;">int</span>[<span class="cm-variable">scr</span>.<span class="cm-variable">length</span>];</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-variable">System</span>.<span class="cm-variable">arraycopy</span>(<span class="cm-variable">scr</span>, <span class="cm-number" style="color: #116644;">0</span>, <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span>, <span class="cm-number" style="color: #116644;">0</span>, <span class="cm-variable">scr</span>.<span class="cm-variable">length</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">What’s the difference? Well, the member variable&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>&nbsp;is no longer referring to the object referred by the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scr</code>&nbsp;variable. Instead, the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>&nbsp;is initialized to a new one with size equals to the size of the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scr</code>. Then, we copy all elements from the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scr</code>&nbsp;to the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>, using&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">System.arraycopy()</code>&nbsp;method.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Run the following example again, and it will give us the following output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 92.9375px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">4</span> <span class="cm-number" style="color: #116644;">3</span> <span class="cm-number" style="color: #116644;">2</span> <span class="cm-number" style="color: #116644;">4</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">4</span> <span class="cm-number" style="color: #116644;">3</span> <span class="cm-number" style="color: #116644;">2</span> <span class="cm-number" style="color: #116644;">4</span></span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Now, the two invocations of&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">displayScores()</code>&nbsp;produce the same output. That means the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>&nbsp;is independent and different than the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scr</code>&nbsp;passed into the setter, thus we have the assignment:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 131.906px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">myScores</span>[<span class="cm-number" style="color: #116644;">1</span>] <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 56px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">This does not affect the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So, the rule of thumb is: If you pass an object reference into a setter method, then don’t copy that reference into the internal variable directly. Instead, you should find some ways to copy values of the passed object into the internal object, like we have copied elements from one array to another using the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">System.arraycopy()</code>&nbsp; method.</p> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong>Mistake #3: Return the object reference directly in getter</strong></h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Consider the following getter method:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 209.875px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">scores</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-def" style="color: #0000ff;">getScores</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">And then look at the following code snippet:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 288px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">myScores</span> <span class="cm-operator">=</span> {<span class="cm-number" style="color: #116644;">5</span>, <span class="cm-number" style="color: #116644;">5</span>, <span class="cm-number" style="color: #116644;">4</span>, <span class="cm-number" style="color: #116644;">3</span>, <span class="cm-number" style="color: #116644;">2</span>, <span class="cm-number" style="color: #116644;">4</span>};</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">setScores</span>(<span class="cm-variable">myScores</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">displayScores</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">copyScores</span> <span class="cm-operator">=</span> <span class="cm-variable">getScores</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">copyScores</span>[<span class="cm-number" style="color: #116644;">1</span>] <span class="cm-operator">=</span> <span class="cm-number" style="color: #116644;">1</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">displayScores</span>();</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 236px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">It will produce the following output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 92.9375px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">4</span> <span class="cm-number" style="color: #116644;">3</span> <span class="cm-number" style="color: #116644;">2</span> <span class="cm-number" style="color: #116644;">4</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-number" style="color: #116644;">5</span> <span class="cm-number" style="color: #116644;">1</span> <span class="cm-number" style="color: #116644;">4</span> <span class="cm-number" style="color: #116644;">3</span> <span class="cm-number" style="color: #116644;">2</span> <span class="cm-number" style="color: #116644;">4</span></span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As you notice, the 2<span>nd</span>&nbsp;element of the array&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">scores</code>&nbsp;is modified outside the setter, in line 5. Because the getter method returns the reference of the internal variable scores directly, the outside code can obtain this reference and make a change to the internal object.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">A workaround for this case is that, instead of returning the reference directly in the getter, we should return a copy of the object. This is so that the outside code can obtain only a copy, not the internal object. Therefore, we modify the above getter as follows:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 467.453px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-def" style="color: #0000ff;">getScores</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-type" style="color: #008855;">int</span>[] <span class="cm-variable">copy</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-type" style="color: #008855;">int</span>[<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span>.<span class="cm-variable">length</span>];</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-variable">System</span>.<span class="cm-variable">arraycopy</span>(<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">scores</span>, <span class="cm-number" style="color: #116644;">0</span>, <span class="cm-variable">copy</span>, <span class="cm-number" style="color: #116644;">0</span>, <span class="cm-variable">copy</span>.<span class="cm-variable">length</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable">copy</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So the rule of thumb is: Do not return a reference of the original object in the getter method. Instead, it should return a copy of the original object.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">5. Implementing Getters and Setters for Primitive Types</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">With primitive types (<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">int</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">float</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">double</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">boolean</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">char</code>…), you can freely assign/return values directly in setter/getter because Java copies the value of one primitive to another instead of copying the object reference. So, mistakes #2 and #3 can easily be avoided.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For example, the following code is safe because the setter and getter are involved in a primitive type of&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">float</code>:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 295.734px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-keyword" style="color: #770088;">float</span> <span class="cm-variable">amount</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setAmount</span>(<span class="cm-keyword" style="color: #770088;">float</span> <span class="cm-variable">amount</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">amount</span> <span class="cm-operator">=</span> <span class="cm-variable">amount</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">float</span> <span class="cm-variable">getAmount</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">amount</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So, for primitive types, there is no special trick to correctly implement the getter and setter.</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">6. Implementing Getters and Setters for Common Object Types</h2> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong>Getters and Setters for String Objects:</strong></h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">String is an object type, but it is immutable, which means once a String object is created, its String literal cannot be changed. In other words, every change on that String object will result in a newly created String object. So, like primitive types, you can safely implement getter and setter for a String variable, like this:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 295.734px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">address</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setAddress</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">addr</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">address</span> <span class="cm-operator">=</span> <span class="cm-variable">addr</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-def" style="color: #0000ff;">getAddress</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">address</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <h3 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 25px; clear: both;"><strong>Getters and Setters for Date Objects:</strong></h3> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">java.util.Date</code>&nbsp;class implements the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method from the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Object</code>&nbsp;class. The method&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;returns a copy of the object, so we can use it for the getter and setter, as shown in the following example:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 326.984px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-variable">Date</span> <span class="cm-variable">birthDate</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setBirthDate</span>(<span class="cm-variable">Date</span> <span class="cm-variable">date</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">birthDate</span> <span class="cm-operator">=</span> (<span class="cm-variable">Date</span>) <span class="cm-variable">date</span>.<span class="cm-variable">clone</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">Date</span> <span class="cm-def" style="color: #0000ff;">getBirthDate</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> (<span class="cm-variable">Date</span>) <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">birthDate</span>.<span class="cm-variable">clone</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method returns an&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Object</code>, so we must cast it to the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Date</code>&nbsp;type.You can learn more about this in item 39 of&nbsp;<a style="background-color: transparent; color: #29a8ff;" href="https://amzn.to/2YibYrg" rel="nofollow" target="_blank">Effective Java</a>&nbsp;by&nbsp;Joshua Bloch:</p> 
 <blockquote style="padding: 8px 35px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 725.047px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;">
  "Make defensive copies when needed."&nbsp;
 </blockquote> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">7. Implementing Getters and Setters for Collection Types</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As described in mistakes #2 and #3, it’s not good to have setter and getter methods like this:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 381.578px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">listTitles</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setListTitles</span>(<span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">titles</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listTitles</span> <span class="cm-operator">=</span> <span class="cm-variable">titles</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-def" style="color: #0000ff;">getListTitles</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listTitles</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Consider the following program:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 521.984px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">import</span> <span class="cm-variable">java</span>.<span class="cm-variable">util</span>.<span class="cm-operator">*</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">class</span> <span class="cm-def" style="color: #0000ff;">CollectionGetterSetter</span> {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">listTitles</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">setListTitles</span>(<span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">titles</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listTitles</span> <span class="cm-operator">=</span> <span class="cm-variable">titles</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">getListTitles</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listTitles</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            14
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">static</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">main</span>(<span class="cm-type" style="color: #008855;">String</span>[] <span class="cm-variable">args</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            15
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">CollectionGetterSetter</span> <span class="cm-variable">app</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">CollectionGetterSetter</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            16
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">titles1</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            17
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">titles1</span>.<span class="cm-variable">add</span>(<span class="cm-string" style="color: #aa1111;">"Name"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            18
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">titles1</span>.<span class="cm-variable">add</span>(<span class="cm-string" style="color: #aa1111;">"Address"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            19
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">titles1</span>.<span class="cm-variable">add</span>(<span class="cm-string" style="color: #aa1111;">"Email"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            20
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">titles1</span>.<span class="cm-variable">add</span>(<span class="cm-string" style="color: #aa1111;">"Job"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            21
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            22
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">app</span>.<span class="cm-variable">setListTitles</span>(<span class="cm-variable">titles1</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            23
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            24
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"Titles 1: "</span> <span class="cm-operator">+</span> <span class="cm-variable">titles1</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            25
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            26
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">titles1</span>.<span class="cm-variable">set</span>(<span class="cm-number" style="color: #116644;">2</span>, <span class="cm-string" style="color: #aa1111;">"Habilitation"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            27
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            28
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">titles2</span> <span class="cm-operator">=</span> <span class="cm-variable">app</span>.<span class="cm-variable">getListTitles</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            29
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"Titles 2: "</span> <span class="cm-operator">+</span> <span class="cm-variable">titles2</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            30
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            31
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">titles2</span>.<span class="cm-variable">set</span>(<span class="cm-number" style="color: #116644;">0</span>, <span class="cm-string" style="color: #aa1111;">"Full name"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            32
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            33
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">titles3</span> <span class="cm-operator">=</span> <span class="cm-variable">app</span>.<span class="cm-variable">getListTitles</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            34
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"Titles 3: "</span> <span class="cm-operator">+</span> <span class="cm-variable">titles3</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            35
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            36
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            37
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            38
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 722px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">According to the rules for implementing getter and setter, the three&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">System.out.println()</code>&nbsp;statements should produce the same result. However, when running the above program, it produces the following output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 389.375px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">Titles</span> <span class="cm-number" style="color: #116644;">1</span>: [<span class="cm-variable">Name</span>, <span class="cm-variable">Address</span>, <span class="cm-variable">Email</span>, <span class="cm-variable">Job</span>]</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">Titles</span> <span class="cm-number" style="color: #116644;">2</span>: [<span class="cm-variable">Name</span>, <span class="cm-variable">Address</span>, <span class="cm-variable">Habilitation</span>, <span class="cm-variable">Job</span>]</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">Titles</span> <span class="cm-number" style="color: #116644;">3</span>: [<span class="cm-variable">Full</span> <span class="cm-variable">name</span>, <span class="cm-variable">Address</span>, <span class="cm-variable">Habilitation</span>, <span class="cm-variable">Job</span>]</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">For a collection of Strings, one solution is to use the constructor that takes another collection as an argument. For example, we can change the code of the above getter and setter as follows:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 420.594px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setListTitles</span>(<span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-variable">titles</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listTitles</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span>(<span class="cm-variable">titles</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span> <span class="cm-def" style="color: #0000ff;">getListTitles</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-type" style="color: #008855;">String</span><span class="cm-operator">&gt;</span>(<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listTitles</span>);   </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 164px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Re-compile and run the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">CollectionGetterSetter</code>&nbsp;program; it will produce the desired output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 295.734px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">Titles</span> <span class="cm-number" style="color: #116644;">1</span>: [<span class="cm-variable">Name</span>, <span class="cm-variable">Address</span>, <span class="cm-variable">Email</span>, <span class="cm-variable">Job</span>]</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">Titles</span> <span class="cm-number" style="color: #116644;">2</span>: [<span class="cm-variable">Name</span>, <span class="cm-variable">Address</span>, <span class="cm-variable">Email</span>, <span class="cm-variable">Job</span>]</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">Titles</span> <span class="cm-number" style="color: #116644;">3</span>: [<span class="cm-variable">Name</span>, <span class="cm-variable">Address</span>, <span class="cm-variable">Email</span>, <span class="cm-variable">Job</span>]</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><strong>NOTE</strong>: The constructor approach above is only working with Collections of&nbsp;<strong>Strings</strong>, but it will not work for Collections&nbsp;<strong>objects</strong>. Consider the following example for a Collection of the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Person</code>&nbsp;object:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 623.391px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">import</span> <span class="cm-variable">java</span>.<span class="cm-variable">util</span>.<span class="cm-operator">*</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">class</span> <span class="cm-def" style="color: #0000ff;">CollectionGetterSetterObject</span> { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">listPeople</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">setListPeople</span>(<span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list</span>) { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listPeople</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>(<span class="cm-variable">list</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">getListPeople</span>() { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>(<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listPeople</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            14
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">static</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">main</span>(<span class="cm-type" style="color: #008855;">String</span>[] <span class="cm-variable">args</span>) { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            15
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">CollectionGetterSetterObject</span> <span class="cm-variable">app</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">CollectionGetterSetterObject</span>(); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            16
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            17
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list1</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>(); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            18
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">add</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-string" style="color: #aa1111;">"Peter"</span>)); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            19
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">add</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-string" style="color: #aa1111;">"Alice"</span>)); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            20
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">add</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-string" style="color: #aa1111;">"Mary"</span>)); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            21
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            22
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">app</span>.<span class="cm-variable">setListPeople</span>(<span class="cm-variable">list1</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            23
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            24
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"List 1: "</span> <span class="cm-operator">+</span> <span class="cm-variable">list1</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            25
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            26
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">get</span>(<span class="cm-number" style="color: #116644;">2</span>).<span class="cm-variable">setName</span>(<span class="cm-string" style="color: #aa1111;">"Maryland"</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            27
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            28
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list2</span> <span class="cm-operator">=</span> <span class="cm-variable">app</span>.<span class="cm-variable">getListPeople</span>(); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            29
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"List 2: "</span> <span class="cm-operator">+</span> <span class="cm-variable">list2</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            30
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            31
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">get</span>(<span class="cm-number" style="color: #116644;">0</span>).<span class="cm-variable">setName</span>(<span class="cm-string" style="color: #aa1111;">"Peter Crouch"</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            32
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            33
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list3</span> <span class="cm-operator">=</span> <span class="cm-variable">app</span>.<span class="cm-variable">getListPeople</span>(); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            34
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"List 3: "</span> <span class="cm-operator">+</span> <span class="cm-variable">list3</span>); </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            35
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            36
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            37
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">} </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            38
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            39
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">class</span> <span class="cm-def" style="color: #0000ff;">Person</span> { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            40
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            41
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            42
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">Person</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>) { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            43
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span> <span class="cm-operator">=</span> <span class="cm-variable">name</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            44
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            45
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            46
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">getName</span>() { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            47
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            48
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            49
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            50
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">setName</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>) { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            51
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span> <span class="cm-operator">=</span> <span class="cm-variable">name</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            52
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            53
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            54
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">toString</span>() { </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            55
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span>; </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            56
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    } </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            57
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 1064px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">It produces the following output when running:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 311.359px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">List</span> <span class="cm-number" style="color: #116644;">1</span>: [<span class="cm-variable">Peter</span>, <span class="cm-variable">Alice</span>, <span class="cm-variable">Mary</span>]</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">List</span> <span class="cm-number" style="color: #116644;">2</span>: [<span class="cm-variable">Peter</span>, <span class="cm-variable">Alice</span>, <span class="cm-variable">Maryland</span>]</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">List</span> <span class="cm-number" style="color: #116644;">3</span>: [<span class="cm-variable">Peter</span> <span class="cm-variable">Crouch</span>, <span class="cm-variable">Alice</span>, <span class="cm-variable">Maryland</span>]</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Because unlike String, for which new objects will be created whenever a String object is copied, other&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Object</code>&nbsp;types are not. Only references are copied, so that’s why two Collections are distinct but they contain the same objects. In other words, it is because we haven’t provided any means for copying objects.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Look at the Collection API; we found that&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">ArrayList</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">HashMap</code>,&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">HashSet</code>, etc. implement their own&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;methods. These methods return shallow copies, which do not copy elements from the source Collection to the destination. According to the Javadoc of the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method of the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">ArrayList</code>&nbsp;class:</p> 
 <blockquote style="padding: 8px 35px; margin: 30px auto; font-size: 18px; border-left: none; background-color: #ffffff; border-top-color: #545454; border-bottom-color: #545454; color: #222635; width: 725.047px; font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; font-weight: 600; line-height: 1.3; text-align: center;"> 
  <code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 16.2px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">public Object clone()</code>
  <br>
  <code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 16.2px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Returns a shallow copy of this ArrayList instance.<br>(The elements themselves are not copied.)</code> 
 </blockquote> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Thus, we cannot use the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method of these Collection classes. The solution is to implement the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method for our own defined object — the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Person</code>&nbsp;class in the above example. We implement the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method in the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Person</code>&nbsp;class as shown below:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 334.797px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">Object</span> <span class="cm-def" style="color: #0000ff;">clone</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-variable">Person</span> <span class="cm-variable">aClone</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable">aClone</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The setter for&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">listPeople</code>&nbsp;is modified as follows:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 428.375px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setListPeople</span>(<span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">for</span> (<span class="cm-variable">Person</span> <span class="cm-variable">aPerson</span> : <span class="cm-variable">list</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listPeople</span>.<span class="cm-variable">add</span>((<span class="cm-variable">Person</span>) <span class="cm-variable">aPerson</span>.<span class="cm-variable">clone</span>());</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
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
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">The corresponding getter is modified, as shown below:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 428.422px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-def" style="color: #0000ff;">getListPeople</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">listReturn</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">for</span> (<span class="cm-variable">Person</span> <span class="cm-variable">aPerson</span> : <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listPeople</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">listReturn</span>.<span class="cm-variable">add</span>((<span class="cm-variable">Person</span>) <span class="cm-variable">aPerson</span>.<span class="cm-variable">clone</span>());</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable">listReturn</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 182px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">That results in a new version of the class&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">CollectionGetterSetterObject,</code>&nbsp;shown below:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 615.578px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">import</span> <span class="cm-variable">java</span>.<span class="cm-variable">util</span>.<span class="cm-operator">*</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">class</span> <span class="cm-def" style="color: #0000ff;">CollectionGetterSetterObject</span> {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">listPeople</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">setListPeople</span>(<span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">for</span> (<span class="cm-variable">Person</span> <span class="cm-variable">aPerson</span> : <span class="cm-variable">list</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">            <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listPeople</span>.<span class="cm-variable">add</span>((<span class="cm-variable">Person</span>) <span class="cm-variable">aPerson</span>.<span class="cm-variable">clone</span>());</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">getListPeople</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">listReturn</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            14
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">for</span> (<span class="cm-variable">Person</span> <span class="cm-variable">aPerson</span> : <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">listPeople</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            15
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">            <span class="cm-variable">listReturn</span>.<span class="cm-variable">add</span>((<span class="cm-variable">Person</span>) <span class="cm-variable">aPerson</span>.<span class="cm-variable">clone</span>());</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            16
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            17
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            18
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable">listReturn</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            19
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            20
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            21
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-keyword" style="color: #770088;">static</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">main</span>(<span class="cm-type" style="color: #008855;">String</span>[] <span class="cm-variable">args</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            22
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">CollectionGetterSetterObject</span> <span class="cm-variable">app</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">CollectionGetterSetterObject</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            23
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            24
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list1</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">ArrayList</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            25
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">add</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-string" style="color: #aa1111;">"Peter"</span>));</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            26
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">add</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-string" style="color: #aa1111;">"Alice"</span>));</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            27
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">add</span>(<span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-string" style="color: #aa1111;">"Mary"</span>));</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            28
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            29
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">app</span>.<span class="cm-variable">setListPeople</span>(<span class="cm-variable">list1</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            30
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            31
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"List 1: "</span> <span class="cm-operator">+</span> <span class="cm-variable">list1</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            32
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            33
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">get</span>(<span class="cm-number" style="color: #116644;">2</span>).<span class="cm-variable">setName</span>(<span class="cm-string" style="color: #aa1111;">"Maryland"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            34
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            35
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list2</span> <span class="cm-operator">=</span> <span class="cm-variable">app</span>.<span class="cm-variable">getListPeople</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            36
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"List 2: "</span> <span class="cm-operator">+</span> <span class="cm-variable">list2</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            37
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            38
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">list1</span>.<span class="cm-variable">get</span>(<span class="cm-number" style="color: #116644;">0</span>).<span class="cm-variable">setName</span>(<span class="cm-string" style="color: #aa1111;">"Peter Crouch"</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            39
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            40
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">List</span><span class="cm-operator">&lt;</span><span class="cm-variable">Person</span><span class="cm-operator">&gt;</span> <span class="cm-variable">list3</span> <span class="cm-operator">=</span> <span class="cm-variable">app</span>.<span class="cm-variable">getListPeople</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            41
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">System</span>.<span class="cm-variable">out</span>.<span class="cm-variable">println</span>(<span class="cm-string" style="color: #aa1111;">"List 3: "</span> <span class="cm-operator">+</span> <span class="cm-variable">list3</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            42
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            43
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            44
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 830px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Compile and run the new version of&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">CollectionGetterSetterObject</code>; it will produce the desired output:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 233.328px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">List</span> <span class="cm-number" style="color: #116644;">1</span>: [<span class="cm-variable">Peter</span>, <span class="cm-variable">Alice</span>, <span class="cm-variable">Mary</span>] </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">List</span> <span class="cm-number" style="color: #116644;">2</span>: [<span class="cm-variable">Peter</span>, <span class="cm-variable">Alice</span>, <span class="cm-variable">Mary</span>] </span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-variable">List</span> <span class="cm-number" style="color: #116644;">3</span>: [<span class="cm-variable">Peter</span>, <span class="cm-variable">Alice</span>, <span class="cm-variable">Mary</span>]</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So, the key points for implementing getter and setter for a Collection type are:</p> 
 <ul style="margin-bottom: 10px; color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <li style="padding-bottom: 8px;">For a Collection of String objects, it&nbsp;does not need any special tweak since String objects are immutable.</li> 
  <li style="padding-bottom: 8px;">For a Collection of custom types of an object: 
   <ul style="margin-bottom: 0px;"> 
    <li style="padding-bottom: 8px;">Implement the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method for the custom type.</li> 
    <li style="padding-bottom: 8px;">For the setter, add cloned items from the source Collection to the destination one.</li> 
    <li style="padding-bottom: 8px;">For the getter, create a new Collection, which is being returned. Add cloned items from the original Collection to the new one.</li> 
   </ul> </li> 
 </ul> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">8. Implementing Getters and Setters for Your Own Type</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">If you define a custom type of object, you should implement the&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method for your own type. For example:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 366px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">class</span> <span class="cm-def" style="color: #0000ff;">Person</span> {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">private</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            4
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">Person</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            5
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span> <span class="cm-operator">=</span> <span class="cm-variable">name</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            6
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            7
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            8
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">getName</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            9
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            10
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            11
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            12
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-variable">setName</span>(<span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">name</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            13
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span> <span class="cm-operator">=</span> <span class="cm-variable">name</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            14
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            15
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            16
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">String</span> <span class="cm-variable">toString</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            17
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            18
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            19
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span>​</span></span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            20
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">Object</span> <span class="cm-variable">clone</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            21
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-variable">Person</span> <span class="cm-variable">aClone</span> <span class="cm-operator">=</span> <span class="cm-keyword" style="color: #770088;">new</span> <span class="cm-variable">Person</span>(<span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">name</span>);</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            22
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">        <span class="cm-keyword" style="color: #770088;">return</span> <span class="cm-variable">aClone</span>;</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            23
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    }</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            24
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 470px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">As we can see, the class&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">Person</code>&nbsp;implements its &nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code><span id="_tmp_pre_88">&nbsp;</span>method to return a cloned version of itself. Then, the setter method should be implemented like below:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 334.766px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-type" style="color: #008855;">void</span> <span class="cm-def" style="color: #0000ff;">setFriend</span>(<span class="cm-variable">Person</span> <span class="cm-variable">person</span>) {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">friend</span> <span class="cm-operator">=</span> (<span class="cm-variable">Person</span>) <span class="cm-variable">person</span>.<span class="cm-variable">clone</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">And for the getter method:</p> 
 <div style="color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <div class="CodeMirror cm-s-default" style="font-family: monospace; height: auto !important; color: black; overflow: hidden; background-color: #fcfcfc !important; border: 1px solid #d9dcdd; font-size: 13px; clear: both;"> 
   <div class="CodeMirror-scroll"> 
    <div class="CodeMirror-sizer" style="border-right: 30px solid transparent; margin-left: 31px; margin-bottom: 0px; min-width: 319.141px; padding-right: 0px; padding-bottom: 0px;"> 
     <div> 
      <div class="CodeMirror-lines" style="padding: 4px 0px; cursor: text;"> 
       <div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div class="CodeMirror-measure" style="width: 820px; height: 0px; overflow: hidden;">
         &nbsp;
        </div> 
        <div>
         &nbsp;
        </div> 
        <div class="CodeMirror-cursors">
         &nbsp;
        </div> 
        <div class="CodeMirror-code"> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            1
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;"><span class="cm-keyword" style="color: #770088;">public</span> <span class="cm-variable">Person</span> <span class="cm-def" style="color: #0000ff;">getFriend</span>() {</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            2
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">    <span class="cm-keyword" style="color: #770088;">return</span> (<span class="cm-variable">Person</span>) <span class="cm-keyword" style="color: #770088;">this</span>.<span class="cm-variable">friend</span>.<span class="cm-variable">clone</span>();</span></pre> 
         </div> 
         <div> 
          <div class="CodeMirror-gutter-wrapper"> 
           <div class="CodeMirror-linenumber CodeMirror-gutter-elt" style="padding: 0px 3px 0px 5px; min-width: 20px; text-align: right; color: #999999; white-space: nowrap; cursor: default; width: 23px;">
            3
           </div> 
          </div> 
          <pre class=" CodeMirror-line "><span style="padding-right: 0.1px;">}</span></pre> 
         </div> 
        </div> 
       </div> 
      </div> 
     </div> 
    </div> 
    <div style="height: 30px; width: 1px; border-bottom: 0px solid transparent;">
     &nbsp;
    </div> 
    <div class="CodeMirror-gutters" style="border-right: 1px solid #dddddd; background-color: #f7f7f7; white-space: nowrap; height: 92px; width: 30px !important;">
     &nbsp;
    </div> 
   </div> 
  </div> 
 </div> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">&nbsp;</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">So, the rules for implementing getter and setter for a custom object type are:</p> 
 <ul style="margin-bottom: 10px; color: #222635; font-family: Cambria, serif; font-size: 19px;"> 
  <li style="padding-bottom: 8px;">Implement a&nbsp;<code style="font-family: Menlo, Monaco, Consolas, 'Courier New', monospace; font-size: 17.1px; padding: 2px 4px; color: #c7254e; background-color: #f9f2f4; border-radius: 4px;">clone()</code>&nbsp;method for the custom type.</li> 
  <li style="padding-bottom: 8px;">Return a cloned object from the getter.</li> 
  <li style="padding-bottom: 8px;">Assign a cloned object in the setter.</li> 
 </ul> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Conclusion</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Java getter and setter seems to be simple, yet it can be dangerous if implemented naively. It could even be a source of problems that cause your code to misbehave. Or worse, one could easily exploit your programs by insidiously manipulating the arguments to, and returned objects from, your getters and setters. So, be careful and consider implementing the best practices mentioned above.</p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;">Hope you enjoyed!</p> 
 <h2 style="font-family: 'Helvetica Neue', Helvetica, Arial, sans-serif; line-height: 1.2; color: #222635; margin-top: 20px; margin-bottom: 5px; font-size: 30px; clear: both;">Further Reading</h2> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><a style="background-color: transparent; color: #29a8ff;" href="https://dzone.com/articles/why-should-i-write-getters-and-setters">Why Should I Write Getters and Setters?</a></p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><a style="background-color: transparent; color: #29a8ff;" href="https://dzone.com/articles/gettersetterthe-most-hated-practice-in-java">Getter/Setter: The Most Hated Practice in Java</a></p> 
 <p style="margin-top: 5px; margin-bottom: 15px; color: #222635; font-family: Cambria, serif; font-size: 19px;"><a style="background-color: transparent; color: #29a8ff;" href="https://dzone.com/articles/setters-method-handles-and-java-11">Setters, Method Handles, and Java 11</a></p> 
</div>