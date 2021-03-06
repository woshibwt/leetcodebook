给定一个二叉树，检查它是否是镜像对称的

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的



![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20200921232030.png)

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20200921232119.png)

## 思路

评论里这位老哥说的很好：

> 递归的难点在于：找到可以递归的点 为什么很多人觉得递归一看就会，一写就废。 或者说是自己写无法写出来，关键就是你对递归理解的深不深。
>
> 对于此题： 递归的点怎么找？从拿到题的第一时间开始，思路如下：
>
> 1.怎么判断一棵树是不是对称二叉树？ 答案：如果所给根节点，为空，那么是对称。如果不为空的话，当他的左子树与右子树对称时，他对称
>
> 2.那么怎么知道左子树与右子树对不对称呢？在这我直接叫为左树和右树 答案：如果左树的左孩子与右树的右孩子对称，左树的右孩子与右树的左孩子对称，那么这个左树和右树就对称。
>
> 仔细读这句话，是不是有点绕？怎么感觉有一个功能A我想实现，但我去实现A的时候又要用到A实现后的功能呢？
>
> 当你思考到这里的时候，递归点已经出现了： 递归点：我在尝试判断左树与右树对称的条件时，发现其跟两树的孩子的对称情况有关系。
>
> 想到这里，你不必有太多疑问，上手去按思路写代码，函数A（左树，右树）功能是返回是否对称
>
> def 函数A（左树，右树）： 左树节点值等于右树节点值 且 函数A（左树的左子树，右树的右子树），函数A（左树的右子树，右树的左子树）均为真 才返回真
>
> 实现完毕。。。
>
> 写着写着。。。你就发现你写出来了。。。

```java
class Solution {
        public boolean isSymmetric(TreeNode root) {
        if(root == null) return true;
        return helper(root.left,root.right);
    }
    public boolean helper(TreeNode left,TreeNode right){
         if(left == null && right == null)
            return true;
        else if(left==null || right == null)
            return false;
        else if(left.val != right.val)
            return false;

        return helper(left.left,right.right) && helper(left.right,right.left);
    }
}
```

注意这种思路下要跳出原来只给一个参数的局限，坚决定义辅助函数