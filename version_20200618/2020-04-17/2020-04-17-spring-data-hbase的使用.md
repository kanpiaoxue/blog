#spring-data-hbase的使用
###发表时间：2020-04-17
###分类：Spring,springboot,java,hbase
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2513691" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2513691</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>maven的配置</p> 
 <pre name="code" class="xml">&lt;!-- hbase start --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.springframework.data&lt;/groupId&gt;
    &lt;artifactId&gt;spring-data-hadoop&lt;/artifactId&gt;
    &lt;version&gt;${spring.hadoop.version}&lt;/version&gt;
    &lt;exclusions&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;org.springframework&lt;/groupId&gt;
            &lt;artifactId&gt;spring-context-support&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
            &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;javax.servlet&lt;/groupId&gt;
            &lt;artifactId&gt;servlet-api&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
            &lt;artifactId&gt;guava&lt;/artifactId&gt;
        &lt;/exclusion&gt;
    &lt;/exclusions&gt;
&lt;/dependency&gt;


&lt;!-- hadoop start --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.apache.hadoop&lt;/groupId&gt;
    &lt;artifactId&gt;hadoop-client&lt;/artifactId&gt;
    &lt;version&gt;${hadoop.version}&lt;/version&gt;
    &lt;scope&gt;compile&lt;/scope&gt;
    &lt;exclusions&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
            &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
            &lt;artifactId&gt;guava&lt;/artifactId&gt;
        &lt;/exclusion&gt;
    &lt;/exclusions&gt;
&lt;/dependency&gt;
&lt;!-- hadoop end --&gt;

&lt;!-- hbase start --&gt;
&lt;dependency&gt;
    &lt;groupId&gt;org.apache.hbase&lt;/groupId&gt;
    &lt;artifactId&gt;hbase-client&lt;/artifactId&gt;
    &lt;version&gt;${hbase.version}&lt;/version&gt;
    &lt;exclusions&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;log4j&lt;/groupId&gt;
            &lt;artifactId&gt;log4j&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;org.slf4j&lt;/groupId&gt;
            &lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;javax.servlet&lt;/groupId&gt;
            &lt;artifactId&gt;servlet-api&lt;/artifactId&gt;
        &lt;/exclusion&gt;
        &lt;!-- &lt;exclusion&gt;
            &lt;groupId&gt;javax.servlet.jsp&lt;/groupId&gt;
            &lt;artifactId&gt;jsp-api&lt;/artifactId&gt;
        &lt;/exclusion&gt; --&gt;
        &lt;exclusion&gt;
            &lt;groupId&gt;com.google.guava&lt;/groupId&gt;
            &lt;artifactId&gt;guava&lt;/artifactId&gt;
        &lt;/exclusion&gt;
    &lt;/exclusions&gt;
&lt;/dependency&gt;

&lt;!-- hbase end --&gt;</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.apache.hadoop.hbase.HBaseConfiguration;
import org.apache.hadoop.hbase.HConstants;
import org.apache.hadoop.hbase.client.Admin;
import org.apache.hadoop.hbase.client.Connection;
import org.apache.hadoop.hbase.client.ConnectionFactory;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.hadoop.hbase.HbaseTemplate;

import java.io.IOException;

/**
 * HbaseTempalteConfig
 *
 * @ClassName: HbaseTempalteConfig
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2020/04/10 14:19:41
 * @Description:
 */
@Configuration
public class HbaseTempalteConfig {
    private static final Logger LOGGER = LoggerFactory.getLogger(HbaseTempalteConfig.class);

    @Value("${hbase.zookeeper.quorum}")
    private String zkQuorum;
    @Value("${hbase.zookeeper.port:2181}")
    private Integer zkPort;
    @Value("${hbase.zookeeper.znode.parent}")
    private String zkZnodeParent;

    @Bean
    public Admin hbaseAdmin(@Autowired org.apache.hadoop.conf.Configuration configuration)
            throws IOException {
        LOGGER.debug("start to hbaseAdmin. zkQuorum:{},zkPort:{},zkZnodeParent:{}", zkQuorum, zkPort,
                zkZnodeParent);
        Connection connection = ConnectionFactory.createConnection(configuration);
        Admin admin = connection.getAdmin();
        return admin;
    }

    @Bean
    public org.apache.hadoop.conf.Configuration hbaseConfiguration() {
        LOGGER.debug("start to hbaseConfiguration. zkQuorum:{},zkPort:{},zkZnodeParent:{}", zkQuorum, zkPort,
                zkZnodeParent);
        org.apache.hadoop.conf.Configuration configuration = HBaseConfiguration.create();
        configuration.set(HConstants.ZOOKEEPER_QUORUM, zkQuorum);
        configuration.set(HConstants.ZOOKEEPER_CLIENT_PORT, String.valueOf(zkPort));
        configuration.set(HConstants.ZOOKEEPER_ZNODE_PARENT, zkZnodeParent);
        configuration.set("log4j.logger.org.apache.hadoop.hbase", "DEBUG");
        // 设置keyvalue.maxsize的大小限制，这里设置500M = 500*1024*1024
        configuration.set("hbase.client.keyvalue.maxsize", "524288000");

        return configuration;
    }

    @Bean
    public HbaseTemplate hbaseTemplate(@Autowired org.apache.hadoop.conf.Configuration configuration) {
        LOGGER.debug("start to hbaseTemplate. zkQuorum:{},zkPort:{},zkZnodeParent:{}", zkQuorum, zkPort,
                zkZnodeParent);
        HbaseTemplate hbaseTemplate = new HbaseTemplate(configuration);

        return hbaseTemplate;
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.apache.commons.io.IOUtils;
import org.apache.hadoop.hbase.HColumnDescriptor;
import org.apache.hadoop.hbase.HTableDescriptor;
import org.apache.hadoop.hbase.TableName;
import org.apache.hadoop.hbase.client.Admin;
import org.apache.hadoop.hbase.client.Result;
import org.apache.hadoop.hbase.util.Bytes;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.data.hadoop.hbase.HbaseTemplate;
import org.springframework.stereotype.Service;

import com.google.common.base.Preconditions;
import com.google.common.io.ByteSource;
import com.google.common.io.Files;

import java.io.File;
import java.io.IOException;
import java.io.InputStream;
import java.util.Objects;

import javax.annotation.PostConstruct;

/**
 * HBase的文件服务实现类
 *
 * @ClassName: HBaseRemoteTargetFileServiceImpl
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2020/04/10 16:12:51
 * @Description:
 */
@Service
public class HBaseRemoteTargetFileServiceImpl implements RemoteTargetFileService {
    private static final Logger LOGGER = LoggerFactory.getLogger(HBaseRemoteTargetFileServiceImpl.class);

    @Autowired
    private Admin admin;
    @Autowired
    private HbaseTemplate hbaseTemplate;

    @Value("${hbase.table.name}")
    private String tableName;
    @Value("${hbase.table.column.family}")
    private String columnFamily;
    @Value("${hbase.table.column.columnName}")
    private String column;

    private byte[] tableNameAsBytes;
    private byte[] columnFamilyAsBytes;
    private byte[] columnAsBytes;

 
    @Override
    public InputStream getFile(String key) throws Exception {
        LOGGER.info("start to getFile. key:{}", key);
        key = CommonUtils.checkStringArgs(key, "key");
        InputStream input = hbaseTemplate.get(tableName, key, (Result result, int rowNum) -&gt; {
            byte[] value = result.getValue(columnFamilyAsBytes, columnAsBytes);
            if (Objects.isNull(value)) {
                return null;
            }
            InputStream targetStream = ByteSource.wrap(value).openStream();
            return targetStream;
        });

        CommonUtils.checkDataExist(input,
                String.format(
                        "can not find data with tableName:%s,columnFamily:%s,column:%s,key:%s from hbase",
                        tableName, columnFamily, column, key));

        return input;
    }

    @PostConstruct
    public void initialize() throws Exception {
        LOGGER.info("start to initialize. tableName:{},columnFamily:{},column:{},admin:{},hbaseTemplate:{}",
                tableName, columnFamily, column, admin, hbaseTemplate);
        Preconditions.checkNotNull(admin, "admin is null");
        Preconditions.checkNotNull(hbaseTemplate, "hbaseTemplate is null");
        initTableInfo();
        initTable();
        LOGGER.info("finish initializing. tableName:{},columnFamily:{},column:{},admin:{},hbaseTemplate:{}",
                tableName, columnFamily, column, admin, hbaseTemplate);
    }


    @Override
    public void saveFile(String key, File file) throws Exception {
        LOGGER.info("start to saveFile. key:{},file:{}", key, file);
        CommonUtils.checkStringArgs(key, "key");
        Preconditions.checkNotNull(file, "file is null");
        Preconditions.checkArgument(file.exists(), "file:%s does not exist.", file);
        Preconditions.checkArgument(file.isFile(), "file:%s is not a valid file.", file);
        try (InputStream input = Files.asByteSource(file).openStream()) {
            byte[] value = IOUtils.toByteArray(input);
            hbaseTemplate.put(tableName, key, columnFamily, column, value);
        }
    }

    private void initTable() throws IOException {
        LOGGER.info("start to initializeTable.");
        TableName tableName = TableName.valueOf(tableNameAsBytes);
        if (!admin.tableExists(tableName)) {
            LOGGER.info("tableName:{} does not exist. create it.", tableName);
            HTableDescriptor tableDescriptor = new HTableDescriptor(tableName);
            HColumnDescriptor columnDescriptor = new HColumnDescriptor(columnFamily);
            tableDescriptor.addFamily(columnDescriptor);
            admin.createTable(tableDescriptor);
        }
    }

    private void initTableInfo() {
        LOGGER.info("start to initTableInfo.");
        tableName = CommonUtils.checkStringArgs(tableName, "tableName");
        columnFamily = CommonUtils.checkStringArgs(columnFamily, "columnFamily");
        column = CommonUtils.checkStringArgs(column, "column");

        tableNameAsBytes = Bytes.toBytes(tableName);
        columnFamilyAsBytes = Bytes.toBytes(columnFamily);
        columnAsBytes = Bytes.toBytes(column);
    }

}</pre> 
 <p>&nbsp;</p> 
 <p>参考文档：</p> 
 <p>1、<a href="https://www.baeldung.com/hbase">https://www.baeldung.com/hbase</a></p> 
 <p>2、<a href="https://www.jianshu.com/p/c04993cf85ac">https://www.jianshu.com/p/c04993cf85ac</a></p> 
 <p>3、<a href="https://docs.spring.io/spring-hadoop/docs/1.0.0.RELEASE/reference/html/hbase.html">https://docs.spring.io/spring-hadoop/docs/1.0.0.RELEASE/reference/html/hbase.html</a>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>