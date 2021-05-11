#java中tree的应用示例：javax.swing.tree.DefaultMutableTreeNode
###发表时间：2021-02-03
###分类：经验,java,tree
###iteye原始地址：<a href="https://kanpiaoxue.iteye.com/admin/blogs/2519061" target="_blank">https://kanpiaoxue.iteye.com/admin/blogs/2519061</a>

---

<div class="iteye-blog-content-contain" style="font-size: 14px;"> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
 <pre name="code" class="java">package org.kanpiaoxue.tree;

import org.apache.commons.collections.CollectionUtils;

import com.google.common.base.Splitter;
import com.google.common.collect.Lists;

import java.util.List;
import java.util.Queue;

import javax.swing.tree.DefaultMutableTreeNode;

/**
 * tree的示例
 *
 * @ClassName: TreeExample
 * @author kanpiaoxue
 * @version 1.0
 * @CreateTime: 2021/02/03 14:55:12
 * @Description:
 */
public class TreeExample {
    private static final String PATH_SPLIT_STRING = "/";

    /**
     *
     * DefaultMutableTreeNode 树形结构的示例。
     *
     * @throws Exception
     * @author kanpiaoxue
     * @CreateTime: 2021/02/03 14:55:12
     * @Description:
     */
    public static void main(String[] args) {

        /**
         * 示例1：构建一颗树
         * 下面的代码构建了一棵树，有7个node。如url的图片。
         * https://app.diagrams.net/?lightbox=1&amp;highlight=0000ff&amp;edit=_blank&amp;layers=1&amp;nav=1&amp;title=Untitled%20Diagram.drawio#R5ZhNj5swEIZ%2FDcdKfC0h1023zaE9VDnsqjcvnoAjwyBjAvTX1ywmBLlNqdQWRz2BX4%2BN%2FfidQeAEu7z9KEiZfUYK3PFd2jrBe8f3Pc%2BN1KVXukHZbjeDkApGddAkHNg30KKr1ZpRqGaBEpFLVs7FBIsCEjnTiBDYzMOOyOdPLUkKhnBICDfVZ0ZlNqixv5n0PbA0G5%2FsRduhJydjsN5JlRGKzZUUPDnBTiDK4S5vd8B7eCOXYdyHn%2FReFiagkEsGdDH%2F%2BlLvX%2FmJ7atz%2BfIlOz2%2FC4ZZzoTXesN6sbIbCQisCwr9JK4TPKKQGaZYEP4JsVSip8QTSNnpsyO1RCVlMue6d5gRqAF6WrmWKqxFAjeWOzqAiBTkjTj%2FwlcZEzAHKTo1TgAnkp3n6yDaIeklboKobjTH32D68GumPYyDbhZYqMvjPWIO18TsGZiJyZlzVSh6vE3GJBxK8rbvRtWqOTxSlUP1OLK2PwRN8wxCQnubp7l%2FPSAYM1%2BXPj%2FW7WYqJKGWsqsaMmp%2FnpiJ7N6cGS50puf%2B%2BGj%2BjTVDg3NilzVDd27NIFrbmq6B7Gg3sjBcGdnm7pPZX5jM0Zq5vP1vMMdrYvYNzK925f8lkW0pmbFBDCwjFltWMb0FXzuW53K0MJe9Vb%2BAIoMztcyatr3MPbP%2BpXYje%2FD%2FGjLVnH6LvPVd%2FVwKnr4D
         */
        DefaultMutableTreeNode a = new DefaultMutableTreeNode("a", true);
        DefaultMutableTreeNode b = new DefaultMutableTreeNode("b", true);
        DefaultMutableTreeNode c = new DefaultMutableTreeNode("c", true);
        DefaultMutableTreeNode d = new DefaultMutableTreeNode("d", true);
        DefaultMutableTreeNode e = new DefaultMutableTreeNode("e", true);
        DefaultMutableTreeNode f = new DefaultMutableTreeNode("f", true);
        DefaultMutableTreeNode g = new DefaultMutableTreeNode("g", true);

        a.add(b);
        a.add(c);

        b.add(d);
        b.add(e);

        c.add(f);

        d.add(g);

        System.out.println(String.format("%s", Lists.newArrayList(g.getPath())));
        System.out.println(String.format("%s", a.getDepth()));
        System.out.println(String.format("%s", a.getLevel()));

        /**
         * 示例2：从一个存储路径构建一棵树
         * 下面的代码构建了一棵树，有18个node。如path。
         */
        String path =
                "/Users/kanpiaoxue/workspaces/test-web/src/main/java/org/kanpiaoxue/test/web/service/store/impl";

        DefaultMutableTreeNode root = buildTreeFromPath(path);

        System.out.println(String.format("--&gt;%s", root));
        System.out.println(String.format("--&gt;%s", root.getFirstChild()));
        System.out.println(String.format("--&gt;%s", root.getFirstChild().getChildAt(0)));
        System.out.println(String.format("--&gt;%s", root.getFirstChild().getChildAt(0).getChildAt(0)));
        System.out.println(String.format("--&gt;%s", root.getDepth()));
        System.out.println(String.format("--&gt;%s", Lists.newArrayList(root.getLastLeaf().getPath())));
        System.out.println(String.format("--&gt;%s", Lists.newArrayList(root.getLastLeaf().getPath()).size()));

    }

    /**
     *
     * 从路径构建一棵树
     *
     * @param path
     * @return
     * @author kanpiaoxue
     * @CreateTime: 2021/02/03 14:57:42
     * @Description:
     */
    private static DefaultMutableTreeNode buildTreeFromPath(String path) {
        Queue&lt;String&gt; treeData = Lists.newLinkedList();
        List&lt;String&gt; list = Splitter.on(PATH_SPLIT_STRING).trimResults().omitEmptyStrings().splitToList(path);
        if (CollectionUtils.isNotEmpty(list)) {
            treeData.addAll(list);
        }

        DefaultMutableTreeNode root = new DefaultMutableTreeNode(PATH_SPLIT_STRING, true);
        int level = 0;

        DefaultMutableTreeNode currentNode = null;
        while (!treeData.isEmpty()) {
            DefaultMutableTreeNode node = new DefaultMutableTreeNode(treeData.poll(), true);
            if (level != 0) {
                currentNode.add(node);
            } else {
                root.add(node);
            }
            currentNode = node;
            level++;
        }
        return root;
    }
}
</pre> 
 <p>&nbsp;</p> 
 <p>&nbsp;</p> 
</div>