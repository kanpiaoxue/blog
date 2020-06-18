#Ext ComboBox
###发表时间：2013-12-19
###分类：Ext,javascript
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1992269" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1992269</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">// 一个简单的Array数组的Combo
var store = new Ext.data.ArrayStore({
       fields: ['key','value'],
       data : [[1,'饼状图'],[2,'折线图']]
 });
 
var combo = new Ext.form.ComboBox({
       store: store,
       valueField:'key',
       displayField:'value',
       typeAhead: true,
       mode: 'local',
       forceSelection: true,
       triggerAction: 'all',
       emptyText:'选择图形...',
       selectOnFocus:true,
       editable : false// 不允许编辑
});
   
var win = new Ext.Window(
		{
			title : '图形选择', 
			id : 'graphWindow',
			layout : 'fit',
			width : 200,
			height : 150,
			closable : true,
			resizable : false,
			draggable : false,
			plain : false,
			border : false,
			frame : true,
			modal : true,
			bodyStyle : 'padding:20 20 20 20 ',
			items : [ combo]
		});
win.show();</pre> 
 <p>&nbsp;</p> 
 <p>下面给出一个带有分页，读取后台数据的ComboBox的代码。</p> 
 <pre name="code" class="java">--- ComboBox  的后台JavaBean
public final class KeyValue&lt;K, V&gt; {
	private K key;
	private V value;

	public KeyValue(K key, V value) {
		super();
		this.key = key;
		this.value = value;
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((key == null) ? 0 : key.hashCode());
		result = prime * result + ((value == null) ? 0 : value.hashCode());
		return result;
	}

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
		@SuppressWarnings("rawtypes")
		KeyValue other = (KeyValue) obj;
		if (key == null) {
			if (other.key != null) {
				return false;
			}
		} else if (!key.equals(other.key)) {
			return false;
		}
		if (value == null) {
			if (other.value != null) {
				return false;
			}
		} else if (!value.equals(other.value)) {
			return false;
		}
		return true;
	}

	@Override
	public String toString() {
		return "KeyValue [key=" + key + ", value=" + value + "]";
	}

	public K getKey() {
		return key;
	}

	public void setKey(K key) {
		this.key = key;
	}

	public V getValue() {
		return value;
	}

	public void setValue(V value) {
		this.value = value;
	}

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">--- javascript 
--- 带有分页，读取服务器数据的ComboBox
var InfoClass = Ext.data.Record.create([ {
	name : 'key',
	type : 'string'
}, {
	name : 'value',
	type : 'string'
} ]);

var store = new Ext.data.JsonStore({
       root: 'root',
       totalProperty: 'totalProperty',
       fields: InfoClass,
       proxy : new Ext.data.HttpProxy({
       	url : basePath + 'web/dataQuery/getSQLHistoryDatas'
	})
   });

var pageSize = 10;
store.baseParams.userKey = parent.userKey;// come from index.jsp
store.baseParams.start = 0;
store.baseParams.limit = pageSize;
store.load();

new Ext.form.ComboBox(
		{
			id : 'sqlQueryHistoryCombo',
			tpl : '&lt;tpl for="."&gt;&lt;div ext:qtip="{key} {nick}" class="x-combo-list-item"&gt;{value}&lt;/div&gt;&lt;/tpl&gt;',
			store : store,
			displayField : 'value',
			valureField : 'key',
			typeAhead : true,
			width : 600,
			editable : false,// 不允许编辑
			mode : 'remote',
			forceSelection : true,
			triggerAction : 'all',
			emptyText : '选择历史查询记录...',
			selectOnFocus : true,
			renderTo : 'sqlQueryHistoryDivId',
			pageSize : pageSize,
			listeners : {
				select : function(combo, record, index) {
					
				}
			}
		});</pre> 
 <p>&nbsp;</p> 
</div>