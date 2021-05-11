#Guava中Strings的操作说明（Guava 23）
###发表时间：2017-08-14
###分类：java,guava
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2389581" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2389581</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考范例：</p> 
 <pre name="code" class="java">String theDigits = CharMatcher.digit().retainFrom("42d3d43gfsdg4fafdasfdasf3f42fsf4fsd3"); // 42343434243
System.out.println(theDigits);
String rs = CharMatcher.whitespace().collapseFrom("42d3 d43  gfsdg4f afdasf        dasf3f 42fsf 4fsd3",' '); // 42d3 d43 gfsdg4f afdasf dasf3f 42fsf 4fsd3
System.out.println(rs);

System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.LOWER_CAMEL, "hello_world")); // helloWorld
System.out.println(CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.LOWER_CAMEL, "_hello_world")); // HelloWorld
System.out.println(CaseFormat.LOWER_CAMEL.to(CaseFormat.LOWER_HYPHEN, "helloWorld")); // hello-world
System.out.println(CaseFormat.LOWER_CAMEL.to(CaseFormat.LOWER_UNDERSCORE, "helloWorld")); // hello_world
System.out.println(CaseFormat.LOWER_CAMEL.to(CaseFormat.UPPER_CAMEL, "helloWorld")); // HelloWorld
System.out.println(CaseFormat.LOWER_CAMEL.to(CaseFormat.UPPER_UNDERSCORE, "helloWorld")); // HELLO_WORLD</pre> 
 <p>&nbsp;</p> 
 <p>文档参考地址： <a href="https://github.com/google/guava/wiki/StringsExplained">https://github.com/google/guava/wiki/StringsExplained</a>&nbsp;</p> 
 <p>&nbsp;</p> 
 <h2 style="">Joiner</h2> 
 <p style="">Joining together a sequence of strings with a separator can be unnecessarily tricky -- but it shouldn't be. If your sequence contains nulls, it can be even harder. The fluent style of&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Joiner.html"><code style="">Joiner</code></a>&nbsp;makes it simple.</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-smi" style="color: #24292e;">Joiner</span> joiner <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">Joiner</span><span class="pl-k" style="color: #d73a49;">.</span>on(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>; <span class="pl-pds" style="">"</span></span>)<span class="pl-k" style="color: #d73a49;">.</span>skipNulls();
<span class="pl-k" style="color: #d73a49;">return</span> joiner<span class="pl-k" style="color: #d73a49;">.</span>join(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>Harry<span class="pl-pds" style="">"</span></span>, <span class="pl-c1" style="color: #005cc5;">null</span>, <span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>Ron<span class="pl-pds" style="">"</span></span>, <span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>Hermione<span class="pl-pds" style="">"</span></span>);</pre> 
 </div> 
 <p style="">returns the string "Harry; Ron; Hermione". Alternately, instead of using&nbsp;<code style="">skipNulls</code>, you may specify a string to use instead of null with&nbsp;<code style="">useForNull(String)</code>.</p> 
 <p style="">You may also use&nbsp;<code style="">Joiner</code>&nbsp;on objects, which will be converted using their&nbsp;<code style="">toString()</code>&nbsp;and then joined.</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-smi" style="color: #24292e;">Joiner</span><span class="pl-k" style="color: #d73a49;">.</span>on(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>,<span class="pl-pds" style="">"</span></span>)<span class="pl-k" style="color: #d73a49;">.</span>join(<span class="pl-smi" style="color: #24292e;">Arrays</span><span class="pl-k" style="color: #d73a49;">.</span>asList(<span class="pl-c1" style="color: #005cc5;">1</span>, <span class="pl-c1" style="color: #005cc5;">5</span>, <span class="pl-c1" style="color: #005cc5;">7</span>)); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> returns "1,5,7"</span></pre> 
 </div> 
 <p style=""><span style="font-weight: 600;">Warning:</span>&nbsp;joiner instances are always immutable. The joiner configuration methods will always return a new&nbsp;<code style="">Joiner</code>, which you must use to get the desired semantics. This makes any&nbsp;<code style="">Joiner</code>&nbsp;thread safe, and usable as a&nbsp;<code style="">static final</code>&nbsp;constant.</p> 
 <h2 style=""> <a id="user-content-splitter" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#splitter"></a>Splitter</h2> 
 <p style="">The built in Java utilities for splitting strings can have some quirky behaviors. For example,&nbsp;<code style="">String.split</code>&nbsp;silently discards trailing separators, and&nbsp;<code style="">StringTokenizer</code>&nbsp;respects exactly five whitespace characters and nothing else.</p> 
 <p style="">Quiz: What does&nbsp;<code style="">",a,,b,".split(",")</code>&nbsp;return?</p> 
 <ol style=""> 
  <li style=""><code style="">"", "a", "", "b", ""</code></li> 
  <li style="margin-top: 0.25em;"><code style="">null, "a", null, "b", null</code></li> 
  <li style="margin-top: 0.25em;"><code style="">"a", null, "b"</code></li> 
  <li style="margin-top: 0.25em;"><code style="">"a", "b"</code></li> 
  <li style="margin-top: 0.25em;">None of the above</li> 
 </ol> 
 <p style="">The correct answer is none of the above:&nbsp;<code style="">"", "a", "", "b"</code>. Only trailing empty strings are skipped. What is this I don't even.</p> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html"><code style="">Splitter</code></a>&nbsp;allows complete control over all this confusing behavior using a reassuringly straightforward fluent pattern.</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-smi" style="color: #24292e;">Splitter</span><span class="pl-k" style="color: #d73a49;">.</span>on(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">'</span>,<span class="pl-pds" style="">'</span></span>)
    .trimResults()
    .omitEmptyStrings()
    .split(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>foo,bar,,   qux<span class="pl-pds" style="">"</span></span>);</pre> 
 </div> 
 <p style="">returns an&nbsp;<code style="">Iterable&lt;String&gt;</code>&nbsp;containing "foo", "bar", "qux". A&nbsp;<code style="">Splitter</code>&nbsp;may be set to split on any&nbsp;<code style="">Pattern</code>,&nbsp;<code style="">char</code>,&nbsp;<code style="">String</code>, or&nbsp;<code style="">CharMatcher</code>.</p> 
 <h4 style=""> <a id="user-content-base-factories" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#base-factories"></a>Base Factories</h4> 
 <table style=""> 
  <thead style="">
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Method</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Description</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Example</th> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#on(char)"><code style="">Splitter.on(char)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Split on occurrences of a specific, individual character.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">Splitter.on(';')</code></td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#on(com.google.common.base.CharMatcher)"><code style="">Splitter.on(CharMatcher)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Split on occurrences of any character in some category.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"> <code style="">Splitter.on(CharMatcher.BREAKING_WHITESPACE)</code><br style=""><code style="">Splitter.on(CharMatcher.anyOf(";,."))</code> </td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#on(java.lang.String)"><code style="">Splitter.on(String)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Split on a literal&nbsp;<code style="">String</code>.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">Splitter.on(", ")</code></td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"> <a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#on(java.util.regex.Pattern)"><code style="">Splitter.on(Pattern)</code></a><br style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#onPattern(java.lang.String)"><code style="">Splitter.onPattern(String)</code></a> </td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Split on a regular expression.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">Splitter.onPattern("\r?\n")</code></td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#fixedLength(int)"><code style="">Splitter.fixedLength(int)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Splits strings into substrings of the specified fixed length. The last piece can be smaller than&nbsp;<code style="">length</code>, but will never be empty.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">Splitter.fixedLength(3)</code></td> 
   </tr> 
  </tbody> 
 </table> 
 <h4 style=""> <a id="user-content-modifiers" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#modifiers"></a>Modifiers</h4> 
 <table style=""> 
  <thead style="">
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Method</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Description</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Example</th> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#omitEmptyStrings()"><code style="">omitEmptyStrings()</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Automatically omits empty strings from the result.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"> <code style="">Splitter.on(',').omitEmptyStrings().split("a,,c,d")</code>returns&nbsp;<code style="">"a", "c", "d"</code> </td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#trimResults()"><code style="">trimResults()</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Trims whitespace from the results; equivalent to&nbsp;<code style="">trimResults(CharMatcher.WHITESPACE)</code>.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"> <code style="">Splitter.on(',').trimResults().split("a, b, c, d")</code>&nbsp;returns&nbsp;<code style="">"a", "b", "c", "d"</code> </td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#trimResults(com.google.common.base.CharMatcher)"><code style="">trimResults(CharMatcher)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Trims characters matching the specified&nbsp;<code style="">CharMatcher</code>&nbsp;from results.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"> <code style="">Splitter.on(',').trimResults(CharMatcher.is('_')).split("_a ,_b_ ,c__")</code>&nbsp;returns&nbsp;<code style="">"a ", "b_ ", "c"</code>.</td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Splitter.html#limit(int)"><code style="">limit(int)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Stops splitting after the specified number of strings have been returned.</td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"> <code style="">Splitter.on(',').limit(3).split("a,b,c,d")</code>&nbsp;returns&nbsp;<code style="">"a", "b", "c,d"</code> </td> 
   </tr> 
  </tbody> 
 </table> 
 <p style="">TODO: Map splitters</p> 
 <p style="">If you wish to get a&nbsp;<code style="">List</code>, just use&nbsp;<code style="">Lists.newArrayList(splitter.split(string))</code>&nbsp;or the like.</p> 
 <p style=""><span style="font-weight: 600;">Warning:</span>&nbsp;splitter instances are always immutable. The splitter configuration methods will always return a new&nbsp;<code style="">Splitter</code>, which you must use to get the desired semantics. This makes any&nbsp;<code style="">Splitter</code>&nbsp;thread safe, and usable as a&nbsp;<code style="">static final</code>&nbsp;constant.</p> 
 <h2 style=""> <a id="user-content-charmatcher" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#charmatcher"></a>CharMatcher</h2> 
 <p style="">In olden times, our&nbsp;<code style="">StringUtil</code>&nbsp;class grew unchecked, and had many methods like these:</p> 
 <ul style=""> 
  <li style=""><code style="">allAscii</code></li> 
  <li style="margin-top: 0.25em;"><code style="">collapse</code></li> 
  <li style="margin-top: 0.25em;"><code style="">collapseControlChars</code></li> 
  <li style="margin-top: 0.25em;"><code style="">collapseWhitespace</code></li> 
  <li style="margin-top: 0.25em;"><code style="">lastIndexNotOf</code></li> 
  <li style="margin-top: 0.25em;"><code style="">numSharedChars</code></li> 
  <li style="margin-top: 0.25em;"><code style="">removeChars</code></li> 
  <li style="margin-top: 0.25em;"><code style="">removeCrLf</code></li> 
  <li style="margin-top: 0.25em;"><code style="">retainAllChars</code></li> 
  <li style="margin-top: 0.25em;"><code style="">strip</code></li> 
  <li style="margin-top: 0.25em;"><code style="">stripAndCollapse</code></li> 
  <li style="margin-top: 0.25em;"><code style="">stripNonDigits</code></li> 
 </ul> 
 <p style="">They represent a partial cross product of two notions:</p> 
 <ol style=""> 
  <li style="">what constitutes a "matching" character?</li> 
  <li style="margin-top: 0.25em;">what to do with those "matching" characters?</li> 
 </ol> 
 <p style="">To simplify this morass, we developed&nbsp;<code style="">CharMatcher</code>.</p> 
 <p style="">Intuitively, you can think of a&nbsp;<code style="">CharMatcher</code>&nbsp;as representing a particular class of characters, like digits or whitespace. Practically speaking, a&nbsp;<code style="">CharMatcher</code>&nbsp;is just a boolean predicate on characters -- indeed,&nbsp;<code style="">CharMatcher</code>&nbsp;implements&nbsp;<a class="internal present" style="background-color: transparent; color: #0366d6;" href="https://github.com/google/guava/wiki/FunctionalExplained#predicate">Predicate&lt;Character&gt;</a>&nbsp;-- but because it is so common to refer to "all whitespace characters" or "all lowercase letters," Guava provides this specialized syntax and API for characters.</p> 
 <p style="">But the utility of a&nbsp;<code style="">CharMatcher</code>&nbsp;is in the&nbsp;<em style="">operations</em>&nbsp;it lets you perform on occurrences of the specified class of characters: trimming, collapsing, removing, retaining, and much more. An object of type&nbsp;<code style="">CharMatcher</code>&nbsp;represents notion 1: what constitutes a matching character? It then provides many operations answering notion 2: what to do with those matching characters? The result is that API complexity increases linearly for quadratically increasing flexibility and power. Yay!</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-smi" style="color: #24292e;">String</span> noControl <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">CharMatcher</span><span class="pl-k" style="color: #d73a49;">.</span>javaIsoControl()<span class="pl-k" style="color: #d73a49;">.</span>removeFrom(string); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> remove control characters</span>
<span class="pl-smi" style="color: #24292e;">String</span> theDigits <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">CharMatcher</span><span class="pl-k" style="color: #d73a49;">.</span>digit()<span class="pl-k" style="color: #d73a49;">.</span>retainFrom(string); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> only the digits</span>
<span class="pl-smi" style="color: #24292e;">String</span> spaced <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">CharMatcher</span><span class="pl-k" style="color: #d73a49;">.</span>whitespace()<span class="pl-k" style="color: #d73a49;">.</span>trimAndCollapseFrom(string, <span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">'</span> <span class="pl-pds" style="">'</span></span>);
  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> trim whitespace at ends, and replace/collapse whitespace into single spaces</span>
<span class="pl-smi" style="color: #24292e;">String</span> noDigits <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">CharMatcher</span><span class="pl-k" style="color: #d73a49;">.</span>javaDigit()<span class="pl-k" style="color: #d73a49;">.</span>replaceFrom(string, <span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>*<span class="pl-pds" style="">"</span></span>); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> star out all digits</span>
<span class="pl-smi" style="color: #24292e;">String</span> lowerAndDigit <span class="pl-k" style="color: #d73a49;">=</span> <span class="pl-smi" style="color: #24292e;">CharMatcher</span><span class="pl-k" style="color: #d73a49;">.</span>javaDigit()<span class="pl-k" style="color: #d73a49;">.</span>or(<span class="pl-smi" style="color: #24292e;">CharMatcher</span><span class="pl-k" style="color: #d73a49;">.</span>javaLowerCase())<span class="pl-k" style="color: #d73a49;">.</span>retainFrom(string);
  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> eliminate all characters that aren't digits or lowercase</span></pre> 
 </div> 
 <p style=""><span style="font-weight: 600;">Note:</span>&nbsp;<code style="">CharMatcher</code>&nbsp;deals only with&nbsp;<code style="">char</code>&nbsp;values; it does not understand supplementary Unicode code points in the range 0x10000 to 0x10FFFF. Such logical characters are encoded into a&nbsp;<code style="">String</code>&nbsp;using surrogate pairs, and a&nbsp;<code style="">CharMatcher</code>&nbsp;treats these just as two separate characters.</p> 
 <h3 style=""> <a id="user-content-obtaining-charmatchers" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#obtaining-charmatchers"></a>Obtaining CharMatchers</h3> 
 <p style="">Many needs can be satisfied by the provided&nbsp;<code style="">CharMatcher</code>&nbsp;factory methods:</p> 
 <ul style=""> 
  <li style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#any()"><code style="">any()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#none()"><code style="">none()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#whitespace()"><code style="">whitespace()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#breakingWhitespace()"><code style="">breakingWhitespace()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#invisible()"><code style="">invisible()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#digit()"><code style="">digit()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaLetter()"><code style="">javaLetter()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaDigit()"><code style="">javaDigit()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaLetterOrDigit()"><code style="">javaLetterOrDigit()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaIsoControl()"><code style="">javaIsoControl()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaLowerCase()"><code style="">javaLowerCase()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#javaUpperCase()"><code style="">javaUpperCase()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#ascii()"><code style="">ascii()</code></a></li> 
  <li style="margin-top: 0.25em;"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#singleWidth()"><code style="">singleWidth()</code></a></li> 
 </ul> 
 <p style="">Other common ways to obtain a&nbsp;<code style="">CharMatcher</code>&nbsp;include:</p> 
 <table style=""> 
  <thead style="">
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Method</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Description</th> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#anyOf(java.lang.CharSequence)"><code style="">anyOf(CharSequence)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Specify all the characters you wish matched. For example,&nbsp;<code style="">CharMatcher.anyOf("aeiou")</code>&nbsp;matches lowercase English vowels.</td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#is(char)"><code style="">is(char)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Specify exactly one character to match.</td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#inRange(char,%20char)"><code style="">inRange(char, char)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Specify a range of characters to match, e.g.&nbsp;<code style="">CharMatcher.inRange('a', 'z')</code>.</td> 
   </tr> 
  </tbody> 
 </table> 
 <p style="">Additionally,&nbsp;<code style="">CharMatcher</code>&nbsp;has&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#negate()"><code style="">negate()</code></a>,&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#and(com.google.common.base.CharMatcher)"><code style="">and(CharMatcher)</code></a>, and&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#or(com.google.common.base.CharMatcher)"><code style="">or(CharMatcher)</code></a>. These provide simple boolean operations on&nbsp;<code style="">CharMatcher</code>.</p> 
 <h3 style=""> <a id="user-content-using-charmatchers" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#using-charmatchers"></a>Using CharMatchers</h3> 
 <p style=""><code style="">CharMatcher</code>&nbsp;provides a&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#method_summary">wide variety</a>&nbsp;of methods to operate on occurrences of the specified characters in any&nbsp;<code style="">CharSequence</code>. There are more methods provided than we can list here, but some of the most commonly used are:</p> 
 <table style=""> 
  <thead style="">
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Method</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Description</th> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#collapseFrom(java.lang.CharSequence,%20char)"><code style="">collapseFrom(CharSequence, char)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Replace each group of consecutive matched characters with the specified character. For example,&nbsp;<code style="">WHITESPACE.collapseFrom(string, ' ')</code>&nbsp;collapses whitespaces down to a single space.</td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#matchesAllOf(java.lang.CharSequence)"><code style="">matchesAllOf(CharSequence)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Test if this matcher matches all characters in the sequence. For example,&nbsp;<code style="">ASCII.matchesAllOf(string)</code>&nbsp;tests if all characters in the string are ASCII.</td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#removeFrom(java.lang.CharSequence)"><code style="">removeFrom(CharSequence)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Removes matching characters from the sequence.</td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#retainFrom(java.lang.CharSequence)"><code style="">retainFrom(CharSequence)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Removes all non-matching characters from the sequence.</td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#trimFrom(java.lang.CharSequence)"><code style="">trimFrom(CharSequence)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Removes leading and trailing matching characters.</td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CharMatcher.html#replaceFrom(java.lang.CharSequence,%20java.lang.CharSequence)"><code style="">replaceFrom(CharSequence, CharSequence)</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Replace matching characters with a given sequence.</td> 
   </tr> 
  </tbody> 
 </table> 
 <p style="">(Note: all of these methods return a&nbsp;<code style="">String</code>, except for&nbsp;<code style="">matchesAllOf</code>, which returns a&nbsp;<code style="">boolean</code>.)</p> 
 <h2 style=""> <a id="user-content-charsets" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#charsets"></a>Charsets</h2> 
 <p style="">Don't do this:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-k" style="color: #d73a49;">try</span> {
  bytes <span class="pl-k" style="color: #d73a49;">=</span> string<span class="pl-k" style="color: #d73a49;">.</span>getBytes(<span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>UTF-8<span class="pl-pds" style="">"</span></span>);
} <span class="pl-k" style="color: #d73a49;">catch</span> (<span class="pl-smi" style="color: #24292e;">UnsupportedEncodingException</span> e) {
  <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> how can this possibly happen?</span>
  <span class="pl-k" style="color: #d73a49;">throw</span> <span class="pl-k" style="color: #d73a49;">new</span> <span class="pl-smi" style="color: #24292e;">AssertionError</span>(e);
}</pre> 
 </div> 
 <p style="">Do this instead:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre>bytes <span class="pl-k" style="color: #d73a49;">=</span> string<span class="pl-k" style="color: #d73a49;">.</span>getBytes(<span class="pl-smi" style="color: #24292e;">Charsets</span><span class="pl-c1" style="color: #005cc5;"><span class="pl-k" style="color: #d73a49;">.</span>UTF_8</span>);</pre> 
 </div> 
 <p style=""><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Charsets.html"><code style="">Charsets</code></a>&nbsp;provides constant references to the six standard&nbsp;<code style="">Charset</code>&nbsp;implementations guaranteed to be supported by all Java platform implementations. Use them instead of referring to charsets by their names.</p> 
 <p style="">TODO: an explanation of charsets and when to use them</p> 
 <p style="">(Note: If you're using JDK7, you should use the constants in&nbsp;<a style="background-color: transparent; color: #0366d6;" href="http://docs.oracle.com/javase/7/docs/api/java/nio/charset/StandardCharsets.html"><code style="">StandardCharsets</code></a></p> 
 <h2 style=""> <a id="user-content-caseformat" class="anchor" style="" href="https://github.com/google/guava/wiki/StringsExplained#caseformat"></a>CaseFormat</h2> 
 <p style=""><code style="">CaseFormat</code>&nbsp;is a handy little class for converting between ASCII case conventions — like, for example, naming conventions for programming languages. Supported formats include:</p> 
 <table style=""> 
  <thead style="">
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Format</th> 
    <th style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left">Example</th> 
   </tr>
  </thead> 
  <tbody style=""> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CaseFormat.html#LOWER_CAMEL"><code style="">LOWER_CAMEL</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">lowerCamel</code></td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CaseFormat.html#LOWER_HYPHEN"><code style="">LOWER_HYPHEN</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">lower-hyphen</code></td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CaseFormat.html#LOWER_UNDERSCORE"><code style="">LOWER_UNDERSCORE</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">lower_underscore</code></td> 
   </tr> 
   <tr style="background-color: #f6f8fa; border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CaseFormat.html#UPPER_CAMEL"><code style="">UPPER_CAMEL</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">UpperCamel</code></td> 
   </tr> 
   <tr style="border-top: 1px solid #c6cbd1;"> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><a style="background-color: transparent; color: #0366d6;" href="http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/CaseFormat.html#UPPER_UNDERSCORE"><code style="">UPPER_UNDERSCORE</code></a></td> 
    <td style="padding: 6px 13px; border: 1px solid #dfe2e5;" align="left"><code style="">UPPER_UNDERSCORE</code></td> 
   </tr> 
  </tbody> 
 </table> 
 <p style="">Using it is relatively straightforward:</p> 
 <div class="highlight highlight-source-java" style=""> 
  <pre><span class="pl-smi" style="color: #24292e;">CaseFormat</span><span class="pl-c1" style="color: #005cc5;"><span class="pl-k" style="color: #d73a49;">.</span>UPPER_UNDERSCORE</span><span class="pl-k" style="color: #d73a49;">.</span>to(<span class="pl-smi" style="color: #24292e;">CaseFormat</span><span class="pl-c1" style="color: #005cc5;"><span class="pl-k" style="color: #d73a49;">.</span>LOWER_CAMEL</span>, <span class="pl-s" style="color: #032f62;"><span class="pl-pds" style="">"</span>CONSTANT_NAME<span class="pl-pds" style="">"</span></span>)); <span class="pl-c" style="color: #6a737d;"><span class="pl-c" style="">//</span> returns "constantName"</span></pre> 
 </div> 
 <p style="">We find this especially useful, for example, when writing programs that generate other programs.</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>