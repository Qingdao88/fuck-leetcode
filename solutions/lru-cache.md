---
title: 146. LRU 缓存
date: 2025-01-16
tags:
  - 链表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/lru-cache/description/)

实现 LRU 数据结构。

### 解题思路

#### 方法一

采用哈希表与双向链表结合的方式实现了 LRU（最近最少使用）缓存策略。利用哈希表可以在 O(1) 时间内定位缓存中的节点，而双向链表则用来维护节点的访问顺序：每次通过 `get` 或 `put` 操作访问到某个节点时，都会将这个节点移动到链表的头部，表明它是最近被使用的；当缓存达到最大容量时，链表尾部的节点（也就是最长时间未被访问的节点）会被移除，从而为新的数据腾出空间。

```java
class LRUCache {

    public class Node {
        Node prev;
        Node next;
        int key;
        int val;

        Node(Node prev, Node next, int key, int val) {
            this.prev = prev;
            this.next = next;
            this.key = key;
            this.val = val;
        }
    }

    Node head;
    Node tail;
    int capacity;
    HashMap<Integer, Node> map;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        head = null;
        tail = null;
    }

    public int get(int key) {
        if (!map.containsKey(key)) {
            return -1;
        }
        Node node = map.get(key);
        moveNodeToHead(node);
        return node.val;
    }

    private void moveNodeToHead(Node node) {
        if (head == tail) {
            return;
        }
        removeNode(node);
        node.next = head;
        head.prev = node;
        head = node;
    }

    private void removeNode(Node node) {
        Node prevNode = node.prev;
        Node nextNode = node.next;
        if (prevNode != null) {
            prevNode.next = nextNode;
        } else {
            head = nextNode;
        }
        if (nextNode != null) {
            nextNode.prev = prevNode;
        } else {
            tail = prevNode;
        }
        node.next = null;
        node.prev = null;
    }

    public void put(int key, int value) {
        if (head == null && tail == null) { // 如果为空
            Node node = new Node(null, null, key, value);
            head = node;
            tail = node;
            map.put(key, node);
            return;
        }
        Node node = map.getOrDefault(key, null);
        if (node != null) { // 如果已存在
            node.val = value;
            moveNodeToHead(node);
        } else { // 如果不存在
            if (map.size() + 1 > capacity) {
                Node tailPrev = tail.prev;
                map.remove(tail.key);
                removeNode(tail);
                tail = tailPrev;
            }
            node = new Node(null, head, key, value);
            if (head != null) {
                head.prev = node;
                head = node;
            } else {
                head = node;
                tail = node;
            }
            map.put(key, node);
        }
    }

}
```

**算法复杂度分析：**

时间复杂度：$O(1)$

空间复杂度：$O(n)$
