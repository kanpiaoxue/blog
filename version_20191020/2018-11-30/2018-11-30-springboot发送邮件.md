#springboot发送邮件
###发表时间：2018-11-30
###分类：Spring,springboot,java,mail
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2434564" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2434564</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>参考资料：</p> 
 <p><a href="https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-email.html">https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-email.html</a></p> 
 <p><a href="https://docs.spring.io/spring/docs/5.0.11.RELEASE/spring-framework-reference/integration.html#mail">https://docs.spring.io/spring/docs/5.0.11.RELEASE/spring-framework-reference/integration.html#mail</a></p> 
 <p><a href="http://www.ityouknow.com/springboot/2017/05/06/springboot-mail.html">http://www.ityouknow.com/springboot/2017/05/06/springboot-mail.html</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import java.util.Collection;

import javax.mail.MessagingException;

/**
 * @ClassName: MailService
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2018/11/30 11:39:16
 * @Description: 邮件服务类接口
 */
public interface MailService {
    /**
     *
     * @param to
     *            邮件接收人列表，如：hello@163.com
     * @param subject
     *            邮件标题
     * @param content
     *            邮件内容。支持HTML
     * @param filePath
     *            附件地址列表
     * @throws MessagingException
     * @author kanpiaoxue
     * @CreateTime: 2018/11/30 14:21:10
     * @Description: 发送带有附件的邮件
     */
    void sendAttachmentsMail(Collection&lt;String&gt; to, String subject, String content,
            Collection&lt;String&gt; filePaths) throws MessagingException;

    /**
     *
     * @param to
     *            邮件接收人列表，如：hello@163.com
     * @param subject
     *            邮件标题
     * @param content
     *            邮件内容。支持HTML
     * @throws MessagingException
     * @author kanpiaoxue
     * @CreateTime: 2018/11/30 14:21:08
     * @Description: 发送邮件
     */
    void sendEmail(Collection&lt;String&gt; to, String subject, String content) throws MessagingException;
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.apache.commons.collections.CollectionUtils;
import org.apache.commons.lang3.StringUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.core.io.FileSystemResource;
import org.springframework.mail.javamail.JavaMailSender;
import org.springframework.mail.javamail.MimeMessageHelper;
import org.springframework.stereotype.Service;

import com.google.common.base.Stopwatch;

import java.io.File;
import java.util.Collection;

import javax.mail.MessagingException;
import javax.mail.internet.MimeMessage;

/**
 * @ClassName: MailServiceImpl
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2018/11/30 11:41:02
 * @Description: 邮件服务实现类
 */
@Service
public class MailServiceImpl implements MailService {
    private static final Logger LOGGER = LoggerFactory.getLogger(MailServiceImpl.class);
    @Value("${email.from:hello@163.com}")
    private String from;
    @Autowired
    private JavaMailSender mailSender;


    @Override
    public void sendAttachmentsMail(Collection&lt;String&gt; to, String subject, String content,
            Collection&lt;String&gt; filePaths) throws MessagingException {
        LOGGER.info("start to sendAttachmentsMail. to:{},subject:{},content:{},filePaths:{}", to, subject,
                content, filePaths);
        sendAttachmentsMail(to.toArray(new String[] {}), subject, content, filePaths);
    }


    @Override
    public void sendEmail(Collection&lt;String&gt; to, String subject, String content) throws MessagingException {
        LOGGER.info("start to sendEmail. to:{},subject:{},content:{}", to, subject, content);
        sendAttachmentsMail(to.toArray(new String[] {}), subject, content, null);
    }

    private void sendAttachmentsMail(String[] to, String subject, String content,
            Collection&lt;String&gt; filePaths) throws MessagingException {
        Stopwatch sw = Stopwatch.createStarted();
        MimeMessage message = mailSender.createMimeMessage();
        MimeMessageHelper helper = new MimeMessageHelper(message, true);
        helper.setFrom(from);
        helper.setTo(to);
        helper.setSubject(StringUtils.isNotBlank(subject) ? subject.trim() : subject);
        helper.setText(StringUtils.isNotBlank(content) ? content.trim() : content, true);

        if (CollectionUtils.isNotEmpty(filePaths)) {
            for (String filePath : filePaths) {
                FileSystemResource file = new FileSystemResource(new File(filePath.trim()));
                String fileName = filePath.substring(filePath.lastIndexOf(File.separator));
                helper.addAttachment(fileName, file);
            }
        }
        mailSender.send(message);
        LOGGER.info("finsih sendAttachmentsMail. to:{},subject:{},content:{},filePaths:{}. it consumes {}",
                to, subject, content, filePaths, sw);
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>application.yml</p> 
 <pre name="code" class="java">spring:
  mail:
    protocol: smtp
    host: smtp.163.com
    port: 25
    username: hello@163.com
    password: 163.pwd
    default-encoding: UTF-8
    properties:
      mail:
        smtp:
          connectiontimeout: 5000
          timeout: 5000
          writetimeout: 10000
email:
  from: hello@163.com    </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>