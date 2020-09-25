给你一个二叉树，请你返回其按 **层序遍历** 得到的节点值。 （即逐层地，从左到右访问所有节点）。

## 示例

二叉树：`[3,9,20,null,null,15,7]`



![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20200925085256.png)

返回其层次遍历结果：



![](https://bwtpicturehouse.oss-cn-shanghai.aliyuncs.com/img/20200925085659.png)

## 思路

很典型的bfs的应用，使用一个队列，bfs的模板如下：

```java
void bfs(TreeNode root) {
    Queue<TreeNode> queue = new ArrayDeque<>();
    queue.add(root);
    while (!queue.isEmpty()) {
        TreeNode node = queue.poll(); // Java 的 pop 写作 poll()
        if (node.left != null) {
            queue.add(node.left);
        }
        if (node.right != null) {
            queue.add(node.right);
        }
    }
}
```

而对于这道题，需要在每一层遍历开始前，使用一个变量来记录队列中的数量n(对应这一层的节点数量)，然后一口气处理完这一层的n个节点。

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> res = new ArrayList<>();

    Queue<TreeNode> queue = new ArrayDeque<>();
    if (root != null) {
        queue.add(root);
    }
    while (!queue.isEmpty()) {
        int n = queue.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < n; i++) { 
            TreeNode node = queue.poll();
            level.add(node.val);
            if (node.left != null) {
                queue.add(node.left);
            }
            if (node.right != null) {
                queue.add(node.right);
            }
        }
        res.add(level);
    }

    return res;
}

```



其中注意在每一轮遍历前都要将list清空