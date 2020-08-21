---
title: LeetCode 96 不同的二叉搜索树
date: 2020-07-08 16:11:00
tags:
- 二叉树
- 树
- 动态规划
categories: leetcode
top: 20
copyright: true
---
给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？  
**示例:**
![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/example.PNG)

## 思路
&emsp;假设n个节点存在二叉排序树的个数是$G(n)$,令$f(i)$为以$i$为根的二叉搜索树的个数，则：  
$$G(n) = f(1)+f(2)+f(3)+f(4)+...+f(n)$$
&emsp;当$i$为根节点时，其左子树节点个数为$i-1$个，右子树节点为$n-i$个，则：
$$f(i) = G(i-1)*G(n-i)$$
&emsp;综合可得卡特兰数的公式：
$$G(n) = G(0)*G(n-1) + G(1)*G(n-2)+...+G(n-1)*G(0)$$

```
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;

        for(int i=2;i<n+1;i++){
            for(int j = 1;j<i+1;j++){
                dp[i] += dp[j-1] * dp[i-j];
            }
        }
        return dp[n];

    }
}
```