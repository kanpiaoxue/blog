#springboot使用yml文件配置javabean
###发表时间：2018-11-15
###分类：Spring,springboot,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2433901" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2433901</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">application-dev.yml</p> 
 <pre name="code" class="java">spring:
  application:
    name: cleanHDFSFilesJob-dev

hdfs:
  clean:
    hdfsCleanStrategies:
      - 
        keepDays: 30
        pathPattern: /strategy/hello1/(\d{12})
      - 
        keepDays: 30
        pathPattern: /strategy/hello2/(\d{12})
      - 
        keepDays: 30
        pathPattern: /strategy/hello3/(\d{12})
      - 
        keepDays: 30
        pathPattern: /strategy/hello4/(\d{12})</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public class HDFSCleanStrategy {
    private Integer keepDays;
    private String pathPattern;

    /**
     *
     */
    public HDFSCleanStrategy() {
        super();
    }

    /**
     * @param keepDays
     * @param pathPattern
     */
    public HDFSCleanStrategy(Integer keepDays, String pathPattern) {
        super();
        this.keepDays = keepDays;
        this.pathPattern = pathPattern;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#equals(java.lang.Object)
     */
    @Override
    public boolean equals(Object obj) {
        if (this == obj) {
            return true;
        }
        if (obj == null) {
            return false;
        }
        if (getClass() != obj.getClass()) {
            return false;
        }
        HDFSCleanStrategy other = (HDFSCleanStrategy) obj;
        if (keepDays == null) {
            if (other.keepDays != null) {
                return false;
            }
        } else if (!keepDays.equals(other.keepDays)) {
            return false;
        }
        if (pathPattern == null) {
            if (other.pathPattern != null) {
                return false;
            }
        } else if (!pathPattern.equals(other.pathPattern)) {
            return false;
        }
        return true;
    }

    /**
     * @return the keepDays
     */
    public Integer getKeepDays() {
        return keepDays;
    }

    /**
     * @return the pathPattern
     */
    public String getPathPattern() {
        return pathPattern;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((keepDays == null) ? 0 : keepDays.hashCode());
        result = prime * result + ((pathPattern == null) ? 0 : pathPattern.hashCode());
        return result;
    }

    /**
     * @param keepDays
     *            the keepDays to set
     */
    public void setKeepDays(Integer keepDays) {
        this.keepDays = keepDays;
    }

    /**
     * @param pathPattern
     *            the pathPattern to set
     */
    public void setPathPattern(String pathPattern) {
        this.pathPattern = pathPattern;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return CommonUtils.toJSONString(this);
    }

}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Component
@ConfigurationProperties(prefix = "hdfs.clean")
public class HDFSCleanStrategyConfig {

    private List&lt;HDFSCleanStrategy&gt; hdfsCleanStrategies;

    /**
     * @return the hdfsCleanStrategies
     */
    public List&lt;HDFSCleanStrategy&gt; getHdfsCleanStrategies() {
        return hdfsCleanStrategies;
    }

    /**
     * @param hdfsCleanStrategies
     *            the hdfsCleanStrategies to set
     */
    public void setHdfsCleanStrategies(List&lt;HDFSCleanStrategy&gt; hdfsCleanStrategies) {
        this.hdfsCleanStrategies = hdfsCleanStrategies;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return CommonUtils.toJSONString(this);
    }
}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">@Service
public class CleanHDFSServcieImpl implements CleanHDFSServcie {
    private static final Logger LOGGER = LoggerFactory.getLogger(CleanHDFSServcieImpl.class);

    @Autowired
    private HDFSCleanStrategyConfig hdfsCleanStrategyConfig;

    /*
     * (non-Javadoc)
     * 
     */
    @Override
    @PostConstruct
    public void start() {
        // TODO Auto-generated method stub
        LOGGER.info("start to cleanHDFS:{}", hdfsCleanStrategyConfig);
    }

}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
</div>