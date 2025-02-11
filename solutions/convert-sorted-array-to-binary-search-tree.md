---
title: 108. 将有序数组转换为二叉搜索树
date: 2025-02-11
tags:
  - 二叉树
---

### 问题描述

[题目链接](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/description/)

从一个有序数组构建出一颗二叉搜索树。

### 解题思路

#### 方法一

递归地找数组的中点。

可以通过以下步骤理解这个算法的自然演化：

二叉搜索树的性质：
1. 左子树的所有节点值都比该节点小。
2. 右子树的所有节点值都比该节点大。

当数组中的元素按升序排列时，利用中间的元素作为根节点可以保持二叉搜索树的性质。

平衡二叉树的性质：树的高度应该尽可能小，因为树的高度越低，查找、插入和删除操作的时间复杂度就越小。所以，树的左右子树的大小应尽可能相等。

选取数组的中间元素作为根节点，能够平衡左右两侧的元素数目大致相同（保证树的平衡性），又可以保持二叉搜索树的性质。

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return sortedArrayToBST(nums, 0, nums.length - 1);
    }

    public TreeNode sortedArrayToBST(int[] nums, int left, int right) {
        if (right < left || left >= nums.length) {
            return null;
        }
        int mid_val_index = left + ((right - left) >> 1);
        int mid_val = nums[mid_val_index];
        TreeNode node = new TreeNode(mid_val);
        node.left = sortedArrayToBST(nums, left, mid_val_index - 1);
        node.right = sortedArrayToBST(nums, mid_val_index + 1, right);
        return node;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
