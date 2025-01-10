---
title: 239. 滑动窗口最大值
date: 2025-01-10
tags:
  - 滑动窗口
---

### 问题描述

[题目链接](https://leetcode.cn/problems/sliding-window-maximum/description/)

滑动窗口每次往右边移动一位，找到滑动窗口每次移动后窗口中的最大值，返回最大值数组。

### 解题思路

#### 方法一

利用双端队列（`Deque`）来维护当前窗口中可能成为最大值的元素下标，从而高效地找到每个窗口的最大值。队首到队尾单调递减，窗口最大值就是队首元素对应在 `nums` 数组中的值。

```java
class Solution {  
    public int[] maxSlidingWindow(int[] nums, int k) {  
        int[] ans = new int[nums.length - k + 1];  
        int ansIndex = 0;  
        Deque<Integer> deque = new ArrayDeque<>();  
        for (int i = 0; i < nums.length; i++) {  
            while (!deque.isEmpty() && nums[deque.peekLast()] <= nums[i]) {  
                deque.removeLast();  
            }  
            deque.add(i);  
            if (deque.peekLast() - k == deque.peek()) {  
                deque.poll();  
            }  
            if (i >= k - 1) {  
                ans[ansIndex++] = nums[deque.peekFirst()];  
            }  
        }  
        return ans;  
    }  
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
