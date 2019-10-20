#Java中equals和== 的区别
###发表时间：2013-11-27
###分类：经验,java
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/1981704" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/1981704</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>很新手都困惑在equals和== 这个2个比较操作上面。</p> 
 <p>在《Java编程思想（第四版）》里面对这2个操作符有详细的论述。</p> 
 <p>我这里呢，写出了自己给出的一个例子，实在懒得看书的，可以看看。</p> 
 <pre name="code" class="java">public class TestEquals {

	/**
	 * &lt;pre&gt;
	 * 这里的例子给出了 equals() 和 == 的区别
	 * 阐述如下：
	 * 1、 == 比较的是两个引用的内存地址。如果两个引用的内存地址一样，那么 == 的操作的结果为： true
	 * 	什么时候两个引用的内存地址一样呢？下面的例子里面有说明。
	 *  内存地址一样，其实就是这两个引用指向的实例就是同一个。
	 *  
	 * 2、equals 比较的是两个引用的内容。
	 * 	每个类需要覆盖Object这个“根”类的equals方法。如果在类里面不覆盖equals()方法，就会调用父类的equals()方法。
	 *  如果父类就是Object，会出现什么情况呢？下面是JDK中Object的equals源代码：
	 *  public boolean equals(Object obj) {
	 *         return (this == obj);
	 *   }
	 *   我们可以看见，Object类的equals方法，默认的是对比两个引用的内存地址，采用的是 == 的比较。
	 * 
	 * &lt;/pre&gt;
	 */
	public static void main(String[] args) {
		TestEquals t = new TestEquals();
		String name = "kanpiaoxue";
		int age = 30;

		Person p1 = t.new Female(name, age);// 这里的Female类里面，没有覆盖Object的equals()
		Person p2 = t.new Female(name, age);
		System.out.println(p1 == p2);// false
										// 因为他们是2个引用指向了2个实例，这2个实例在内存的堆上面分配了不同的内存地址空间。
		System.out.println(p1.equals(p2));// false
											// 因为Female类没有覆盖equals的方法，所以会去调用Object的equals，这里依然采用的
											// == 进行比较，是比较的内存地址。

		p2 = p1;// 这里将2个引用指向了同一个实例，也就是指向了同一个内存地址。
		System.out.println(p1 == p2);// true 相同的内存地址，这里输出 true
		System.out.println(p1.equals(p2));// true
											// 因为Female没有覆盖equals方法，所以会调用父类Person的equals方法。因为Person也没有覆盖equals，所以继续调用Person的父类Object的equals方法。相同的内存地址，这里输出
											// true

		Person p3 = t.new Male(name, age); // Male类 覆盖了equals方法。
		Person p4 = t.new Male(name, age);
		System.out.println(p3 == p4);// false 同样，这里是2个实例，就是2个不同的内存地址。
		System.out.println(p3.equals(p4));// true
											// 这里实现了equals方法，而且equals方法里面是对name和age的比较。

		String hello1 = "hello";// 开辟一个String的内存地址
		String hello2 = "hello";// 这里可不是指向新的内存地址。为什么？因为Java对String有特殊的处理。在Java的内存中，所有的相同的字符串，都是同一个内存地址，也就是同一个实例。具体解释，请看《Java编程思想（第四版）》关于String的描述。
		System.out.println(hello1 == hello2);// true
		System.out.println(hello1.equals(hello2));// true

	}

	class Person {
		protected String name;
		protected int age;

		public Person(String name, int age) {
			super();
			this.name = name;
			this.age = age;
		}
	}

	class Female extends Person {
		public Female(String name, int age) {
			super(name, age);
		}
	}

	class Male extends Person {
		public Male(String name, int age) {
			super(name, age);
		}

		@Override
		public int hashCode() {
			final int prime = 31;
			int result = 1;
			result = prime * result + getOuterType().hashCode();
			result = prime * result + age;
			result = prime * result + ((name == null) ? 0 : name.hashCode());
			return result;
		}

		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			Male other = (Male) obj;
			if (!getOuterType().equals(other.getOuterType()))
				return false;
			if (age != other.age)
				return false;
			if (name == null) {
				if (other.name != null)
					return false;
			} else if (!name.equals(other.name))
				return false;
			return true;
		}

		private TestEquals getOuterType() {
			return TestEquals.this;
		}

	}

}</pre> 
 <p>&nbsp;</p> 
</div>