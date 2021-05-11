#HBaseUtils（HbaseTemplate）工具类
###发表时间：2020-12-10
###分类：hbase,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2518020" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2518020</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.TableName;
import org.apache.hadoop.hbase.client.Admin;
import org.apache.hadoop.hbase.client.Result;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.data.hadoop.hbase.HbaseTemplate;

import java.io.IOException;
import java.util.Arrays;
import java.util.Objects;

/**
 * hbase工具类
 *
 * @ClassName: HBaseUtils
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2020/11/24 16:18:55
 * @Description:
 */
public class HBaseUtils {
    private static final Logger LOGGER = LoggerFactory.getLogger(HBaseUtils.class);

    public static byte[] getValue(HbaseTemplate hbaseTemplate, String tableName, byte[] columnFamily,
            byte[] column, String rowKey) {
        byte[] rs = hbaseTemplate.get(tableName, rowKey, (Result result, int rowNum) -&gt; {
            byte[] value = result.getValue(columnFamily, column);
            if (Objects.isNull(value)) {
                return null;
            }
            return value;
        });
        return rs;
    }

    public static boolean isExistColumnFamily(Admin admin, TableName tableName, String cf)
            throws IOException {
        HTableDescriptor tableDescriptor = admin.getTableDescriptor(tableName);
        HColumnDescriptor[] descriptors = tableDescriptor.getColumnFamilies();
        return Arrays.stream(descriptors).filter(descriptor -&gt; {
            String name = descriptor.getNameAsString();
            LOGGER.info("tableName:{},columnFamily name:{},cf:{}", tableName, name, cf);
            return name.equals(cf);
        }).findFirst().isPresent();
    }

    public static boolean isExistTable(Admin admin, TableName tableName) throws IOException {
        return admin.tableExists(tableName);
    }

    public static void write(HbaseTemplate hbaseTemplate, String tableName, String columnFamily,
            String column, String rowKey, byte[] value) {
        hbaseTemplate.put(tableName, rowKey, columnFamily, column, value);
    }

    /**
     *
     */
    private HBaseUtils() {
        super();
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>