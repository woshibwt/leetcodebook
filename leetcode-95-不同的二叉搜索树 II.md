给定一个整数 n，生成所有由 1 ... n 为节点所组成的 二叉搜索树 。

 

示例：

输入：3
输出：
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20200826164907.png)



思考这个问题，我们先从锚定根节点，如何构建一棵二叉搜索树开始，然后进一步思考，在一个区间内遍历选择所有不同的根节点，并且将返回的节点装在列表中（left,right）,并且通过二层循环将两个列表中的节点依次放在当前root两边

# 构建一棵二叉搜索树

```java

public TreeNode createBinaryTree(int n){
    return helper(1, n);
}

public TreeNode helper(int start, int end){
    if (start > end)
        return null;


// 这里可以选择从start到end的任何一个值做为根结点，
// 这里选择它们的中点，实际上，这样构建出来的是一颗平衡二叉搜索树
int val = (start + end) / 2;
TreeNode root = new TreeNode(val);

root.left = helper(start, val - 1);
root.right = helper(val + 1, end);

return root;

}

```

在选择根节点时，可以不用取中点构造平衡二叉树，用遍历的方法也可

```java
// 选择所有可能的根结点
for(int i = start; i <= end; i++){
    TreeNode root = new TreeNode(i);
    ...
}
```

# 构建多棵二叉搜索树返回列表

在这道题中我们需要的是多棵树，可以将不同的根节点装入list后返回，可以将上述代码改写为：

```java
    public List<TreeNode> helper(int start, int end){
        List<TreeNode> list = new ArrayList<>();        

        if(start > end){
            list.add(null);
            return list;
        }

        for(int i = start; i <= end; i++){
            TreeNode root = new TreeNode(i);
            ...
            ...
            // 装入所有根结点
            list.add(root);
        }

        return list;
    }
```



# 如何构建root的左右子树

我们抛开复杂的递归函数，只关心递归的返回值，每次选择根结点root，我们

1.递归构建左子树，并拿到左子树所有可能的根结点列表left  
        2.递归构右子树，并拿到右子树所有可能的根结点列表right  
        这个时候我们有了左右子树列表，我们的左右子树都是各不相同的，因为根结点不同，我们如何通过左右子树列表构建出所有的以root为根的树呢？  

我们固定一个左孩子，遍历右子树列表，那么以当前为root根结点的树个数就为left.size() * right.size()个。  

```java
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if(n < 1)
            return new ArrayList<>();
        return helper(1, n);
    }

    public List<TreeNode> helper(int start, int end){
        List<TreeNode> list = new ArrayList<>();

        if(start > end){
            // 如果当前子树为空，不加null行吗？
            list.add(null);
            return list;
        }

        for(int i = start; i <= end; i++){
            // 想想为什么这行不能放在这里，而放在下面？
            // TreeNode root = new TreeNode(i);
            List<TreeNode> left = helper(start, i-1);  
            List<TreeNode> right = helper(i+1, end); 

            // 固定左孩子，遍历右孩子
            for(TreeNode l : left){
                for(TreeNode r : right){
                    TreeNode root = new TreeNode(i);
                    root.left = l;
                    root.right = r;
                    list.add(root);
                }
            }
        }
        return list;
    }
}
```

# 值得注意的问题

关于`TreeNode root = new TreeNode(i)`的放置的位置问题，如果放在注释那行，那么每次从left,right列表摘一个TreeNode出来时，放在的都是同一个root下，这样该root(i)只会有```num``` 棵相同的树（```num = left.size() * right.size() > 1```）  

当前子树为空则必须要加null 显然，如果一颗树的左子树为空，右子树不为空，要正确构建所有树，依赖于对左右子树列表的遍历，也就是上述代码两层for循环的地方，如果其中一个列表为空，那么循环都将无法进行。(list.size==1)  

每棵树的根节点在递归是start都与end相同，如```helper(1,1),helper(2,2),helper(3,3)```,会用这个值生成一个根节点并装在list中返回回去(list.size==1),作为上一级方法中根节点的```left列表```或```right列表```

