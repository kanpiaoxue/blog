#python的assert断言
###发表时间：2020-05-15
###分类：python,pyassert
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2514148" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2514148</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>举例：</p> 
 <p>assert len(lists) &gt;=3,'列表元素个数小于3'</p> 
 <p>&nbsp;</p> 
 <p>官网的内容如下：</p> 
 <p>&nbsp;</p> 
 <p><span class="section-number">6.3.<span class="Apple-converted-space">&nbsp;</span></span>The<span class="Apple-converted-space">&nbsp;</span><a class="reference internal" style="color: #355f7c;"><code class="xref std std-keyword docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">assert</span></code></a><span class="Apple-converted-space">&nbsp;</span>statement</p> 
 <p id="index-15" style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">Assert statements are a convenient way to insert debugging assertions into a program:</p> 
 <pre><strong id="grammar-token-assert-stmt">assert_stmt</strong> ::=  "assert" <a class="reference internal" style="color: #355f7c;"><code class="xref docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">expression</span></code></a> ["," <a class="reference internal" style="color: #355f7c;"><code class="xref docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">expression</span></code></a>]
</pre> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The simple form,<span class="Apple-converted-space">&nbsp;</span><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">assert</span><span class="Apple-converted-space">&nbsp;</span><span class="pre">expression</span></code>, is equivalent to</p> 
 <div class="highlight-default notranslate" style="font-family: sans-serif; font-size: 16px;"> 
  <div class="highlight" style="background-color: #eeffcc;"> 
   <pre><span class="k" style="color: #007020;">if</span> <span class="n">__debug__</span><span class="p">:</span>
    <span class="k" style="color: #007020;">if</span> <span class="ow" style="color: #007020;">not</span> <span class="n">expression</span><span class="p">:</span> <span class="k" style="color: #007020;">raise</span> <span class="ne" style="color: #007020;">AssertionError</span>
</pre> 
  </div> 
 </div> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">The extended form,<span class="Apple-converted-space">&nbsp;</span><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">assert</span><span class="Apple-converted-space">&nbsp;</span><span class="pre">expression1,</span><span class="Apple-converted-space">&nbsp;</span><span class="pre">expression2</span></code>, is equivalent to</p> 
 <div class="highlight-default notranslate" style="font-family: sans-serif; font-size: 16px;"> 
  <div class="highlight" style="background-color: #eeffcc;"> 
   <pre><span class="k" style="color: #007020;">if</span> <span class="n">__debug__</span><span class="p">:</span>
    <span class="k" style="color: #007020;">if</span> <span class="ow" style="color: #007020;">not</span> <span class="n">expression1</span><span class="p">:</span> <span class="k" style="color: #007020;">raise</span> <span class="ne" style="color: #007020;">AssertionError</span><span class="p">(</span><span class="n">expression2</span><span class="p">)</span>
</pre> 
  </div> 
 </div> 
 <p id="index-16" style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">These equivalences assume that<span class="Apple-converted-space">&nbsp;</span><a class="reference internal" style="color: #355f7c;" title="__debug__"><code class="xref py py-const docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">__debug__</span></code></a><span class="Apple-converted-space">&nbsp;</span>and<span class="Apple-converted-space">&nbsp;</span><a class="reference internal" style="color: #355f7c;" title="exceptions.AssertionError"><code class="xref py py-exc docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">AssertionError</span></code></a><span class="Apple-converted-space">&nbsp;</span>refer to the built-in variables with those names. In the current implementation, the built-in variable<span class="Apple-converted-space">&nbsp;</span><a class="reference internal" style="color: #355f7c;" title="__debug__"><code class="xref py py-const docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">__debug__</span></code></a><span class="Apple-converted-space">&nbsp;</span>is<span class="Apple-converted-space">&nbsp;</span><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">True</span></code><span class="Apple-converted-space">&nbsp;</span>under normal circumstances,<span class="Apple-converted-space">&nbsp;</span><code class="docutils literal notranslate" style="background-color: #ecf0f3; padding: 0px 1px; font-size: 0.95em;"><span class="pre">False</span></code><span class="Apple-converted-space">&nbsp;</span>when optimization is requested (command line option -O). The current code generator emits no code for an assert statement when optimization is requested at compile time. Note that it is unnecessary to include the source code for the expression that failed in the error message; it will be displayed as part of the stack trace.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">Assignments to<span class="Apple-converted-space">&nbsp;</span><a class="reference internal" style="color: #355f7c;" title="__debug__"><code class="xref py py-const docutils literal notranslate" style="background-color: transparent; padding: 0px 1px; font-size: 0.95em; font-weight: bold;"><span class="pre">__debug__</span></code></a><span class="Apple-converted-space">&nbsp;</span>are illegal. The value for the built-in variable is determined when the interpreter starts.</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">&nbsp;</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">&nbsp;</p> 
 <p style="text-align: justify; line-height: 20.8px; font-family: sans-serif; font-size: 16px;">&nbsp;</p> 
</div>