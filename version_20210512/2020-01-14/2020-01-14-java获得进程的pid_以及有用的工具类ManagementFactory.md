#java获得进程的pid、以及有用的工具类ManagementFactory
###发表时间：2020-01-14
###分类：
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2512001" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2512001</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    // 参考来源：org.springframework.boot.system.ApplicationPid.java#getPid()
    public static String getPid() {
        try {
            String jvmName = ManagementFactory.getRuntimeMXBean().getName();
            System.out.println("jvmName : " + jvmName);
            return jvmName.split("@")[0];
        } catch (Throwable ex) {
            ex.printStackTrace();
            return null;
        }
    }</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">    public static void test05() throws Exception {
        System.out.println("pid : " + getPid());

        System.out.println(StringUtils.center("CompilationMXBean", 100, "="));
        CompilationMXBean compilationMXBean = ManagementFactory.getCompilationMXBean();
        System.out.println(compilationMXBean.getName());
        System.out.println(compilationMXBean.getObjectName());
        System.out.println(compilationMXBean.getTotalCompilationTime());

        System.out.println(StringUtils.center("OperatingSystemMXBean", 100, "="));
        OperatingSystemMXBean operatingSystemMXBean = ManagementFactory.getOperatingSystemMXBean();
        System.out.println(operatingSystemMXBean.getObjectName());
        System.out.println(operatingSystemMXBean.getName());
        System.out.println(operatingSystemMXBean.getAvailableProcessors());
        System.out.println(operatingSystemMXBean.getArch());
        System.out.println(operatingSystemMXBean.getSystemLoadAverage());
        System.out.println(operatingSystemMXBean.getVersion());

        System.out.println(StringUtils.center("RuntimeMXBean", 100, "="));
        RuntimeMXBean runtimeMXBean = ManagementFactory.getRuntimeMXBean();
        System.out.println(runtimeMXBean.getObjectName());
        System.out.println(runtimeMXBean.getName());
        System.out.println(runtimeMXBean.getClassPath());
        System.out.println(runtimeMXBean.getUptime());
        System.out.println(runtimeMXBean.getVmName());
        System.out.println(runtimeMXBean.getVmVersion());
        System.out.println(runtimeMXBean.getVmVendor());
        System.out.println(runtimeMXBean.getInputArguments());
        System.out.println(runtimeMXBean.getBootClassPath());
        System.out.println(runtimeMXBean.getManagementSpecVersion());
        System.out.println(runtimeMXBean.getSpecName());
        System.out.println(runtimeMXBean.getSpecVersion());

        System.out.println(StringUtils.center("MemoryMXBean", 100, "="));
        MemoryMXBean memoryMXBean = ManagementFactory.getMemoryMXBean();
        System.out.println(memoryMXBean.getObjectName());
        System.out.println(memoryMXBean.getHeapMemoryUsage());
        System.out.println(memoryMXBean.getNonHeapMemoryUsage());
        System.out.println(memoryMXBean.getObjectPendingFinalizationCount());

        System.out.println(StringUtils.center("ClassLoadingMXBean", 100, "="));
        ClassLoadingMXBean classLoadingMXBean = ManagementFactory.getClassLoadingMXBean();
        System.out.println(classLoadingMXBean.getObjectName());
        System.out.println(classLoadingMXBean.getTotalLoadedClassCount());
        System.out.println(classLoadingMXBean.getUnloadedClassCount());

        System.out.println(StringUtils.center("ThreadMXBean", 100, "="));
        ThreadMXBean threadMXBean = ManagementFactory.getThreadMXBean();
        System.out.println(threadMXBean.getObjectName());
        System.out.println(threadMXBean.getThreadInfo(Thread.currentThread().getId()));
        Arrays.stream(threadMXBean.getAllThreadIds()).forEach(id -&gt; {
            System.out.println(String.format("id:%s, info:%s", id, threadMXBean.getThreadInfo(id)));
        });

        System.out.println(StringUtils.center("JavaVersion", 100, "="));
        String version = System.getProperty("java.version");
        System.out.println("java.version:" + version);
    }</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>