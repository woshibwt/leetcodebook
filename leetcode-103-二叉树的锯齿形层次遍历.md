给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 [3,9,20,null,null,15,7]

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20201006142104.png)

返回锯齿形层次遍历如下：

![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20201006142159.png)



## 解题思路

与[leetcode 102题](leetcode-102-二叉树的层次遍历.md)本质上相同，只是增加一个标志位flag,每次翻转来影响节点入list的顺序

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = null;
        if(root==null){
            return res;
        }
        int flag = 1;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        while(!queue.isEmpty()){
            int size = queue.size();
            list = new ArrayList<>();
            while(flag==1 && size>0){
                TreeNode curr = queue.poll();
                list.add(curr.val);
                if(curr.left!=null){
                    queue.offer(curr.left);
                }
                if(curr.right!=null){
                    queue.offer(curr.right);
                }
                size --;
            }
            while(flag==-1 && size>0){
                TreeNode curr = queue.poll();
                list.add(0,curr.val);
                if(curr.left!=null){
                    queue.offer(curr.left);
                }
                if(curr.right!=null){
                    queue.offer(curr.right);
                }
                size --;
                
            }
            res.add(list);
            flag *= -1;
        }
        return res;

    }
}
```