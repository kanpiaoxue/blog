#PowerMockit常用
###发表时间：2015-11-09
###分类：java,powermockito,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2255799" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2255799</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>文档：&nbsp;<a href="http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html">http://site.mockito.org/mockito/docs/current/org/mockito/Mockito.html</a></p> 
 <p>&nbsp;</p> 
 <p>1、测试 void 方法</p> 
 <pre name="code" class="java">@Autowired
    private JdbcTemplate jdbcTemplate;
    public static final String DELETE_INSTANCE_RELY_BY_TASK = " DELETE FROM tb_instance_rely_rel    "
            + "WHERE task_id=? AND instance_id IN (    SELECT c.instance_id    FROM     "
            + "(SELECT task_id     FROM tb_task    WHERE task_id=?    )a     JOIN    tb_data_version b   "
            + " ON a.task_id =  "
            + " b.task_id     JOIN    tb_instance c    ON b.version_id = c.version_id    WHERE c.state=?    )";


    @Override
    public void deleteInitializedInstanceRelyByTask(long taskId, long upTaskId) {

        final Object[] args = { upTaskId, taskId, InstanceState.INITIALIZED.getValue() };

        LOGGER.debug(Tools.getSqlArgsString(DELETE_INSTANCE_RELY_BY_TASK, args));
        jdbcTemplate.update(DELETE_INSTANCE_RELY_BY_TASK, args);
    }
</pre> 
 <p>&nbsp;</p> 
 <p>测试代码片段：</p> 
 <pre name="code" class="java">  private JdbcTemplate jdbcTemplate;
    private InstanceRelyRelDaoImpl impl;
    private long taskId = 100L;
    private long upTaskId = 101L;

    @Before
    public void before() {
        jdbcTemplate = mock(JdbcTemplate.class);
        impl = new InstanceRelyRelDaoImpl();

        Whitebox.setInternalState(impl, "jdbcTemplate", jdbcTemplate);
    }

    public void testDeleteInitializedInstanceRelyByTask() {
        impl.deleteInitializedInstanceRelyByTask(taskId, upTaskId);
        Object[] args = { upTaskId, taskId, InstanceState.INITIALIZED.getValue() };
        Mockito.verify(jdbcTemplate).update(InstanceRelyRelDaoImpl.DELETE_INSTANCE_RELY_BY_TASK, args);
    }
</pre> 
 <p>&nbsp;</p> 
 <p>2、测试static 静态方法</p> 
 <pre name="code" class="java">import static org.junit.Assert.assertTrue;
import static org.junit.Assert.fail;
import static org.powermock.api.mockito.PowerMockito.mock;
import static org.powermock.api.mockito.PowerMockito.mockStatic;
import static org.powermock.api.mockito.PowerMockito.when;



import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.mockito.Mockito;
import org.powermock.core.classloader.annotations.PrepareForTest;
import org.powermock.modules.junit4.PowerMockRunner;
import org.powermock.reflect.Whitebox;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.PreparedStatementCreator;
import org.springframework.jdbc.support.KeyHolder;

import java.util.Date;

@RunWith(PowerMockRunner.class) // mock静态方法，必须有
@PrepareForTest({ Utils.class }) // mock静态方法，必须有
public class EntitySubscribeFlowDaoImplTest {
    private EntitySubscribeFlowDaoImpl impl;
    private JdbcTemplate jdbcTemplate;

    @Before
    public void before() {
        impl = new EntitySubscribeFlowDaoImpl();
        jdbcTemplate = mock(JdbcTemplate.class);
        Whitebox.setInternalState(impl, "jdbcTemplate", jdbcTemplate);
    }

    /**
     * Test method
     */
    @Test
    public void testAddEntitySubscribeFlow() {
        try {
            impl.addEntitySubscribeFlow(null);
            fail();
        } catch (Exception e) {
            assertTrue(true);
        }
        try {
            EntitySubscribeFlow flow = new EntitySubscribeFlow();
            KeyHolder keyHolder = mock(KeyHolder.class);
            mockStatic(Utils.class); // mock静态方法，必须有
            when(Utils.createKeyHolder()).thenReturn(keyHolder); // mock静态方法，必须有
            when(keyHolder.getKey()).thenReturn(10L);
            long id = impl.addEntitySubscribeFlow(flow);
            Mockito.verify(jdbcTemplate).update(Mockito.any(PreparedStatementCreator.class),
                    Mockito.any(KeyHolder.class));
            System.err.println("================= " + id);
        } catch (Exception e) {
            e.printStackTrace();
            fail();
        }
    }



}
</pre> 
 <p>&nbsp;&nbsp;</p> 
 <p>3、mock 掉方法中的 private 私有方法</p> 
 <p>参考地址：&nbsp;<a href="http://automationrhapsody.com/mock-private-method-call-powermock/">http://automationrhapsody.com/mock-private-method-call-powermock/</a></p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">public class PowerMockDemo {
 
    public Point callPrivateMethod() {
        return privateMethod(new Point(1, 1));
    }
 
    private Point privateMethod(Point point) {
        return new Point(point.getX() + 1, point.getY() + 1);
    }
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;
import org.powermock.api.mockito.PowerMockito;
import org.powermock.core.classloader.annotations.PrepareForTest;
import org.powermock.modules.junit4.PowerMockRunner;
 
import static org.hamcrest.CoreMatchers.is;
import static org.hamcrest.MatcherAssert.assertThat;
import static org.mockito.Matchers.anyObject;
import static org.mockito.Mockito.mock;
 
@RunWith(PowerMockRunner.class)
@PrepareForTest(PowerMockDemo.class)
public class PowerMockDemoTest {
 
    private PowerMockDemo powerMockDemoSpy;
 
    @Before
    public void setUp() {
        powerMockDemoSpy = PowerMockito.spy(new PowerMockDemo());
    }
 
    @Test
    public void testMockPrivateMethod() throws Exception {
        Point mockPoint = mock(Point.class);
 
        PowerMockito.doReturn(mockPoint)
            .when(powerMockDemoSpy, "privateMethod", anyObject());
 
        Point actualMockPoint = powerMockDemoSpy.callPrivateMethod();
 
        assertThat(actualMockPoint, is(mockPoint));
    }
}</pre> 
 <p>&nbsp;或者</p> 
 <pre name="code" class="java">@Test
public void testCompose() {
    Train train = new Train();
    Train trainSpy = Mockito.spy(train);
    //notice different Mockito syntax for spy   
    Mockito.doReturn(TESTING_WAGON_COUNT).when(trainSpy).getWagonsCount();
    Mockito.doNothing().when(trainSpy).addWagon(0);
    // invoke testing method
    int actualWagonCount = trainSpy.compose();
    Assert.assertEquals(actualWagonCount, TESTING_WAGON_COUNT);
    Mockito.verify(trainSpy, Mockito.times(TESTING_WAGON_COUNT))
    .addWagon(0);
}</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;网上找的的一些其他人的例子：</p> 
 <p>参考地址：&nbsp;<a href="http://chenjingbo.iteye.com/blog/1696488">http://chenjingbo.iteye.com/blog/1696488</a></p> 
 <pre name="code" class="java">    @Test  
    public void testCreateMarketingDetail() throws Exception {  
        PowerMockito.doReturn(marketingDetail).when(internalMarketingBuilder,"createMarketingDetail",marketingActivity);  
        Assert.assertTrue(umpDetailManager.createMarketingDetail(marketingActivity).getDetailId() == detailId);  
    }  
  
    @Test(expected = ManagerException.class)  
    public void testCreateMarketingDetail_Exception() throws Exception {  
        PowerMockito.doThrow(new RuntimeException("test")).when(internalMarketingBuilder, "createMarketingDetail", marketingActivity);  
        Assert.assertTrue(umpDetailManager.createMarketingDetail(marketingActivity).getDetailId() == detailId);  
    }  
  
    @Test(expected = ManagerException.class)  
    public void testCreateMarketingDetail_Exception2() throws Exception {  
        umpDetailManager.createMarketingDetail(null);  
    }  
  
    @Test  
    public void testAddMarketingDetail() throws Exception {  
        PowerMockito.doReturn(content).when(internalMarketingBuilder,"build",marketingDetail);  
        PowerMockito.doReturn(prepareResultSupport()).when(marketingActivityTopServiceClient,"addMarketingDetail",activityId,content,sellerId);  
        Assert.assertEquals(umpDetailManager.addMarketingDetail(activityId,marketingDetail,sellerId).getDefaultModel(),detailId);  
    }  
  
    @Test(expected = ManagerException.class)  
    public void testAddMarketingDetail_Exception() throws Exception {  
        PowerMockito.doReturn(content).when(internalMarketingBuilder,"build",marketingDetail);  
        PowerMockito.doThrow(new RuntimeException("test")).when(marketingActivityTopServiceClient,"addMarketingDetail",activityId,content,sellerId);  
        umpDetailManager.addMarketingDetail(activityId,marketingDetail,sellerId);  
    }  
  
    @Test  
    public void testDeleteMarketingDetail() throws Exception {  
        PowerMockito.doReturn(prepareResultSupport2()).when(marketingActivityTopServiceClient,"deleteMarketingDetail",detailId,sellerId);  
        Assert.assertFalse(umpDetailManager.deleteMarketingDetail(detailId,sellerId).isSuccess());  
    }  
  
    @Test(expected = ManagerException.class)  
    public void testDeleteMarketingDetail_Exception() throws Exception {  
        PowerMockito.doThrow(new RuntimeException("test")).when(marketingActivityTopServiceClient,"deleteMarketingDetail",detailId,sellerId);  
        Assert.assertFalse(umpDetailManager.deleteMarketingDetail(detailId,sellerId).isSuccess());  
    }  
  
    @Test  
    public void testUpdateMarketingActivityDetail() throws Exception {  
        PowerMockito.doReturn(content).when(internalMarketingBuilder,"build",marketingDetail);  
        PowerMockito.doReturn(prepareResultSupport2()).when(marketingActivityTopServiceClient,"updateMarketingDetail",detailId,content,sellerId);  
        Assert.assertFalse(umpDetailManager.updateMarketingActivityDetail(detailId,marketingDetail,sellerId).isSuccess());  
    }  
  
    @Test(expected = ManagerException.class)  
    public void testUpdateMarketingActivityDetail_Exception() throws Exception {  
        PowerMockito.doReturn(content).when(internalMarketingBuilder,"build",marketingDetail);  
        PowerMockito.doThrow(new RuntimeException("test")).when(marketingActivityTopServiceClient,"updateMarketingDetail",detailId,content,sellerId);  
        Assert.assertFalse(umpDetailManager.updateMarketingActivityDetail(detailId,marketingDetail,sellerId).isSuccess());  
    }  </pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>