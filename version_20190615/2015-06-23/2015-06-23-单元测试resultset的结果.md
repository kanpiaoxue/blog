#单元测试resultset的结果
###发表时间：2015-06-23
###分类：junit,mockrunner
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2221430" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2221430</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>写junit单测的时候需要模拟jdbc的resultset。我使用了如下的测试mock类：</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="xml">		
		&lt;mockrunner.version&gt;0.4.1&lt;/mockrunner.version&gt;
		&lt;dependency&gt;
			&lt;groupId&gt;com.mockrunner&lt;/groupId&gt;
			&lt;artifactId&gt;mockrunner&lt;/artifactId&gt;
			&lt;scope&gt;test&lt;/scope&gt;
		&lt;/dependency&gt;
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">MockResultSet rs = new MockResultSet("myMock");

rs.addColumn("columnA", new Integer[]{1});
rs.addColumn("columnB", new String[]{"Column B Value"});
rs.addColumn("columnC", new Double[]{2});

// make sure to move the cursor to the first row
try
{
  rs.next();
}
catch (SQLException sqle)
{
  fail("unable to move resultSet");
}

// process the result set
MyObject obj = processor.processResultSet(rs);

// run your tests using the ResultSet like you normally would
assertEquals(1, obj.getColumnAValue());
assertEquals("Column B Value", obj.getColumnBValue());
assertEquals(2.0d, obj.getColumnCValue());</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>自己写的：</p> 
 <pre name="code" class="java">import org.springframework.jdbc.core.RowMapper;

import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.Date;

/**
 * &lt;pre&gt;
 * TaskInitInfoRowMapper.java
 * @author xuepeng01&lt;br&gt;
 * @version 1.0
 * Create Time 2015年6月4日 下午8:44:27&lt;br&gt;
 * Description : TaskInitInfo的RowMapper类
 * &lt;/pre&gt;
 */
public class TaskInitInfoRowMapper implements RowMapper&lt;TaskInitInfo&gt; {

    /*
     * (non-Javadoc)
     * @see org.springframework.jdbc.core.RowMapper#mapRow(java.sql.ResultSet,
     * int)
     */
    @Override
    public TaskInitInfo mapRow(ResultSet rs, int arg1) throws SQLException {
        TaskInitInfo obj = new TaskInitInfo();
        obj.setId(rs.getLong("id"));
        obj.setTaskId(rs.getLong("task_id"));
        obj.setDay(rs.getString("day"));
        obj.setGmtCreate(new Date(rs.getTimestamp("gmt_create").getTime()));
        obj.setGmtModify(new Date(rs.getTimestamp("gmt_modify").getTime()));
        obj.setMessage(rs.getString("message"));
        obj.setState(rs.getInt("state"));
        obj.setTryTimes(rs.getInt("try_times"));
        return obj;
    }

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">import static org.junit.Assert.assertEquals;
import static org.junit.Assert.fail;

import com.baidu.rigel.dmap.commons.bean.impl.TaskInitInfo;

import org.joda.time.DateTime;
import org.junit.Test;

import com.mockrunner.mock.jdbc.MockResultSet;

import java.sql.SQLException;
import java.sql.Timestamp;

/**
 * &lt;pre&gt;
 * TaskInitInfoRowMapperTest.java
 * @author xuepeng01&lt;br&gt;
 * @version 1.0
 * Create Time 2015年6月23日 下午9:04:19&lt;br&gt;
 * Description : TaskInitInfoRowMapper测试类
 * &lt;/pre&gt;
 */
public class TaskInitInfoRowMapperTest {

    /**
     * Test method for
     * {@link com.baidu.rigel.dmap.business.dao.mapper.TaskInitInfoRowMapper#mapRow(java.sql.ResultSet, int)}
     * .
     */
    @Test
    public void testMapRow() {
        try {
            MockResultSet rs = new MockResultSet("myMock");
            long id = 11L;
            long taskId = 11L;
            String day = "20150623";
            String message = "hello";
            int state = 2;
            int tryTimes = 2;
            rs.addColumn("id", new Long[] { id });
            rs.addColumn("task_id", new Long[] { taskId });
            rs.addColumn("day", new String[] { day });
            long time = DateTime.now().getMillis();
            rs.addColumn("gmt_create",
                    new Timestamp[] { new Timestamp(time) });
            rs.addColumn("gmt_modify", new Timestamp[] { new Timestamp(time) });
            rs.addColumn("message", new String[] { message });
            rs.addColumn("state", new Integer[] { state });
            rs.addColumn("try_times", new Integer[] { tryTimes });
            rs.next();
            
            TaskInitInfoRowMapper obj = new TaskInitInfoRowMapper();
            TaskInitInfo o = obj.mapRow(rs, 1);
            
            assertEquals(id, o.getId().longValue());
            
        } catch (SQLException e) {
            e.printStackTrace();
            fail();
        }
    }

}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>参考：<a href="http://stackoverflow.com/questions/878848/easy-way-to-fill-up-resultset-with-data">&nbsp;http://stackoverflow.com/questions/878848/easy-way-to-fill-up-resultset-with-data</a></p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>