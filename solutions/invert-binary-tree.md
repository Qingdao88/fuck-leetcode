---
title: 226. 翻转二叉树
date: 2025-01-22
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/invert-binary-tree/description/)

把二叉树的左子树和右子树交换一下位置。

### 解题思路

#### 方法一

递归。

首先要解决如何交换左右子节点的问题。这与交换两个整数类似，需要借助一个临时变量 `tmp`。目前，我们只是解决了交换根节点左右子树的问题，但还需要进一步解决每个子树左右子节点的交换。递归的退出条件可以明确为当前节点为 `null` 时。对于每个子节点，先交换其左右子节点，然后将当前节点返回给上一级。

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        if (root == null) {
            return null;
        }
        TreeNode tmp = root.left;
        root.left = invertTree(root.right);
        root.right = invertTree(tmp);
        return root;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
