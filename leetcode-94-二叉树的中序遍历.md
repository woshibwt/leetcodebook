---
title: LeetCode 94 二叉树的中序遍历
date: 2020-07-06 23:07:00
tags:
- 二叉树
- 树
categories: leetcode
top: 10
copyright: true
mathjax: true
---
给定一个二叉树，返回它的中序 遍历。

示例:


![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/example.PNG)


进阶: 递归算法很简单，你可以通过迭代算法完成吗？  

## 递归法
首先最简单的方法当然是递归：
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List <Integer> res = new ArrayList<>();
        helper(root,res);
        return res;
    }
    public void helper(TreeNode root,List<Integer> res){
        if(root!=null){
            if(root.left!=null){
                helper(root.left,res);
            }
            res.add(root.val);
            if(root.right!=null){
                helper(root.right,res);
            }
        }
    }
}b

```
在`inorderTraversal`函数中定义了一个**Integer**类型的List,通过递归`helper()`函数,在递归访问完当前节点的左右子树的中间将节点的值加入到List中。

## 迭代法
&emsp;根据中序遍历的顺序，对于任一几点，优先访问其左孩子，而左孩子又可以看成一根节点，然后继续访问其左孩子节点，直到左孩子节点为空的节点才结束访问，然后按照同样的规则访问右子树。其处理过程如下：  
&emsp;对于任一节点curr:  
1)若其左孩子不为空，则将curr入栈并将它的左孩子置为新的curr,然后对新的curr执行新的处理  
2)若其左孩子为空，则取栈顶元素并进行出栈操作，访问该栈顶结点(`res.add(curr.val)`)，然后将栈顶节点的右孩子置为新的curr  
3)直到curr为NULL和栈为空时结束。
```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List <Integer> res = new ArrayList<>();
        Stack <TreeNode> stack =  new Stack <>();
        TreeNode curr = root;
        while(curr!=null||!stack.isEmpty()){
            while(curr != null){
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;

    }
}
```
## ArrayList简单介绍
&emsp;编程的时候存储多个数据时，长度固定的数组不一定能满足需求，此时选择**集合**，其提供了一种存储空间可变的存储模型，存储的数据容量可以改变，其中一个就是**ArrayList**。
### ArrayList<E>:
- 底层是可调整大小的数组实现
- <E>是特殊的数据类型，泛型。
### ArrayList构造方法和添加方法
![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/ArrayList方法.PNG)

### ArrayList常用方法
![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/Arraylist常用方法.PNG)
