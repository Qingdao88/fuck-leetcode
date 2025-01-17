---
title: 234. 回文链表
date: 2025-01-17
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/palindrome-linked-list/description/)

判断链表从左往右读和从右往左读是否一样。

### 解题思路

#### 方法一

1. 找到链表中点
2. 反转从中点开始到链表末尾的后半部分
3. 比较前半部分与反转后的后半部分
4. 恢复后半部分的指向

```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head.next == null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode prevNode = null;
        ListNode currNode = slow;
        while (currNode != null) {
            ListNode nextNode = currNode.next;
            currNode.next = prevNode;
            prevNode = currNode;
            currNode = nextNode;
        }
        ListNode left = head;
        ListNode right = prevNode;
        while (left != null) {
            if (left.val != right.val) {
                return false;
            }
            left = left.next;
            right = right.next;
        }
        currNode = prevNode;
        prevNode = null;
        while (prevNode != slow) {
            ListNode nextNode = currNode.next;
            currNode.next = prevNode;
            prevNode = currNode;
            currNode = nextNode;
        }
        return true;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
