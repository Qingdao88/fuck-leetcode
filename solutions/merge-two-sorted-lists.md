---
title: 21. 合并两个有序链表
date: 2025-01-15
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/merge-two-sorted-lists/description/)

合并两个升序的链表，合并后的链表也要是升序的。

### 解题思路

#### 方法一

用双指针，将较小的值加入结果链表，并将指向较小值的链表指针向后移动。

```java
class Solution {
    public ListNode mergeTwoLists(ListNode list1, ListNode list2) {
        ListNode head = new ListNode(Integer.MAX_VALUE);
        ListNode currNode = head;
        final int NO_VALUE = Integer.MAX_VALUE;
        while (list1 != null || list2 != null) {
            int list1Val = list1 != null ? list1.val : NO_VALUE;
            int list2Val = list2 != null ? list2.val : NO_VALUE;
            ListNode nextNode = null;
            if (list1Val < list2Val) {
                nextNode = list1;
                list1 = list1.next;
            } else {
                nextNode = list2;
                list2 = list2.next;
            }
            currNode.next = nextNode;
            currNode = currNode.next;
        }
        return head.next;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n + m)$

空间复杂度：$O(1)$
