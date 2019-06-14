#通过表名文件创建MyBatis的table部分的xml
###发表时间：2019-03-06
###分类：mybatis,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2438518" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2438518</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import com.google.common.base.CaseFormat;

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.stream.Stream;

/**
 * @ClassName: TempXMLTools
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2019/02/15 17:33:25
 *              通过表名文件创建MyBatis的table部分的xml
 */
public class MyBatisXMLTools {

    /**
     *
     * @param args
     * @author kanpiaoxue
     * @CreateTime: 2019/02/15 17:33:25
     */
    public static void main(String[] args) {
        String schema = "hellodb";
        String sqlFile = "/Users/kanpiaoxue/tmp/20190306/hello.sql";
        /**
         * &lt;pre&gt;
         * hello.sql的内容：
         * hello
         * world
         * &lt;/pre&gt;
         */
        try (Stream&lt;String&gt; lines = Files.lines(Paths.get(sqlFile))) {
            lines.map(tb -&gt; {

                String mapperName = createMapperName(tb);
                String domainObjectName = createDomainObjectName(tb);

                StringBuilder builder = new StringBuilder();
                builder.append("&lt;table schema=\"").append(schema).append("\" tableName=\"").append(tb)
                        .append("\" mapperName=\"").append(mapperName).append("\"");
                builder.append(" domainObjectName=\"").append(domainObjectName)
                        .append("\" enableCountByExample=\"false\"");
                builder.append(" enableDeleteByExample=\"false\" enableSelectByExample=\"false\"");
                builder.append(" enableUpdateByExample=\"false\"&gt;");
                builder.append("&lt;property name=\"useActualColumnNames\" value=\"false\" /&gt;");
                builder.append("&lt;/table&gt;");
                return builder.toString();
            }).forEach(System.out::println);
                /**
                 * 输出内容：
                 * &lt;table schema="hellodb" tableName="hello" mapperName="HelloDAO" domainObjectName="Hello" enableCountByExample="false" enableDeleteByExample="false" enableSelectByExample="false" enableUpdateByExample="false"&gt;&lt;property name="useActualColumnNames" value="false" /&gt;&lt;/table&gt;
                 * &lt;table schema="hellodb" tableName="world" mapperName="WorldDAO" domainObjectName="World" enableCountByExample="false" enableDeleteByExample="false" enableSelectByExample="false" enableUpdateByExample="false"&gt;&lt;property name="useActualColumnNames" value="false" /&gt;&lt;/table&gt;
                 */
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    static String createMapperName(String tb) {
        return String.format("%sDAO", createDomainObjectName(tb));
    }

    static String createDomainObjectName(String tb) {
        return CaseFormat.LOWER_UNDERSCORE.to(CaseFormat.UPPER_CAMEL, tb);
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>