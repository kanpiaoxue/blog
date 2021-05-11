#java判断是否Linux操作系统，判断OS操作系统类型工具类
###发表时间：2014-09-18
###分类：经验,java,Linux,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2117714" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2117714</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java"> /**
     * &lt;pre&gt;
     * @return 是否Linux操作系统
     * &lt;/pre&gt;
     */
    public static boolean isLinux() {
        return !System.getProperty("os.name").toLowerCase()
                .startsWith("windows");
    }</pre> 
 <p>&nbsp;上面代码的前提是该java程序只运行在Windows和Linux系统上面才是正确的。如果运行在Mac系统，那么就是有问题的。下面给出一个更加完整和全面的代码。具体用法参看里面的main函数</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">/**
 * &lt;pre&gt;
 * OS操作系统的工具类
 * @author kanpiaoxue
 * 2015-05-05
 * &lt;/pre&gt;
 */
public class OSUtils {
	public enum OSType {
		OS_TYPE_LINUX, OS_TYPE_WIN, OS_TYPE_SOLARIS, OS_TYPE_MAC, OS_TYPE_FREEBSD, OS_TYPE_OTHER
	}

	static private OSType getOSType() {
		String osName = System.getProperty("os.name");
		if (osName.startsWith("Windows")) {
			return OSType.OS_TYPE_WIN;
		} else if (osName.contains("SunOS") || osName.contains("Solaris")) {
			return OSType.OS_TYPE_SOLARIS;
		} else if (osName.contains("Mac")) {
			return OSType.OS_TYPE_MAC;
		} else if (osName.contains("FreeBSD")) {
			return OSType.OS_TYPE_FREEBSD;
		} else if (osName.startsWith("Linux")) {
			return OSType.OS_TYPE_LINUX;
		} else {
			// Some other form of Unix
			return OSType.OS_TYPE_OTHER;
		}
	}

	public static final OSType osType = getOSType();
	// Helper static vars for each platform
	public static final boolean WINDOWS = (osType == OSType.OS_TYPE_WIN);
	public static final boolean SOLARIS = (osType == OSType.OS_TYPE_SOLARIS);
	public static final boolean MAC = (osType == OSType.OS_TYPE_MAC);
	public static final boolean FREEBSD = (osType == OSType.OS_TYPE_FREEBSD);
	public static final boolean LINUX = (osType == OSType.OS_TYPE_LINUX);
	public static final boolean OTHER = (osType == OSType.OS_TYPE_OTHER);

	/*public static void main(String[] args) {
		System.out.println(OSUtils.WINDOWS);
		System.out.println(OSUtils.LINUX);
		System.out.println(OSUtils.MAC);
		System.out.println("OSUtils.main()");
	}*/
}</pre> 
 <p>&nbsp;</p> 
</div>