#springmvc的路径匹配AntPathMatcher
###发表时间：2019-03-27
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2439436" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2439436</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>springmvc的路径匹配经常使用到通配符。</p> 
 <p>可以做URLs匹配，规则如下</p> 
 <p>？匹配一个字符</p> 
 <p>*匹配0个或多个字符</p> 
 <p>**匹配0个或多个目录</p> 
 <p>我们要是自己要使用spring的这个匹配路径的方法该如何处理呢？使用spring的AntPathMatcher</p> 
 <p>The Spring Framework PathMatcherTests.java source code</p> 
 <pre name="code" class="java">/*
 * Copyright 2002-2007 the original author or authors.
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

package org.springframework.util;

import junit.framework.TestCase;

/**
 * @author Alef Arendsen
 * @author Seth Ladd
 * @author Juergen Hoeller
 */
public class PathMatcherTests extends TestCase {

	public void testAntPathMatcher() {
		PathMatcher pathMatcher = new AntPathMatcher();

		// test exact matching
		assertTrue(pathMatcher.match("test", "test"));
		assertTrue(pathMatcher.match("/test", "/test"));
		assertFalse(pathMatcher.match("/test.jpg", "test.jpg"));
		assertFalse(pathMatcher.match("test", "/test"));
		assertFalse(pathMatcher.match("/test", "test"));

		// test matching with ?'s
		assertTrue(pathMatcher.match("t?st", "test"));
		assertTrue(pathMatcher.match("??st", "test"));
		assertTrue(pathMatcher.match("tes?", "test"));
		assertTrue(pathMatcher.match("te??", "test"));
		assertTrue(pathMatcher.match("?es?", "test"));
		assertFalse(pathMatcher.match("tes?", "tes"));
		assertFalse(pathMatcher.match("tes?", "testt"));
		assertFalse(pathMatcher.match("tes?", "tsst"));

		// test matchin with *'s
		assertTrue(pathMatcher.match("*", "test"));
		assertTrue(pathMatcher.match("test*", "test"));
		assertTrue(pathMatcher.match("test*", "testTest"));
		assertTrue(pathMatcher.match("test/*", "test/Test"));
		assertTrue(pathMatcher.match("test/*", "test/t"));
		assertTrue(pathMatcher.match("test/*", "test/"));
		assertTrue(pathMatcher.match("*test*", "AnothertestTest"));
		assertTrue(pathMatcher.match("*test", "Anothertest"));
		assertTrue(pathMatcher.match("*.*", "test."));
		assertTrue(pathMatcher.match("*.*", "test.test"));
		assertTrue(pathMatcher.match("*.*", "test.test.test"));
		assertTrue(pathMatcher.match("test*aaa", "testblaaaa"));
		assertFalse(pathMatcher.match("test*", "tst"));
		assertFalse(pathMatcher.match("test*", "tsttest"));
		assertFalse(pathMatcher.match("test*", "test/"));
		assertFalse(pathMatcher.match("test*", "test/t"));
		assertFalse(pathMatcher.match("test/*", "test"));
		assertFalse(pathMatcher.match("*test*", "tsttst"));
		assertFalse(pathMatcher.match("*test", "tsttst"));
		assertFalse(pathMatcher.match("*.*", "tsttst"));
		assertFalse(pathMatcher.match("test*aaa", "test"));
		assertFalse(pathMatcher.match("test*aaa", "testblaaab"));

		// test matching with ?'s and /'s
		assertTrue(pathMatcher.match("/?", "/a"));
		assertTrue(pathMatcher.match("/?/a", "/a/a"));
		assertTrue(pathMatcher.match("/a/?", "/a/b"));
		assertTrue(pathMatcher.match("/??/a", "/aa/a"));
		assertTrue(pathMatcher.match("/a/??", "/a/bb"));
		assertTrue(pathMatcher.match("/?", "/a"));

		// test matching with **'s
		assertTrue(pathMatcher.match("/**", "/testing/testing"));
		assertTrue(pathMatcher.match("/*/**", "/testing/testing"));
		assertTrue(pathMatcher.match("/**/*", "/testing/testing"));
		assertTrue(pathMatcher.match("/bla/**/bla", "/bla/testing/testing/bla"));
		assertTrue(pathMatcher.match("/bla/**/bla", "/bla/testing/testing/bla/bla"));
		assertTrue(pathMatcher.match("/**/test", "/bla/bla/test"));
		assertTrue(pathMatcher.match("/bla/**/**/bla", "/bla/bla/bla/bla/bla/bla"));
		assertTrue(pathMatcher.match("/bla*bla/test", "/blaXXXbla/test"));
		assertTrue(pathMatcher.match("/*bla/test", "/XXXbla/test"));
		assertFalse(pathMatcher.match("/bla*bla/test", "/blaXXXbl/test"));
		assertFalse(pathMatcher.match("/*bla/test", "XXXblab/test"));
		assertFalse(pathMatcher.match("/*bla/test", "XXXbl/test"));

		assertFalse(pathMatcher.match("/????", "/bala/bla"));
		assertFalse(pathMatcher.match("/**/*bla", "/bla/bla/bla/bbb"));

		assertTrue(pathMatcher.match("/*bla*/**/bla/**", "/XXXblaXXXX/testing/testing/bla/testing/testing/"));
		assertTrue(pathMatcher.match("/*bla*/**/bla/*", "/XXXblaXXXX/testing/testing/bla/testing"));
		assertTrue(pathMatcher.match("/*bla*/**/bla/**", "/XXXblaXXXX/testing/testing/bla/testing/testing"));
		assertTrue(pathMatcher.match("/*bla*/**/bla/**", "/XXXblaXXXX/testing/testing/bla/testing/testing.jpg"));

		assertTrue(pathMatcher.match("*bla*/**/bla/**", "XXXblaXXXX/testing/testing/bla/testing/testing/"));
		assertTrue(pathMatcher.match("*bla*/**/bla/*", "XXXblaXXXX/testing/testing/bla/testing"));
		assertTrue(pathMatcher.match("*bla*/**/bla/**", "XXXblaXXXX/testing/testing/bla/testing/testing"));
		assertFalse(pathMatcher.match("*bla*/**/bla/*", "XXXblaXXXX/testing/testing/bla/testing/testing"));

		assertFalse(pathMatcher.match("/x/x/**/bla", "/x/x/x/"));

		assertTrue(pathMatcher.match("", ""));
	}

	public void testAntPathMatcherWithMatchStart() {
		PathMatcher pathMatcher = new AntPathMatcher();

		// test exact matching
		assertTrue(pathMatcher.matchStart("test", "test"));
		assertTrue(pathMatcher.matchStart("/test", "/test"));
		assertFalse(pathMatcher.matchStart("/test.jpg", "test.jpg"));
		assertFalse(pathMatcher.matchStart("test", "/test"));
		assertFalse(pathMatcher.matchStart("/test", "test"));

		// test matching with ?'s
		assertTrue(pathMatcher.matchStart("t?st", "test"));
		assertTrue(pathMatcher.matchStart("??st", "test"));
		assertTrue(pathMatcher.matchStart("tes?", "test"));
		assertTrue(pathMatcher.matchStart("te??", "test"));
		assertTrue(pathMatcher.matchStart("?es?", "test"));
		assertFalse(pathMatcher.matchStart("tes?", "tes"));
		assertFalse(pathMatcher.matchStart("tes?", "testt"));
		assertFalse(pathMatcher.matchStart("tes?", "tsst"));

		// test matchin with *'s
		assertTrue(pathMatcher.matchStart("*", "test"));
		assertTrue(pathMatcher.matchStart("test*", "test"));
		assertTrue(pathMatcher.matchStart("test*", "testTest"));
		assertTrue(pathMatcher.matchStart("test/*", "test/Test"));
		assertTrue(pathMatcher.matchStart("test/*", "test/t"));
		assertTrue(pathMatcher.matchStart("test/*", "test/"));
		assertTrue(pathMatcher.matchStart("*test*", "AnothertestTest"));
		assertTrue(pathMatcher.matchStart("*test", "Anothertest"));
		assertTrue(pathMatcher.matchStart("*.*", "test."));
		assertTrue(pathMatcher.matchStart("*.*", "test.test"));
		assertTrue(pathMatcher.matchStart("*.*", "test.test.test"));
		assertTrue(pathMatcher.matchStart("test*aaa", "testblaaaa"));
		assertFalse(pathMatcher.matchStart("test*", "tst"));
		assertFalse(pathMatcher.matchStart("test*", "test/"));
		assertFalse(pathMatcher.matchStart("test*", "tsttest"));
		assertFalse(pathMatcher.matchStart("test*", "test/"));
		assertFalse(pathMatcher.matchStart("test*", "test/t"));
		assertTrue(pathMatcher.matchStart("test/*", "test"));
		assertTrue(pathMatcher.matchStart("test/t*.txt", "test"));
		assertFalse(pathMatcher.matchStart("*test*", "tsttst"));
		assertFalse(pathMatcher.matchStart("*test", "tsttst"));
		assertFalse(pathMatcher.matchStart("*.*", "tsttst"));
		assertFalse(pathMatcher.matchStart("test*aaa", "test"));
		assertFalse(pathMatcher.matchStart("test*aaa", "testblaaab"));

		// test matching with ?'s and /'s
		assertTrue(pathMatcher.matchStart("/?", "/a"));
		assertTrue(pathMatcher.matchStart("/?/a", "/a/a"));
		assertTrue(pathMatcher.matchStart("/a/?", "/a/b"));
		assertTrue(pathMatcher.matchStart("/??/a", "/aa/a"));
		assertTrue(pathMatcher.matchStart("/a/??", "/a/bb"));
		assertTrue(pathMatcher.matchStart("/?", "/a"));

		// test matching with **'s
		assertTrue(pathMatcher.matchStart("/**", "/testing/testing"));
		assertTrue(pathMatcher.matchStart("/*/**", "/testing/testing"));
		assertTrue(pathMatcher.matchStart("/**/*", "/testing/testing"));
		assertTrue(pathMatcher.matchStart("test*/**", "test/"));
		assertTrue(pathMatcher.matchStart("test*/**", "test/t"));
		assertTrue(pathMatcher.matchStart("/bla/**/bla", "/bla/testing/testing/bla"));
		assertTrue(pathMatcher.matchStart("/bla/**/bla", "/bla/testing/testing/bla/bla"));
		assertTrue(pathMatcher.matchStart("/**/test", "/bla/bla/test"));
		assertTrue(pathMatcher.matchStart("/bla/**/**/bla", "/bla/bla/bla/bla/bla/bla"));
		assertTrue(pathMatcher.matchStart("/bla*bla/test", "/blaXXXbla/test"));
		assertTrue(pathMatcher.matchStart("/*bla/test", "/XXXbla/test"));
		assertFalse(pathMatcher.matchStart("/bla*bla/test", "/blaXXXbl/test"));
		assertFalse(pathMatcher.matchStart("/*bla/test", "XXXblab/test"));
		assertFalse(pathMatcher.matchStart("/*bla/test", "XXXbl/test"));

		assertFalse(pathMatcher.matchStart("/????", "/bala/bla"));
		assertTrue(pathMatcher.matchStart("/**/*bla", "/bla/bla/bla/bbb"));

		assertTrue(pathMatcher.matchStart("/*bla*/**/bla/**", "/XXXblaXXXX/testing/testing/bla/testing/testing/"));
		assertTrue(pathMatcher.matchStart("/*bla*/**/bla/*", "/XXXblaXXXX/testing/testing/bla/testing"));
		assertTrue(pathMatcher.matchStart("/*bla*/**/bla/**", "/XXXblaXXXX/testing/testing/bla/testing/testing"));
		assertTrue(pathMatcher.matchStart("/*bla*/**/bla/**", "/XXXblaXXXX/testing/testing/bla/testing/testing.jpg"));

		assertTrue(pathMatcher.matchStart("*bla*/**/bla/**", "XXXblaXXXX/testing/testing/bla/testing/testing/"));
		assertTrue(pathMatcher.matchStart("*bla*/**/bla/*", "XXXblaXXXX/testing/testing/bla/testing"));
		assertTrue(pathMatcher.matchStart("*bla*/**/bla/**", "XXXblaXXXX/testing/testing/bla/testing/testing"));
		assertTrue(pathMatcher.matchStart("*bla*/**/bla/*", "XXXblaXXXX/testing/testing/bla/testing/testing"));

		assertTrue(pathMatcher.matchStart("/x/x/**/bla", "/x/x/x/"));

		assertTrue(pathMatcher.matchStart("", ""));
	}

	public void testAntPathMatcherWithUniqueDeliminator() {
		AntPathMatcher pathMatcher = new AntPathMatcher();
		pathMatcher.setPathSeparator(".");

		// test exact matching
		assertTrue(pathMatcher.match("test", "test"));
		assertTrue(pathMatcher.match(".test", ".test"));
		assertFalse(pathMatcher.match(".test/jpg", "test/jpg"));
		assertFalse(pathMatcher.match("test", ".test"));
		assertFalse(pathMatcher.match(".test", "test"));

		// test matching with ?'s
		assertTrue(pathMatcher.match("t?st", "test"));
		assertTrue(pathMatcher.match("??st", "test"));
		assertTrue(pathMatcher.match("tes?", "test"));
		assertTrue(pathMatcher.match("te??", "test"));
		assertTrue(pathMatcher.match("?es?", "test"));
		assertFalse(pathMatcher.match("tes?", "tes"));
		assertFalse(pathMatcher.match("tes?", "testt"));
		assertFalse(pathMatcher.match("tes?", "tsst"));

		// test matchin with *'s
		assertTrue(pathMatcher.match("*", "test"));
		assertTrue(pathMatcher.match("test*", "test"));
		assertTrue(pathMatcher.match("test*", "testTest"));
		assertTrue(pathMatcher.match("*test*", "AnothertestTest"));
		assertTrue(pathMatcher.match("*test", "Anothertest"));
		assertTrue(pathMatcher.match("*/*", "test/"));
		assertTrue(pathMatcher.match("*/*", "test/test"));
		assertTrue(pathMatcher.match("*/*", "test/test/test"));
		assertTrue(pathMatcher.match("test*aaa", "testblaaaa"));
		assertFalse(pathMatcher.match("test*", "tst"));
		assertFalse(pathMatcher.match("test*", "tsttest"));
		assertFalse(pathMatcher.match("*test*", "tsttst"));
		assertFalse(pathMatcher.match("*test", "tsttst"));
		assertFalse(pathMatcher.match("*/*", "tsttst"));
		assertFalse(pathMatcher.match("test*aaa", "test"));
		assertFalse(pathMatcher.match("test*aaa", "testblaaab"));

		// test matching with ?'s and .'s
		assertTrue(pathMatcher.match(".?", ".a"));
		assertTrue(pathMatcher.match(".?.a", ".a.a"));
		assertTrue(pathMatcher.match(".a.?", ".a.b"));
		assertTrue(pathMatcher.match(".??.a", ".aa.a"));
		assertTrue(pathMatcher.match(".a.??", ".a.bb"));
		assertTrue(pathMatcher.match(".?", ".a"));

		// test matching with **'s
		assertTrue(pathMatcher.match(".**", ".testing.testing"));
		assertTrue(pathMatcher.match(".*.**", ".testing.testing"));
		assertTrue(pathMatcher.match(".**.*", ".testing.testing"));
		assertTrue(pathMatcher.match(".bla.**.bla", ".bla.testing.testing.bla"));
		assertTrue(pathMatcher.match(".bla.**.bla", ".bla.testing.testing.bla.bla"));
		assertTrue(pathMatcher.match(".**.test", ".bla.bla.test"));
		assertTrue(pathMatcher.match(".bla.**.**.bla", ".bla.bla.bla.bla.bla.bla"));
		assertTrue(pathMatcher.match(".bla*bla.test", ".blaXXXbla.test"));
		assertTrue(pathMatcher.match(".*bla.test", ".XXXbla.test"));
		assertFalse(pathMatcher.match(".bla*bla.test", ".blaXXXbl.test"));
		assertFalse(pathMatcher.match(".*bla.test", "XXXblab.test"));
		assertFalse(pathMatcher.match(".*bla.test", "XXXbl.test"));
	}

	public void testAntPathMatcherExtractPathWithinPattern() throws Exception {
		PathMatcher pathMatcher = new AntPathMatcher();

		assertEquals("", pathMatcher.extractPathWithinPattern("/docs/commit.html", "/docs/commit.html"));

		assertEquals("cvs/commit", pathMatcher.extractPathWithinPattern("/docs/*", "/docs/cvs/commit"));
		assertEquals("commit.html", pathMatcher.extractPathWithinPattern("/docs/cvs/*.html", "/docs/cvs/commit.html"));
		assertEquals("cvs/commit", pathMatcher.extractPathWithinPattern("/docs/**", "/docs/cvs/commit"));
		assertEquals("cvs/commit.html", pathMatcher.extractPathWithinPattern("/docs/**/*.html", "/docs/cvs/commit.html"));
		assertEquals("commit.html", pathMatcher.extractPathWithinPattern("/docs/**/*.html", "/docs/commit.html"));
		assertEquals("commit.html", pathMatcher.extractPathWithinPattern("/*.html", "/commit.html"));
		assertEquals("docs/commit.html", pathMatcher.extractPathWithinPattern("/*.html", "/docs/commit.html"));
		assertEquals("/commit.html", pathMatcher.extractPathWithinPattern("*.html", "/commit.html"));
		assertEquals("/docs/commit.html", pathMatcher.extractPathWithinPattern("*.html", "/docs/commit.html"));
		assertEquals("/docs/commit.html", pathMatcher.extractPathWithinPattern("**/*.*", "/docs/commit.html"));
		assertEquals("/docs/commit.html", pathMatcher.extractPathWithinPattern("*", "/docs/commit.html"));

		assertEquals("docs/cvs/commit", pathMatcher.extractPathWithinPattern("/d?cs/*", "/docs/cvs/commit"));
		assertEquals("cvs/commit.html", pathMatcher.extractPathWithinPattern("/docs/c?s/*.html", "/docs/cvs/commit.html"));
		assertEquals("docs/cvs/commit", pathMatcher.extractPathWithinPattern("/d?cs/**", "/docs/cvs/commit"));
		assertEquals("docs/cvs/commit.html", pathMatcher.extractPathWithinPattern("/d?cs/**/*.html", "/docs/cvs/commit.html"));
	}

}</pre> 
 <p>&nbsp;</p> 
 <p>参考：</p> 
 <p>1、<a href="https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/AntPathMatcher.html">https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/util/AntPathMatcher.html</a></p> 
 <p>2、<a href="https://www.jianshu.com/p/34f87d3097f5">https://www.jianshu.com/p/34f87d3097f5</a></p> 
</div>