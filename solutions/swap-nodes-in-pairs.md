---
title: 24. 两两交换链表中的节点
date: 2025-01-15
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/swap-nodes-in-pairs/description/)

把链表中的节点两两交换。

### 解题思路

#### 方法一

使用三个指针：`left`、`right` 和 `leftPrev`，调整它们的 `next` 指向。在动手操作之前，先在纸上模拟，确保逻辑清晰无误后再写代码。

```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(Integer.MAX_VALUE, head);
        ListNode leftPrev = dummy;
        ListNode left = dummy.next;
        ListNode right = left.next;
        while (true) {
            leftPrev.next = right;
            left.next = right.next;
            right.next = left;

            leftPrev = left;
            left = left.next;
            if (left == null) {
                break;
            }
            right = left.next;
            if (right == null) {
                break;
            }
        }
        return dummy.next;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
