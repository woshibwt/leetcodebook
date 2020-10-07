首先要知道一个结论，前序/后序+中序序列可以唯一确定一棵二叉树，所以自然而然可以用来建树。

# leetcode 105

根据一棵树的前序遍历与中序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20201007120809.png)



## 思路

preorder第一个元素为root，在inorder里面找到root，在它之前的为左子树（长l1），之后为右子树（长l2）。preorder[1]到preorder[l1]为左子树,之后为右子树，分别递归。

//缺张图

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        return buildTreeHelper(preorder,0,preorder.length,inorder,0,inorder.length);
    }
    private TreeNode buildTreeHelper(int[] preorder,int p_start,int p_end,int[] inorder,int i_start,int i_end){
        if(p_start == p_end){
            return null;
        }
        int root_val = preorder[p_start];
        TreeNode root = new TreeNode(root_val);
        int i_root_index = 0;
        for(int i=0;i<inorder.length;i++){
            if(root_val == inorder[i]){
                i_root_index = i;
                break;
            }
        }
        int left_num = i_root_index - i_start;
        root.left = buildTreeHelper(preorder,p_start+1,p_start+left_num+1,inorder,i_start,i_root_index-1);
        root.right = buildTreeHelper(preorder,p_start+left_num+1,p_end,inorder,i_root_index+1,i_end);
        return root;

    }
}
```

