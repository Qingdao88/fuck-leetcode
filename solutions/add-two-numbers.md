---
title: 2. 两数相加
date: 2025-01-14
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/add-two-numbers/description/)

两个链表代表两个数，它们以逆序的方式给出，把这两个数加起来，结果也要是逆序的。

### 解题思路

#### 方法一

模拟加法，注意进位。

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode ansList = null;
        ListNode ansListHead = null;
        int carry = 0;
        while (l1 != null || l2 != null) {
            int l1Val = l1 != null ? l1.val : 0;
            int l2Val = l2 != null ? l2.val : 0;
            int sum = carry + l1Val + l2Val;
            carry = sum / 10;
            int val = sum % 10;
            if (ansList == null) {
                ansList = new ListNode(val);
                ansListHead = ansList;
            } else {
                ansList.next = new ListNode(val);
                ansList = ansList.next;
            }
            l1 = l1 != null ? l1.next : null;
            l2 = l2 != null ? l2.next : null;
        }
        if (carry != 0) {
            ansList.next = new ListNode(carry);
        }
        return ansListHead;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
