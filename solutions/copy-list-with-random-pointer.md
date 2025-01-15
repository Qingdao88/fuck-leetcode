---
title: 138. 随机链表的复制
date: 2025-01-15
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/copy-list-with-random-pointer/description/)

实现对链表的深拷贝：新链表的结构和指针关系完全复制了原链表，但每个节点的地址与原链表的地址不同。

### 解题思路

#### 方法一

使用哈希表，首先遍历链表一次，构建一个旧节点到新节点的映射。然后，再次遍历原链表，为新链表的节点建立连接。

```java
class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node, Node> oldToNew = new HashMap<>();

        Node currNode = head;
        while (currNode != null) {
            Node newNode = new Node(currNode.val);
            oldToNew.put(currNode, newNode);
            currNode = currNode.next;
        }

        currNode = head;
        while (currNode != null) {
            Node newNode = oldToNew.get(currNode);
            Node oldNodeNext = currNode.next;
            newNode.next = oldToNew.get(oldNodeNext);
            Node randomNode = currNode.random;
            newNode.random = oldToNew.get(randomNode);
            currNode = currNode.next;
        }

        return oldToNew.get(head);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
