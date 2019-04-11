#SpringMVC使用@ResponseBody输出字符串时遇到的乱码问题及解决办法
###发表时间：2013-07-17
###分类：Spring
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1908400" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1908400</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>来源：&nbsp;<a style="font-size: 12px; line-height: 1.5;" href="http://tchen8.iteye.com/blog/993504">http://tchen8.iteye.com/blog/993504</a></p> 
 <p>来源：&nbsp;<a style="font-size: 12px; line-height: 1.5;" href="http://forum.springsource.org/showthread.php?81858-ResponseBody-and-UTF-8">http://forum.springsource.org/showthread.php?81858-ResponseBody-and-UTF-8</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>我的个人解决办法有2个：</p> 
 <p>1、在spring的MVC的范例里面找到了一个解决的方法，就是在使用&nbsp;@ResponseBody 注释的方法的 @RequestMapping(value="/test/hello",produces="text/plain;charset=UTF-8") 里面添加&nbsp;<span style="line-height: 25.1875px;">produces="text/plain;charset=UTF-8"</span></p> 
 <p><span style="line-height: 25.1875px;">这样就可以输入你想要的编码格式了。不过，没有下面的第2种方法便捷。因为第1个解决方法中，在每次使用到非ISO-8859-1之外的字符编码的时候，都要填写&nbsp;</span><span style="line-height: 25.1875px;">produces="text/plain;charset=UTF-8"。显得很笨拙，很罗嗦。请看下面的更彻底的解决方法。</span></p> 
 <p>2、在自己的src下面创建于spring同package [ org.springframework.http.converter ]的<span style="background-color: #fafafa; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px;">StringHttpMessageConverter 类，重写里面的编码：</span><span class="keyword" style="color: #7f0055; font-weight: bold; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">public</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;</span><span class="keyword" style="color: #7f0055; font-weight: bold; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">static</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;</span><span class="keyword" style="color: #7f0055; font-weight: bold; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">final</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;Charset&nbsp;DEFAULT_CHARSET&nbsp;=&nbsp;Charset.forName(</span><span class="string" style="color: blue; font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">"ISO-8859-1"</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">);&nbsp;</span></p> 
 <p><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">为：&nbsp;</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">public</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">static</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">final</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;Charset&nbsp;DEFAULT_CHARSET&nbsp;=&nbsp;Charset.forName(</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">"UTF-8"</span><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">);&nbsp;</span></p> 
 <p>&nbsp;</p> 
 <p><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">就解决了该问题，也不用进行额外的spring的xml配置。</span></p> 
 <p><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">我修改后的代码如下：</span></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/*
 * Copyright 2002-2013 the original author or authors.
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package org.springframework.http.converter;

import java.io.IOException;
import java.io.UnsupportedEncodingException;
import java.nio.charset.Charset;
import java.util.ArrayList;
import java.util.List;

import org.springframework.http.HttpInputMessage;
import org.springframework.http.HttpOutputMessage;
import org.springframework.http.MediaType;
import org.springframework.util.StreamUtils;

/**
 * Implementation of {@link HttpMessageConverter} that can read and write strings.
 *
 * &lt;p&gt;By default, this converter supports all media types ({@code &amp;#42;&amp;#47;&amp;#42;}),
 * and writes with a {@code Content-Type} of {@code text/plain}. This can be overridden
 * by setting the {@link #setSupportedMediaTypes supportedMediaTypes} property.
 *
 * @author Arjen Poutsma
 * @since 3.0
 */
public class StringHttpMessageConverter extends AbstractHttpMessageConverter&lt;String&gt; {

	//public static final Charset DEFAULT_CHARSET = Charset.forName("ISO-8859-1");
	//overide here
	public static final Charset DEFAULT_CHARSET = Charset.forName("UTF-8");

	private final Charset defaultCharset;

	private final List&lt;Charset&gt; availableCharsets;

	private boolean writeAcceptCharset = true;


	/**
	 * A default constructor that uses {@code "ISO-8859-1"} as the default charset.
	 * @see #StringHttpMessageConverter(Charset)
	 */
	public StringHttpMessageConverter() {
		this(DEFAULT_CHARSET);
	}

	/**
	 * A constructor accepting a default charset to use if the requested content
	 * type does not specify one.
	 */
	public StringHttpMessageConverter(Charset defaultCharset) {
		super(new MediaType("text", "plain", defaultCharset), MediaType.ALL);
		this.defaultCharset = defaultCharset;
		this.availableCharsets = new ArrayList&lt;Charset&gt;(Charset.availableCharsets().values());
	}

	/**
	 * Indicates whether the {@code Accept-Charset} should be written to any outgoing request.
	 * &lt;p&gt;Default is {@code true}.
	 */
	public void setWriteAcceptCharset(boolean writeAcceptCharset) {
		this.writeAcceptCharset = writeAcceptCharset;
	}

	@Override
	public boolean supports(Class&lt;?&gt; clazz) {
		return String.class.equals(clazz);
	}

	@Override
	protected String readInternal(Class&lt;? extends String&gt; clazz, HttpInputMessage inputMessage) throws IOException {
		Charset charset = getContentTypeCharset(inputMessage.getHeaders().getContentType());
		return StreamUtils.copyToString(inputMessage.getBody(), charset);
	}

	@Override
	protected Long getContentLength(String s, MediaType contentType) {
		Charset charset = getContentTypeCharset(contentType);
		try {
			return (long) s.getBytes(charset.name()).length;
		}
		catch (UnsupportedEncodingException ex) {
			// should not occur
			throw new IllegalStateException(ex);
		}
	}

	@Override
	protected void writeInternal(String s, HttpOutputMessage outputMessage) throws IOException {
		if (this.writeAcceptCharset) {
			outputMessage.getHeaders().setAcceptCharset(getAcceptedCharsets());
		}
		Charset charset = getContentTypeCharset(outputMessage.getHeaders().getContentType());
		StreamUtils.copy(s, charset, outputMessage.getBody());
	}

	/**
	 * Return the list of supported {@link Charset}.
	 * &lt;p&gt;By default, returns {@link Charset#availableCharsets()}. Can be overridden in subclasses.
	 * @return the list of accepted charsets
	 */
	protected List&lt;Charset&gt; getAcceptedCharsets() {
		return this.availableCharsets;
	}

	private Charset getContentTypeCharset(MediaType contentType) {
		if (contentType != null &amp;&amp; contentType.getCharSet() != null) {
			return contentType.getCharSet();
		}
		else {
			return this.defaultCharset;
		}
	}
}
</pre> 
 <p><span style="font-family: Monaco, 'DejaVu Sans Mono', 'Bitstream Vera Sans Mono', Consolas, 'Courier New', monospace; font-size: 12px; line-height: 18px; background-color: #fafafa;">&nbsp;</span></p> 
</div>