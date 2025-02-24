---
title: 230. 二叉搜索树中第 K 小的元素
date: 2025-02-24
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/kth-smallest-element-in-a-bst/description/)

在二叉搜索树中找到第 k 小的元素，实际上就是将树中的元素按升序排列，然后取出第 k 个元素。

### 解题思路

#### 方法一

通过中序遍历，每访问一个节点就进行计数，达到指定位置时返回结果。

```java
class Solution {
    private int k;
    private int result;

    public int kthSmallest(TreeNode root, int k) {
        this.k = k;
        inorder(root);
        return result;
    }

    private void inorder(TreeNode node) {
        if (node == null) {
            return;
        }
        inorder(node.left);
        if (--k == 0) {
            result = node.val;
            return;
        }
        inorder(node.right);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
