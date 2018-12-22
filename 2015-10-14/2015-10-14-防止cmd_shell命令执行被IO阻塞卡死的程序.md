#防止cmd/shell命令执行被IO阻塞卡死的程序
###发表时间：2015-10-14
###分类：经验,shell,Linux,非技术
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2249203" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2249203</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.util;

import org.apache.commons.io.IOUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.common.base.Preconditions;
import com.google.common.base.Strings;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

/**
 * &lt;pre&gt;
 * StreamGobbler.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年9月11日 上午10:54:38&lt;br&gt;
 * Description : 外部数据流消费器
 * &lt;/pre&gt;
 */
public final class StreamGobbler extends Thread {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(StreamGobbler.class);

    private static final String ERROR_MSG = "error";
    private final InputStream is;
    /**
     * &lt;pre&gt;
     * 是否需要打印错误log
     * &lt;/pre&gt;
     */
    private final boolean printErrorLog;

    /**
     * &lt;pre&gt;
     * @param is 输入流
     * @param type 类型
     * &lt;/pre&gt;
     */
    public StreamGobbler(InputStream is, String type) {
        super();
        Preconditions.checkNotNull(is, "InputStream is null.");
        Preconditions.checkArgument(!Strings.isNullOrEmpty(type),
                "type is null or empty!");
        this.is = is;
        this.printErrorLog = type.trim()
                .equalsIgnoreCase(ERROR_MSG);
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Thread#run()
     */
    @Override
    public void run() {
        BufferedReader reader = new BufferedReader(new InputStreamReader(is));
        try {
            for (String line = reader.readLine(); line != null; line = reader
                    .readLine()) {
                // 根据标识位打印出不同的log格式
                if (printErrorLog) {
                    LOGGER.debug("{}&gt;{}", ERROR_MSG, line);
                } else {
                    LOGGER.debug(line);
                }
            }
        } catch (IOException e) {
            LOGGER.error(e.getMessage(), e);
        } finally {
            IOUtils.closeQuietly(reader);
        }
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;举例如下：下面的代码不完整</p> 
 <pre name="code" class="java">String msg = String.format("execute cmd:%s", cmd);
                LOGGER.info(msg);
                Stopwatch w = Stopwatch.createStarted();
                Process process = Runtime.getRuntime().exec(cmd);
                // 消费掉IO流，防止程序被阻塞卡死
                new StreamGobbler(process.getInputStream(), "normal").start();
                new StreamGobbler(process.getErrorStream(), "error").start();

                int exitCode = process.waitFor();
                boolean flag = (0 == exitCode);
                LOGGER.info("{}. exitCode : {}, --&gt;{}! It consumes {}", msg, exitCode, (flag ? "SUCCESS"
                        : "FAILURE"), w.toString());</pre> 
 <p>&nbsp;</p> 
</div>