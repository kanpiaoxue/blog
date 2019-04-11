#ajax/javascript先后台传递对象参数
###发表时间：2015-08-27
###分类：javascript,ajax
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2238377" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2238377</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>在做spring MVC开发的时候，我需要在页面的JavaScript中将js对象拼接成后台spring Controller需要接收的Javabean对象。示例如下：</p> 
 <pre name="code" class="java">    /**
     * 更新团队资源
     * 
     * @param response
     * @param teamResource
     */
    @RequestMapping(value = "/updateTeamResource", method = RequestMethod.POST)
    public void updateTeamResource(HttpServletResponse response, @RequestBody TeamResource teamResource) {

        try {
            TeamResource updatedResource = teamResourceService.updateTeamResource(teamResource);

            processSuccessDataForResponse(response, updatedResource);
        } catch (Exception e) {
            processExceptionForResponse(response, e, e.getMessage());
        }

    }
</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">TeamResource {

    /**
     * 资源id
     */
    private long resourceId;

    /**
     * 资源名称
     */
    private String resourceName;

    /**
     * 资源类型id
     */
    private int resourceTypeId;

    /**
     * 资源配置
     * 
     * &lt;pre&gt;
     * 当为mysql资源时 ,{"host":"10.1.1.1","port":"90","user":"crm","passwd":"123","db":"wdyx","isfenku":"false"}  
     * 为 ftp资源时  {"ip":"10.11","port":"80","user":"12","passwd":"13"} 
     * 为hive资源时, 
     * {
     *                     "hiveSite":{
     *                         "hive.querylog.location":"/home/users/zhouliechun/hive_log",
     *                         "hive.default.database.uri":"hdfs://nmg01-mulan-hdfs.dmop.baidu.com:54310/app/ecom/rigelci/hive"
     *                   
     *                     },
     *                     "hadoopSite":{
     *                         "mapred.job.tracker":"nmg01-mulan-job.dmop.baidu.com:54311",
     *                         "dfs.client.transfer.limit.usetk":"false"
     *                     }
     *                 }
     * 
     * 为drun的时候  {"drun_cluster_name":"cdc_etl2,cdc_etl3"}
     * 
     * 
     * &lt;/pre&gt;
     */
    private String resourceValue;

    /**
     * 团队id
     */
    private long teamId;

    /**
     * 创建时间
     */
    private Date gmtCreate;

    /**
     * 最后修改时间
     */
    private Date gmtModify;

    /**
     * 备注
     */
    private String note;

    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((note == null) ? 0 : note.hashCode());
        result = prime * result + ((gmtCreate == null) ? 0 : gmtCreate.hashCode());
        result = prime * result + ((gmtModify == null) ? 0 : gmtModify.hashCode());
        result = prime * result + (int) (resourceId ^ (resourceId &gt;&gt;&gt; 32));
        result = prime * result + ((resourceName == null) ? 0 : resourceName.hashCode());
        result = prime * result + resourceTypeId;
        result = prime * result + ((resourceValue == null) ? 0 : resourceValue.hashCode());
        result = prime * result + (int) (teamId ^ (teamId &gt;&gt;&gt; 32));
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
        TeamResource other = (TeamResource) obj;
        if (note == null) {
            if (other.note != null) {
                return false;
            }
        } else if (!note.equals(other.note)) {
            return false;
        }
        if (gmtCreate == null) {
            if (other.gmtCreate != null) {
                return false;
            }
        } else if (!gmtCreate.equals(other.gmtCreate)) {
            return false;
        }
        if (gmtModify == null) {
            if (other.gmtModify != null) {
                return false;
            }
        } else if (!gmtModify.equals(other.gmtModify)) {
            return false;
        }
        if (resourceId != other.resourceId) {
            return false;
        }
        if (resourceName == null) {
            if (other.resourceName != null) {
                return false;
            }
        } else if (!resourceName.equals(other.resourceName)) {
            return false;
        }
        if (resourceTypeId != other.resourceTypeId) {
            return false;
        }
        if (resourceValue == null) {
            if (other.resourceValue != null) {
                return false;
            }
        } else if (!resourceValue.equals(other.resourceValue)) {
            return false;
        }
        if (teamId != other.teamId) {
            return false;
        }
        return true;
    }

    @Override
    public String toString() {
        return "Resource [resourceId=" + resourceId + ", resourceName=" + resourceName + ", resourceTypeId="
                + resourceTypeId + ", resourceValue=" + resourceValue + ", teamId=" + teamId + ", gmtCreate="
                + gmtCreate + ", gmtModify=" + gmtModify + ", note=" + note + "]";
    }

    public long getResourceId() {
        return resourceId;
    }

    public void setResourceId(long resourceId) {
        this.resourceId = resourceId;
    }

    public String getResourceName() {
        return resourceName;
    }

    public void setResourceName(String resourceName) {
        this.resourceName = resourceName;
    }

    public int getResourceTypeId() {
        return resourceTypeId;
    }

    public void setResourceTypeId(int resourceTypeId) {
        this.resourceTypeId = resourceTypeId;
    }

    public String getResourceValue() {
        return resourceValue;
    }

    public void setResourceValue(String resourceValue) {
        this.resourceValue = resourceValue;
    }

    public long getTeamId() {
        return teamId;
    }

    public void setTeamId(long teamId) {
        this.teamId = teamId;
    }

    public Date getGmtCreate() {
        return gmtCreate;
    }

    public void setGmtCreate(Date gmtCreate) {
        this.gmtCreate = gmtCreate;
    }

    public Date getGmtModify() {
        return gmtModify;
    }

    public void setGmtModify(Date gmtModify) {
        this.gmtModify = gmtModify;
    }

    public String getNote() {
        return note;
    }

    public void setNote(String note) {
        this.note = note;
    }

}</pre> 
 <p>&nbsp;</p> 
 <pre name="code" class="js">var args = {
                                    resourceId: resourceId,
                                    resourceName: resourceName,
                                    resourceTypeId: resourceType,
                                    resourceValue: resourceValue,
                                    teamId: teamId,
                                    note: comments
                                };
args = JSON.stringify(args);//这一步很关键

                            var options = {
                                url: window.basePath + url,
                                contentType: 'application/json',//这里也很关键，否则后台收不到
                                type: 'post',
                                dataType: 'json',
                                data: args,
                                success: function(rs) {
                                    if (0 === rs.status) {
                                        window.showTipMessage(msg, function() {
                                            bd.m.tools.closeProgress();
                                            // 隐藏panel
                                            bd.v.layout.whole.hide();
                                            // 刷新Grid
                                            bd.m.grid.reloadGrid();
                                        });
                                    }
                                    else {
                                        window.showErrorMessage('操作失败！原因是：'
                                            + rs.statusInfo, function() {
                                            bd.m.tools.closeProgress();
                                        });
                                    }
                                },
                                error: function(rs) {
                                    bd.m.tools.closeProgress();
                                }
                            };
                            $.ajax(options);</pre> 
 <p>&nbsp;</p> 
</div>