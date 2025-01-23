---
title: 101. 对称二叉树
date: 2025-01-23
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/symmetric-tree/description/)

判断一颗二叉树的左子树和右子树是否一样。

### 解题思路

#### 方法一

首先，检查根节点的左右子节点是否具有相同的值。然后，算法递归地将左子树的左孩子与右子树的右孩子进行比较，并继续向下比较左子树的左孩子与右子树的右孩子，直到遍历到叶节点为止。若所有对应的节点值均相同，算法会回退并比较左子树的右孩子与右子树的左孩子。

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return isSymmetric(root.left, root.right);
    }

    public boolean isSymmetric(TreeNode tree1, TreeNode tree2) {
        if (tree1 == null && tree2 == null) {
            return true;
        }
        if (tree1 != null && tree2 != null) {
            return tree1.val == tree2.val && isSymmetric(tree1.left, tree2.right) && isSymmetric(tree1.right, tree2.left);
        }
        return false; // tree1 或 tree2 有一个为 null，另一个不为 null 的情况
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$，需要遍历树中的每一个节点来检查其对称性。

空间复杂度：$O(h)$，由递归调用栈的深度决定。
- 最佳情况下（即平衡二叉树），树的高度为 $O(log n)$，因此递归调用的深度也是 $O(log n)$。
- 最坏情况下（即极度不平衡的二叉树，如链式结构），树的高度为 $O(n)$，递归调用的深度也会达到 $O(n)$。
