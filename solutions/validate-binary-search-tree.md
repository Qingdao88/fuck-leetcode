---
title: 98. 验证二叉搜索树
date: 2025-02-24
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/validate-binary-search-tree/description/)

判断一颗树是否是二叉搜索树。

如果一棵树是二叉搜索树，那么它需要满足如下条件：
1. 树中某个节点的值要大于它左子树的所有节点的值。
2. 树中某个节点的值要小于它右子树的所有节点的值。

### 解题思路

#### 方法一

通过递归遍历二叉树，检查每个节点的值是否在合法范围内，并逐步缩小合法范围，然后将更新后的范围传递给下一层，递归验证其左右子树是否也符合合法范围。

```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean isValidBST(TreeNode node, long left, long right) {
        if (node == null) {
            return true;
        }
        return left < node.val && node.val < right && isValidBST(node.left, left, node.val)
                && isValidBST(node.right, node.val, right);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
