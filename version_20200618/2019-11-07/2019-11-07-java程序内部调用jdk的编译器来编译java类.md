#java程序内部调用jdk的编译器来编译java类
###发表时间：2019-11-07
###分类：java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2509690" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2509690</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>编译java类，一般会用java自带的javac，或者采用其他的编译器。使用javac的时候会比较耗时。其实jdk自身就带有编译器的功能类：javax.tools.<span style="font-family: 'Courier New'; font-size: 18px;">JavaCompiler.java。使用它可以在代码中直接编译java类。</span></p> 
 <p><span style="font-family: 'Courier New'; font-size: 18px;">它的javadoc写的非常清晰：</span></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p style="">nterface to invoke Java™ programming language compilers from programs.</p> 
 <p style="">The compiler might generate diagnostics during compilation (for example, error messages). If a diagnostic listener is provided, the diagnostics will be supplied to the listener. If no listener is provided, the diagnostics will be formatted in an unspecified format and written to the default output, which is<span class="Apple-converted-space">&nbsp;</span><code>System.err</code><span class="Apple-converted-space">&nbsp;</span>unless otherwise specified. Even if a diagnostic listener is supplied, some diagnostics might not fit in a<span class="Apple-converted-space">&nbsp;</span><code>Diagnostic</code><span class="Apple-converted-space">&nbsp;</span>and will be written to the default output.</p> 
 <p style="">A compiler tool has an associated standard file manager, which is the file manager that is native to the tool (or built-in). The standard file manager can be obtained by calling<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">getStandardFileManager</a>.</p> 
 <p style="">A compiler tool must function with any file manager as long as any additional requirements as detailed in the methods below are met. If no file manager is provided, the compiler tool will use a standard file manager such as the one returned by<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">getStandardFileManager</a>.</p> 
 <p style="">An instance implementing this interface must conform to<span class="Apple-converted-space">&nbsp;</span><cite>The Java™ Language Specification</cite><span class="Apple-converted-space">&nbsp;</span>and generate class files conforming to<span class="Apple-converted-space">&nbsp;</span><cite>The Java™ Virtual Machine Specification</cite>. The versions of these specifications are defined in the<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">Tool</a><span class="Apple-converted-space">&nbsp;</span>interface. Additionally, an instance of this interface supporting<span class="Apple-converted-space">&nbsp;</span><code><a style="color: #0068da;">SourceVersion.RELEASE_6</a></code><span class="Apple-converted-space">&nbsp;</span>or higher must also support<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">annotation processing</a>.</p> 
 <p style="">The compiler relies on two services:<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">diagnostic listener</a><span class="Apple-converted-space">&nbsp;</span>and<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">file manager</a>. Although most classes and interfaces in this package defines an API for compilers (and tools in general) the interfaces<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">DiagnosticListener</a>,<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">JavaFileManager</a>,<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">FileObject</a>, and<span class="Apple-converted-space">&nbsp;</span><a style="color: #0068da;">JavaFileObject</a><span class="Apple-converted-space">&nbsp;</span>are not intended to be used in applications. Instead these interfaces are intended to be implemented and used to provide customized services for a compiler and thus defines an SPI for compilers.</p> 
 <p style="">There are a number of classes and interfaces in this package which are designed to ease the implementation of the SPI to customize the behavior of a compiler:</p> 
 <dl style=""> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;">
   <code><a style="color: #0068da;">StandardJavaFileManager</a></code>
  </dt> 
  <dd style="font-size: 1em;">
   Every compiler which implements this interface provides a standard file manager for operating on regular
   <span class="Apple-converted-space">&nbsp;</span>
   <a style="color: #0068da;">files</a>. The StandardJavaFileManager interface defines additional methods for creating file objects from regular files. 
   <p style="font-size: 1em; margin-top: 1em; margin-bottom: 1em;">The standard file manager serves two purposes:</p> 
   <ul style="font-size: 1em; margin-bottom: 1em; margin-left: 1em; padding-left: 1em;"> 
    <li style="font-size: 1em; margin-bottom: 0px;">basic building block for customizing how a compiler reads and writes files</li> 
    <li style="font-size: 1em; margin-bottom: 0px;">sharing between multiple compilation tasks</li> 
   </ul> 
   <p style="font-size: 1em; margin-top: 1em; margin-bottom: 1em;">Reusing a file manager can potentially reduce overhead of scanning the file system and reading jar files. Although there might be no reduction in overhead, a standard file manager must work with multiple sequential compilations making the following example a recommended coding pattern:</p> 
   <pre>       File[] files1 = ... ; // input for first compilation task
       File[] files2 = ... ; // input for second compilation task

       JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();
       StandardJavaFileManager fileManager = compiler.getStandardFileManager(null, null, null);

       <code>Iterable&lt;? extends JavaFileObject&gt;</code> compilationUnits1 =
           fileManager.getJavaFileObjectsFromFiles(<a style="color: #0068da;">Arrays.asList</a>(files1));
       compiler.getTask(null, fileManager, null, null, null, compilationUnits1).call();

       <code>Iterable&lt;? extends JavaFileObject&gt;</code> compilationUnits2 =
           fileManager.getJavaFileObjects(files2); // use alternative method
       // reuse the same file manager to allow caching of jar files
       compiler.getTask(null, fileManager, null, null, null, compilationUnits2).call();

       fileManager.close();</pre> 
  </dd> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;">
   <code><a style="color: #0068da;">DiagnosticCollector</a></code>
  </dt> 
  <dd style="font-size: 1em;">
   Used to collect diagnostics in a list, for example: 
   <pre>       <code>Iterable&lt;? extends JavaFileObject&gt;</code> compilationUnits = ...;
       JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();
       <code>DiagnosticCollector&lt;JavaFileObject&gt; diagnostics = new DiagnosticCollector&lt;JavaFileObject&gt;();</code>
       StandardJavaFileManager fileManager = compiler.getStandardFileManager(diagnostics, null, null);
       compiler.getTask(null, fileManager, diagnostics, null, null, compilationUnits).call();

       for (<code>Diagnostic&lt;? extends JavaFileObject&gt;</code> diagnostic : diagnostics.getDiagnostics())
           System.out.format("Error on line %d in %s%n",
                             diagnostic.getLineNumber(),
                             diagnostic.getSource().toUri());

       fileManager.close();</pre> 
  </dd> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;"> 
   <code><a style="color: #0068da;">ForwardingJavaFileManager</a></code>,
   <span class="Apple-converted-space">&nbsp;</span>
   <code><a style="color: #0068da;">ForwardingFileObject</a></code>, and
   <span class="Apple-converted-space">&nbsp;</span>
   <code><a style="color: #0068da;">ForwardingJavaFileObject</a></code> 
  </dt> 
  <dd style="font-size: 1em;">
   Subclassing is not available for overriding the behavior of a standard file manager as it is created by calling a method on a compiler, not by invoking a constructor. Instead forwarding (or delegation) should be used. These classes makes it easy to forward most calls to a given file manager or file object while allowing customizing behavior. For example, consider how to log all calls to
   <span class="Apple-converted-space">&nbsp;</span>
   <a style="color: #0068da;">JavaFileManager.flush</a>: 
   <pre>       final <a style="color: #0068da;">Logger</a> logger = ...;
       <code>Iterable&lt;? extends JavaFileObject&gt;</code> compilationUnits = ...;
       JavaCompiler compiler = ToolProvider.getSystemJavaCompiler();
       StandardJavaFileManager stdFileManager = compiler.getStandardFileManager(null, null, null);
       JavaFileManager fileManager = new ForwardingJavaFileManager(stdFileManager) {
           public void flush() throws IOException {
               logger.entering(StandardJavaFileManager.class.getName(), "flush");
               super.flush();
               logger.exiting(StandardJavaFileManager.class.getName(), "flush");
           }
       };
       compiler.getTask(null, fileManager, null, null, null, compilationUnits).call();</pre> 
  </dd> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;">
   <code><a style="color: #0068da;">SimpleJavaFileObject</a></code>
  </dt> 
  <dd style="font-size: 1em;">
   This class provides a basic file object implementation which can be used as building block for creating file objects. For example, here is how to define a file object which represent source code stored in a string: 
   <pre>       /**
        * A file object used to represent source coming from a string.
        <code>*</code>/
       public class JavaSourceFromString extends SimpleJavaFileObject {
           /**
            * The source code of this "file".
            <code>*</code>/
           final String code;

           /**
            * Constructs a new JavaSourceFromString.
            * <code>@</code>param name the name of the compilation unit represented by this file object
            * <code>@</code>param code the source code for the compilation unit represented by this file object
            <code>*</code>/
           JavaSourceFromString(String name, String code) {
               super(<a style="color: #0068da;">URI.create</a>("string:///" + name.replace('.','/') + Kind.SOURCE.extension),
                     Kind.SOURCE);
               this.code = code;
           }

           <code>@</code>Override
           public CharSequence getCharContent(boolean ignoreEncodingErrors) {
               return code;
           }
       }</pre> 
  </dd> 
 </dl> 
 <dl style=""> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;">
   Since:
  </dt> 
  <dd style="font-size: 1em;">
   1.6
  </dd> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;">
   Author:
  </dt> 
  <dd style="font-size: 1em;">
   Peter von der Ahé
  </dd> 
  <dd style="font-size: 1em;">
   Jonathan Gibbons
  </dd> 
  <dt style="font-size: 1em; margin-top: 0px; margin-bottom: 0px; font-weight: bold;">
   See Also:
  </dt> 
  <dd style="font-size: 1em;">
   <a style="color: #0068da;">DiagnosticListener</a>
  </dd> 
  <dd style="font-size: 1em;">
   <a style="color: #0068da;">Diagnostic</a>
  </dd> 
  <dd style="font-size: 1em;">
   <a style="color: #0068da;">JavaFileManager</a>
  </dd> 
 </dl> 
</div>