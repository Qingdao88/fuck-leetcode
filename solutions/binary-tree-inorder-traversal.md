---
title: 94. 二叉树的中序遍历
date: 2025-01-20
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/binary-tree-inorder-traversal/description/)

中序遍历一颗树：左子树 -> 根节点 -> 右子树。

### 解题思路

#### 方法一

递归法。

1. **一直往左走**：不断递归访问左子节点，直到到达 `null`（即没有左子节点）。
2. **往前走不动了（左子树走到底）**：当前节点没有左子节点时，处理当前节点（打印或存储节点值）。
3. **往右走**：开始递归访问当前节点的右子树时，同样从右子树的左节点开始处理。

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        inorderTraversal(ans, root);
        return ans;
    }

    public void inorderTraversal(List<Integer> ans, TreeNode node) {
        if (node == null) {
            return;
        }
        inorderTraversal(ans, node.left);
        ans.add(node.val);
        inorderTraversal(ans, node.right);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
