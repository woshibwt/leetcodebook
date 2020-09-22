给定一个二叉树，判断其是否是一个有效的二叉搜索树。
        假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含小于当前节点的数。

- 节点的右子树只包含大于当前节点的数。

- 所有左子树和右子树自身必须也是二叉搜索树。  

示例 1:

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/验证二叉搜索树.PNG)



示例 2:

输入:

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/验证二叉搜索树2.PNG)  

  输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
  根节点的值为 5 ，但是其右子节点值为 4 。

  # 思路

考察二叉搜索树的特征：将二叉搜索树中序遍历则为升序。

因此做一个简单的中序遍历，在进行中序遍历时，判断当前节点是否大于中序遍历的前一个节点，如果当前节点的值大于前一个节点的值，则满足BST，将代表之前的变量pre赋值为该节点，否则直接返回false

```java
class Solution {
     int pre = Integer.MIN_VALUE;
    public boolean isValidBST(TreeNode root) {
        if(root == null) return true;
        if(!isValidBST(root.left)) return false;
        if(root.val<=pre) return false;
        pre = root.val;
        return isValidBST(root.right);
	}

}
```
## java中各类型的最小最大值

注意到该题中使用了类型最小值来作为curr变量的初始值，最常使用到的是Integer类型下的MAX和MIN,格式为```Integer.Max_VALUE,Integer.MIN_VALUE```
![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/最大最小值.PNG)
        而测试用例中（69/75）使用了[-2147483648]，是MIN_VALUE的值,导致了无法通过。因此初始值开到了Long.MIN_VALUE,不同类型下MAX和MIN格式是相通的

