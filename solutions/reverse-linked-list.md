---
title: 206. 反转链表
date: 2025-01-16
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/reverse-linked-list/description/)

反转链表的顺序，下一个节点指向当前节点。

### 解题思路

#### 方法一

从头节点开始逐步改变每个节点的 `next` 指针指向前一个节点。

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode prevNode = null;
        ListNode currNode = head;
        while (currNode != null) {
            ListNode nextNode = currNode.next;
            currNode.next = prevNode;
            prevNode = currNode;
            currNode = nextNode;
        }
        return prevNode;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
