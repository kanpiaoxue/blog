#java的String字符串反转
###发表时间：2019-05-10
###分类：java,经验
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2440852" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2440852</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>反转字符串的实现方法多种多样，这里给出一些小例子：</p> 
 <p>思路：String是有char组成的一个数组，将该数组的元素反向排列形成的新的字符串就是答案。不过实现该方法的具体实现很多，但是本质上是一致的，都是反转字符的数组。</p> 
 <pre name="code" class="java">    public static void main(String[] args)  {
        String base = "helloworld";
        System.out.println(base);
        System.out.println(reverseString01(base));
        System.out.println(reverseString02(base));
        System.out.println(reverseString03(base));
        System.out.println(reverseString04(base, base.length() - 1));
        System.out.println(reverseString05(base));
        /**
         * helloworld
         * dlrowolleh
         * dlrowolleh
         * dlrowolleh
         * dlrowolleh
         * dlrowolleh
         */
    }

    public static String reverseString01(String origin) {
        if (Objects.isNull(origin) || origin.isEmpty()) {
            return origin;
        }
        char[] sourceArray = origin.toCharArray();
        char[] targetArray = new char[sourceArray.length];
        for (int i = sourceArray.length - 1, j = 0; i &gt;= 0; i--, j++) {
            targetArray[j] = sourceArray[i];
        }
        return new String(targetArray);
    }

    public static String reverseString02(String source) {
        int length = source.length();
        StringBuilder dest = new StringBuilder(length);
        for (int i = length - 1; i &gt;= 0; i--) {
            dest.append(source.charAt(i));
        }
        return dest.toString();
    }

    public static String reverseString03(String source) {
        return new StringBuilder(source).reverse().toString();
    }

    public static String reverseString04(String stringToReverse, int index) {
        if (index == 0) {
            return stringToReverse.charAt(0) + "";
        }
        char letter = stringToReverse.charAt(index);
        return letter + reverseString04(stringToReverse, index - 1);
    }

    public static String reverseString05(String s) {
        LinkedList&lt;Character&gt; stack = new LinkedList&lt;&gt;();
        for (int i = 0, j = s.length(); i &lt; j; i++) {
            stack.push(s.charAt(i));
        }
        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        return sb.toString();
    }</pre> 
 <p>&nbsp;</p> 
</div>