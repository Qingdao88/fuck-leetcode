---
title: 144. 二叉树的前序遍历
date: 2025-01-21
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/binary-tree-preorder-traversal/description/)

前序遍历一颗树：根节点 -> 左子树 -> 右子树。

### 解题思路

#### 方法一

递归。

```java
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        preorderTraversal(ans, root);
        return ans;
    }

    public void preorderTraversal(List<Integer> ans, TreeNode node) {
        if (node == null) {
            return;
        }
        ans.add(node.val);
        preorderTraversal(ans, node.left);
        preorderTraversal(ans, node.right);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$
