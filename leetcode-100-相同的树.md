给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

**示例 1:**

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/example1.PNG)

**示例 2:**

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/example2.PNG)

**示例 3:**

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/example3.PNG)

# 思路

```java
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if(p==null&&q==null){
            return true;
        }
        else if(p==null||q==null){
            return false;
        }
        else if(p.val != q.val){
            return false;
        }
        return isSameTree(p.left,q.left) && isSameTree(p.right,q.right);
        
    }
}
```

原理其实相当简单递归的判断两个节点，要么都为空，要么都不为空且值相等，这样递归到将两棵树比较结束。

这里还是看一下labuladong的文章[写树算法的套路框架](https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hui-su-suan-fa-xiang-jie-xiu-ding-ban),特别要注意**框架思维**,如二叉树算法的设计的总路线：

```java
void traverse(TreeNode root) {
    // root 需要做什么？在这做。
    // 其他的不用 root 操心，抛给框架
    traverse(root.left);
    traverse(root.right);
}
```

以及BST遍历的框架：

```java
void BST(TreeNode root, int target) {
    if (root.val == target)
        // 找到目标，做点什么
    if (root.val < target) 
        BST(root.right, target);
    if (root.val > target)
        BST(root.left, target);
}
```

