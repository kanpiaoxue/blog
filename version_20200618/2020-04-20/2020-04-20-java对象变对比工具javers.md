#java对象变对比工具javers
###发表时间：2020-04-20
###分类：javers,java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2513747" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2513747</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <pre name="code" class="java">public static &lt;T&gt; DifferenceResult diff(T oldInstance, T newInstance) {
        LOGGER.debug("start to diff. oldInstance:{},newInstance:{}", oldInstance, newInstance);
        Preconditions.checkNotNull(oldInstance, "oldInstance is null");
        Preconditions.checkNotNull(newInstance, "newInstance is null");
        Stopwatch sw = Stopwatch.createStarted();
        // given
        Javers javers = JaversBuilder.javers().build();
        // when
        Diff diff = javers.compare(oldInstance, newInstance);
        List&lt;ValueChange&gt; changes = diff.getChangesByType(ValueChange.class);
        if (CollectionUtils.isEmpty(changes)) {
            LOGGER.debug("diff. nothing changed. oldInstance:{},newInstance:{}", oldInstance, newInstance);
            return DifferenceResult.builder().withDiff(false).withMessage(StringUtils.EMPTY).build();
        }

        String message = changes.stream().map(change -&gt; {
            Object leftMsg = formatDate(change.getLeft());
            Object rightMsg = formatDate(change.getRight());
            return String.format("%s:[%s]-&gt;[%s]", change.getPropertyName(), leftMsg, rightMsg);
        }).collect(Collectors.joining(","));
        DifferenceResult result = DifferenceResult.builder().withDiff(true).withMessage(message).build();
        LOGGER.debug("diff. {} changed. it consume {}. oldInstance:{},newInstance:{}", result, sw,
                oldInstance, newInstance);
        return result;
    }</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">如果要忽略一些字段的比较，可以采用下面的注解的方式：</p> 
 <pre name="code" class="java">@DiffIgnore
private Date modifiedTime;
@DiffIgnore
private Date createTime;</pre> 
 <p style="font-size: 14px;">&nbsp;&nbsp;&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">javers:&nbsp;<a href="https://javers.org/documentation/diff-examples/#compare-entities">https://javers.org/documentation/diff-examples/#compare-entities</a></p> 
 <p style="font-size: 14px;">参考：&nbsp;<a href="https://www.baeldung.com/javers">https://www.baeldung.com/javers</a></p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">一个简单的方法：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">下面的是简单示例：</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public class JaVers {

    /**
     * @param args
     * @author kanpiaoxue
     * @CreateTime: 2020/04/20 17:09:05
     * @Description:
     */
    public static void main(String[] args) {
        // given
        Javers javers = JaversBuilder.javers().build();

        SimplePerson oldPerson = SimplePerson.builder().withId(1).withName("hello").build();
        SimplePerson newPerson = SimplePerson.builder().withId(1).withName("hello1").build();

        // when
        Diff diff = javers.compare(oldPerson, newPerson);

        // then
        List&lt;ValueChange&gt; changes = diff.getChangesByType(ValueChange.class);
        System.out.println(changes);
        // output: [ValueChange{ 'name' value changed from 'hello' to 'hello1'
        // }]

        changes.stream().forEach(change -&gt; {
            System.out.println(change.prettyPrint(PrettyValuePrinter.getDefault()));
            System.out.println(String.format("%s:%s-&gt;%s", change.getPropertyName(), change.getLeft(),
                    change.getRight()));
            // name:hello-&gt;hello1
        });

    }

}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public class SimplePerson {
    /**
     * Builder to build {@link SimplePerson}.
     */
    public static final class Builder {
        private Integer id;
        private String name;

        private Builder() {
        }

        /**
         * Builder method of the builder.
         * 
         * @return built class
         */
        public SimplePerson build() {
            return new SimplePerson(this);
        }

        /**
         * Builder method for id parameter.
         * 
         * @param id
         *            field to set
         * @return builder
         */
        public Builder withId(Integer id) {
            this.id = id;
            return this;
        }

        /**
         * Builder method for name parameter.
         * 
         * @param name
         *            field to set
         * @return builder
         */
        public Builder withName(String name) {
            this.name = name;
            return this;
        }
    }

    private Integer id;
    private String name;

    /**
     *
     */
    public SimplePerson() {
        super();
    }

    private SimplePerson(Builder builder) {
        this.id = builder.id;
        this.name = builder.name;
    }

    /**
     * Creates builder to build {@link SimplePerson}.
     * 
     * @return created builder
     */
    public static Builder builder() {
        return new Builder();
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
        SimplePerson other = (SimplePerson) obj;
        if (id == null) {
            if (other.id != null) {
                return false;
            }
        } else if (!id.equals(other.id)) {
            return false;
        }
        if (name == null) {
            if (other.name != null) {
                return false;
            }
        } else if (!name.equals(other.name)) {
            return false;
        }
        return true;
    }

    /**
     * @return the id
     */
    public Integer getId() {
        return id;
    }

    /**
     * @return the name
     */
    public String getName() {
        return name;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + ((id == null) ? 0 : id.hashCode());
        result = prime * result + ((name == null) ? 0 : name.hashCode());
        return result;
    }

    /**
     * @param id
     *            the id to set
     */
    public void setId(Integer id) {
        this.id = id;
    }

    /**
     * @param name
     *            the name to set
     */
    public void setName(String name) {
        this.name = name;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#toString()
     */
    @Override
    public String toString() {
        return "SimplePerson [id=" + id + ", name=" + name + "]";
    }

}</pre> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <p style="font-size: 14px;">&nbsp;</p> 
 <pre name="code" class="java">public class DifferenceResult {
    /**
     * Builder to build {@link DifferenceResult}.
     */
    public static final class Builder {
        private boolean diff;
        private String message;

        private Builder() {
        }

        /**
         * Builder method of the builder.
         * 
         * @return built class
         */
        public DifferenceResult build() {
            return new DifferenceResult(this);
        }

        /**
         * Builder method for diff parameter.
         * 
         * @param diff
         *            field to set
         * @return builder
         */
        public Builder withDiff(boolean diff) {
            this.diff = diff;
            return this;
        }

        /**
         * Builder method for message parameter.
         * 
         * @param message
         *            field to set
         * @return builder
         */
        public Builder withMessage(String message) {
            this.message = message;
            return this;
        }
    }

    private boolean diff;
    private String message;

    /**
     *
     */
    public DifferenceResult() {
        super();
    }

    private DifferenceResult(Builder builder) {
        this.diff = builder.diff;
        this.message = builder.message;
    }

    /**
     * Creates builder to build {@link DifferenceResult}.
     * 
     * @return created builder
     */
    public static Builder builder() {
        return new Builder();
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
        DifferenceResult other = (DifferenceResult) obj;
        if (diff != other.diff) {
            return false;
        }
        if (message == null) {
            if (other.message != null) {
                return false;
            }
        } else if (!message.equals(other.message)) {
            return false;
        }
        return true;
    }

    /**
     * @return the message
     */
    public String getMessage() {
        return message;
    }

    /*
     * (non-Javadoc)
     * @see java.lang.Object#hashCode()
     */
    @Override
    public int hashCode() {
        final int prime = 31;
        int result = 1;
        result = prime * result + (diff ? 1231 : 1237);
        result = prime * result + ((message == null) ? 0 : message.hashCode());
        return result;
    }

    /**
     * @return the diff
     */
    public boolean isDiff() {
        return diff;
    }

    /**
     * @param diff
     *            the diff to set
     */
    public void setDiff(boolean diff) {
        this.diff = diff;
    }

    /**
     * @param message
     *            the message to set
     */
    public void setMessage(String message) {
        this.message = message;
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
</div>