#Zookeeper Leader选举工具类
###发表时间：2014-08-07
###分类：zookeeper,curator,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2101327" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2101327</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>这是使用apache.org下面开源的<span style="font-size: 1em; line-height: 1.5; font-family: monospace; background-color: #fafafa;">curator框架写的一个Leader选举的工具类。对于&nbsp;</span><span style="font-size: 1em; line-height: 1.5; font-family: monospace; background-color: #fafafa;">curator 的介绍，如下：</span></p> 
 <p><a href="http://curator.apache.org/">http://curator.apache.org/</a></p> 
 <p><img src="http://curator.apache.org/images/ph-quote.png" alt="" width="537" height="87"></p> 
 <p>&nbsp;</p> 
 <p>本程序用到的pom.xml</p> 
 <pre name="code" class="xml">&lt;org.slf4j.version&gt;1.6.6&lt;/org.slf4j.version&gt;
&lt;commons-logging.version&gt;1.1.1&lt;/commons-logging.version&gt;
&lt;log4j.version&gt;1.2.14&lt;/log4j.version&gt;
&lt;guava.version&gt;17.0&lt;/guava.version&gt;
&lt;curator-version&gt;2.6.0&lt;/curator-version&gt;

&lt;!-- curator start --&gt;
&lt;dependency&gt;
	&lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
	&lt;artifactId&gt;curator-recipes&lt;/artifactId&gt;
	&lt;version&gt;${curator-version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
	&lt;groupId&gt;org.apache.curator&lt;/groupId&gt;
	&lt;artifactId&gt;curator-x-discovery&lt;/artifactId&gt;
	&lt;version&gt;${curator-version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;!-- curator end --&gt;

&lt;dependency&gt;
	&lt;groupId&gt;com.google.guava&lt;/groupId&gt;
	&lt;artifactId&gt;guava&lt;/artifactId&gt;
	&lt;version&gt;${guava.version}&lt;/version&gt;
&lt;/dependency&gt;

&lt;dependency&gt;
	&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
	&lt;artifactId&gt;jcl-over-slf4j&lt;/artifactId&gt;
	&lt;version&gt;${org.slf4j.version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
	&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
	&lt;artifactId&gt;slf4j-api&lt;/artifactId&gt;
	&lt;version&gt;${org.slf4j.version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
	&lt;groupId&gt;org.slf4j&lt;/groupId&gt;
	&lt;artifactId&gt;slf4j-log4j12&lt;/artifactId&gt;
	&lt;version&gt;${org.slf4j.version}&lt;/version&gt;
&lt;/dependency&gt;
&lt;dependency&gt;
	&lt;groupId&gt;log4j&lt;/groupId&gt;
	&lt;artifactId&gt;log4j&lt;/artifactId&gt;
	&lt;version&gt;${log4j.version}&lt;/version&gt;
&lt;/dependency&gt;</pre> 
 <p>&nbsp;</p> 
 <p>下面是程序：</p> 
 <pre name="code" class="java">import org.apache.curator.framework.CuratorFramework;
import org.apache.curator.framework.CuratorFrameworkFactory;
import org.apache.curator.framework.recipes.leader.LeaderLatch;
import org.apache.curator.retry.ExponentialBackoffRetry;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.google.common.base.CharMatcher;

import java.util.UUID;

/**
 * &lt;pre&gt;
 * ZKLeaderUtils.java
 * @author kanpiaoxue&lt;br&gt;
 * @version 1.0
 * Create Time 2014年8月7日 下午1:04:18&lt;br&gt;
 * Description : Zookeeper Leader选举工具类
 * &lt;/pre&gt;
 */
public class ZKLeaderUtils {
    private static final Logger LOGGER = LoggerFactory
            .getLogger(ZKLeaderUtils.class);

    private ZKLeaderUtils() {
    }

    /**
     * &lt;pre&gt;
     * @param connectionString  链接Zookeeper Cluster的字符串，如：127.0.0.1:2181,127.0.0.2:2181,127.0.0.3:2181,127.0.0.4:2181,127.0.0.5:2181
     * @param leaderPath    Zookeeper 上面创建挂在Leader选举使用的路径
     * @param sessionTimeoutMs  它是 session 失效的时间，单位：毫秒。这个参数直接影响备选Leader之间切换间隔时间。
     *          如果该时间设置过长，则当前Leader挂掉之后，备选的Leader不能立刻启动，需要等待sessionTimeoutMs这么长的时间才能确定之前的Leader已经死亡，备选Leader才能进行选举。
     *          如果该时间设置过短，当前Leader与ZK集群通信发生闪断，这个闪断的时间大于sessionTimeoutMs的时间，Leader准备在闪断之后进行尝试连接ZK集群。在这个过程中，其他备选的Leader感知到当前Leader
     * 的session已经失效，则进行选举并产生新的Leader。这个时候，就会出现问题：已有的Leader并没有真正的死亡，只不过是与ZK的集群之间发生网络的闪断而已，它的业务依然正常运行中；而现有的备选Leader不知道
     * 原有的Leader并没有真的死亡，从而选举出Leader并接手业务逻辑。会出现多Leader共存的现象。这是致命的问题。所以要设置恰当的 sessionTimeoutMs 时间，来规避这个问题。
     * @param connectionTimeoutMs 链接超时的时间，单位：毫秒
     * @param baseSleepTimeMs   链接断开之后进行重新连接的间隔时间，单位：毫秒
     * @param maxRetries    链接断开之后进行重新连接的最多次数
     * @throws Exception
     * 功能：等待成为Leader
     * 算法：
     *  为每个备选的Leader的ZK节点分配一个唯一ID。该ID由 UUID.randomUUID() 产生。
     *  当本节点不是Leader的时候，本方法会一直阻塞直到本节点成为Leader。
     *  如果ZK中没有 leaderPath 这个路径，本方法不会自动创建这个路径。
     * &lt;/pre&gt;
     */
    public static void waitForLeader(String connectionString,
            String leaderPath, int sessionTimeoutMs, int connectionTimeoutMs,
            int baseSleepTimeMs, int maxRetries) throws Exception {
        String id = CharMatcher.anyOf("-").removeFrom(
                UUID.randomUUID().toString());
        CuratorFramework zkCient = CuratorFrameworkFactory.newClient(
                connectionString, sessionTimeoutMs, connectionTimeoutMs,
                new ExponentialBackoffRetry(baseSleepTimeMs, maxRetries));
        LOGGER.info(String.format("I'm [%s]. start to work", id));
        zkCient.start();
        zkCient.getZookeeperClient().blockUntilConnectedOrTimedOut();

        @SuppressWarnings("resource")
        LeaderLatch leaderLatch = new LeaderLatch(zkCient, leaderPath, id);
        leaderLatch.start();
        LOGGER.info("leaderLatch has startted and is waitting for being leader.");
        LOGGER.info(String.format("I'm [%s]. I think that the leader is %s",
                id, leaderLatch.getLeader()));
        leaderLatch.await();
        LOGGER.info(String.format("I'm [%s]. I'm the leader now! %s", id,
                leaderLatch.getLeader()));
    }

    public static void main(String[] args) throws Exception {

        String connectionString = "127.0.0.1:2181,127.0.0.2:2181,127.0.0.3:2181";
        String leaderPath = "/leader";
        int sessionTimeoutMs = 10 * 1000;
        int connectionTimeoutMs = 10 * 1000;
        int baseSleepTimeMs = 1;
        int maxRetries = 20000;

        waitForLeader(connectionString, leaderPath, sessionTimeoutMs,
                connectionTimeoutMs, baseSleepTimeMs, maxRetries);
        System.out.println("I'm the leader. I can do something here.")
    }

}</pre> 
 <p>&nbsp;</p> 
</div>