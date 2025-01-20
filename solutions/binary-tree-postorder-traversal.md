---
title: 145. 二叉树的后序遍历
date: 2025-01-21
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/binary-tree-postorder-traversal/description/)

后序遍历一颗树：左子树 -> 右子树 -> 根节点。

### 解题思路

#### 方法一

递归法。

```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        postorderTraversal(root, ans);
        return ans;
    }

    public void postorderTraversal(TreeNode node, List<Integer> ans) {
        if (node == null) {
            return;
        }
        postorderTraversal(node.left, ans);
        postorderTraversal(node.right, ans);
        ans.add(node.val);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$
