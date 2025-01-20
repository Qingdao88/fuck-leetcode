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

空间复杂度：$O(h)$

#### 方法二

用栈模拟递归。

1. **向左遍历：** 如果当前节点不为空，将节点压入栈并持续移动到左子节点。
2. **弹出栈顶：** 若当前节点为空，说明左子树已遍历完，从栈中弹出节点（访问它的值）并转向右子树。
3. **重复过程：** 通过循环反复执行上述步骤，直至栈为空且当前节点为空。

```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<>();
        List<Integer> ans = new ArrayList<>();
        TreeNode currNode = root;
        while (!stack.isEmpty() || currNode != null) {
            if (currNode != null) {
                stack.push(currNode);
                currNode = currNode.left;
            } else {
                TreeNode parentNode = stack.pop();
                currNode = parentNode.right;
                ans.add(parentNode.val);
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(h)$，其中 `h` 是树的高度，最坏为 `O(n)`，退化为链表的树，最好为完全平衡的二叉树，高度 `h = log(n)`。

