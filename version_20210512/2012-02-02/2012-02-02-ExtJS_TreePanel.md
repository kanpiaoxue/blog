#ExtJS TreePanel
###发表时间：2012-02-02
###分类：Ext
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1391489" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1391489</a>

---

<p>ExtJS的Treepanel 经常被使用到，这里我写了一颗树。上面的数据用json从后台打回来到前台就可以使用。这颗树的json数据里面有部分属性没有用到，请大家使用的时候自己去掉。</p>
<p>&nbsp;</p>
<p> </p>
<pre name="code" class="java">var treeMenu = [ {
			"id" : 370,
			"valid" : true,
			"createTime" : "2011-07-22 00:00:00",
			"text" : "小型超市商务平台",
			"nodeId" : "132",
			"parentNodeId" : "0",
			"cls" : "folder",
			"sortId" : 100,
			"link" : "#",
			"children" : [ {
				"id" : 371,
				"valid" : true,
				"createTime" : "2011-07-22 00:00:00",
				"text" : "销售",
				"nodeId" : "133",
				"parentNodeId" : "132",
				"cls" : "folder",
				"sortId" : 1,
				"link" : "#",
				"children" : [ {
					"id" : 376,
					"valid" : true,
					"createTime" : "2011-07-26 00:00:00",
					"text" : "当前销售",
					"nodeId" : "138",
					"parentNodeId" : "133",
					"cls" : "file",
					"sortId" : 1,
					"link" : "/jsp/",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 377,
					"valid" : true,
					"createTime" : "2011-07-26 00:00:00",
					"text" : "销售记录",
					"nodeId" : "139",
					"parentNodeId" : "133",
					"cls" : "file",
					"sortId" : 10,
					"link" : "/jsp",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				} ],
				"validValue" : 0,
				"leaf" : false
			}, {
				"id" : 372,
				"valid" : true,
				"createTime" : "2011-07-22 00:00:00",
				"text" : "进货",
				"nodeId" : "134",
				"parentNodeId" : "132",
				"cls" : "folder",
				"sortId" : 10,
				"link" : "#",
				"children" : [],
				"validValue" : 0,
				"leaf" : false
			}, {
				"id" : 373,
				"valid" : true,
				"createTime" : "2011-07-22 00:00:00",
				"text" : "仓储",
				"nodeId" : "135",
				"parentNodeId" : "132",
				"cls" : "folder",
				"sortId" : 20,
				"link" : "#",
				"children" : [],
				"validValue" : 0,
				"leaf" : false
			}, {
				"id" : 374,
				"valid" : true,
				"createTime" : "2011-07-22 00:00:00",
				"text" : "结余",
				"nodeId" : "136",
				"parentNodeId" : "132",
				"cls" : "folder",
				"sortId" : 30,
				"link" : "#",
				"children" : [],
				"validValue" : 0,
				"leaf" : false
			} ],
			"validValue" : 0,
			"leaf" : false
		}, {
			"id" : 368,
			"valid" : true,
			"createTime" : "2000-01-01 00:00:00",
			"text" : "系统管理",
			"nodeId" : "6",
			"parentNodeId" : "0",
			"cls" : "folder",
			"sortId" : 999999,
			"link" : "#",
			"children" : [ {
				"id" : 378,
				"valid" : true,
				"createTime" : "2011-07-26 00:00:00",
				"text" : "后台管理-管理员",
				"nodeId" : "140",
				"parentNodeId" : "6",
				"cls" : "folder",
				"sortId" : 999,
				"link" : "#",
				"children" : [ {
					"id" : 379,
					"valid" : true,
					"createTime" : "2011-07-26 00:00:00",
					"text" : "个人信息",
					"nodeId" : "141",
					"parentNodeId" : "140",
					"cls" : "file",
					"sortId" : 1,
					"link" : "/jsp/",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				} ],
				"validValue" : 0,
				"leaf" : false
			}, {
				"id" : 7,
				"valid" : true,
				"createTime" : "2009-04-07 00:00:00",
				"text" : "后台管理-&lt;span style='color:red;'&gt;超级管理员&lt;\/span&gt;",
				"nodeId" : "1",
				"parentNodeId" : "6",
				"cls" : "folder",
				"sortId" : 900000,
				"link" : "#",
				"children" : [ {
					"id" : 49,
					"valid" : true,
					"createTime" : "2009-06-05 00:00:00",
					"text" : "菜单树管理",
					"nodeId" : "5",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 0,
					"link" : "/direct/menuTree.do",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 103,
					"valid" : true,
					"createTime" : "2009-07-14 00:00:00",
					"text" : "用户管理",
					"nodeId" : "122",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 10,
					"link" : "/direct/user/manage.do",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 375,
					"valid" : true,
					"createTime" : "2011-07-26 00:00:00",
					"text" : "用户组管理",
					"nodeId" : "137",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 15,
					"link" : "/jsp/",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 107,
					"valid" : true,
					"createTime" : "2010-01-07 00:00:00",
					"text" : "用户组分配",
					"nodeId" : "131",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 20,
					"link" : "/jsp/background_management/adminUserGroup.jsp",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 105,
					"valid" : true,
					"createTime" : "2010-01-07 00:00:00",
					"text" : "权限组管理",
					"nodeId" : "129",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 40,
					"link" : "/jsp/background_management/addAuthGroup.jsp",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 20,
					"valid" : true,
					"createTime" : "2009-04-28 00:00:00",
					"text" : "用户权限管理",
					"nodeId" : "2",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 50,
					"link" : "/jsp/background_management/admin.jsp",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				}, {
					"id" : 106,
					"valid" : true,
					"createTime" : "2010-01-07 00:00:00",
					"text" : "组权限分配",
					"nodeId" : "130",
					"parentNodeId" : "1",
					"cls" : "file",
					"sortId" : 60,
					"link" : "/jsp/background_management/adminAuthGroup.jsp",
					"children" : [],
					"validValue" : 0,
					"leaf" : true
				} ],
				"validValue" : 0,
				"leaf" : false
			} ],
			"validValue" : 0,
			"leaf" : false
		} ];</pre>
<span style="white-space: pre; background-color: #fafafa;"> /**</span>
<pre name="code" class="java">			 * 左边的树
			 */
			var westObj = {
				id : 'menuTree',
				region : 'west',
				collapsible : true,
				animate : true,
				title : CommonUtils.language.treeTitle,
				xtype : 'treepanel',
				width : 200,
				autoScroll : true,
				split : true,
				loader : new Ext.tree.TreeLoader(),
				root : new Ext.tree.AsyncTreeNode( {// 树根
							id : 'rootTreeId',
							text : CommonUtils.language.projectName,
							iconCls : 'treeNodeStyle',
							expanded : true,
							children : treeMenu
						}),
				rootVisible : true,// 根节点的可见性
				listeners : {// 点击后调用的方法
					click : function(n) {

						// 如果是叶子节点并且点击的不是olap菜单
				if (n.isLeaf()) {
					var tabTitle = n.attributes.text;
					var targetUrl = basePath + n.attributes.link;
					addTab(n.attributes.id, tabTitle, targetUrl);
				} else {
					if (n.isExpanded()) {// 树节点的开关
					n.collapse(false, true);
				}
			}

		}
	}
			};</pre>