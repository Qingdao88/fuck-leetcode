---
title: 3. 无重复字符的最长子串
date: 2025-01-04
tags:
  - 滑动窗口
---

### 问题描述

[题目链接](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/)

在字符串中找到一个最长的不含重复字符的子串，返回它的长度。

### 解题思路

#### 方法一

`hashMap` 用于记录每个字符最后一次出现的位置，`left` 则表示当前滑动窗口的左边界。在每次循环中，我们都需要更新当前字符在 `hashMap` 中的位置，并计算以该字符为右边界的窗口大小是否需要更新 `ans`。如果遇到重复的字符，左边界 `left` 会尝试着更新为该字符上一次出现位置的右一位。更新左边界的条件是：新的左边界位置必须比当前的 `left` 更右，若没有更右的位置，则不更新。

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> hashMap = new HashMap<>();
        int ans = 0;
        int left = 0;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (hashMap.containsKey(c)) {
                left = Math.max(left, hashMap.get(c) + 1);
            }
            hashMap.put(c, i);
            ans = Math.max(ans, i - left + 1);
        }
        return ans;
    }
}
```

**算法复杂度分析：**

假设：`n` 是字符串 `s` 的长度，`m` 是不同字符的数量。

时间复杂度：$O(n)$

空间复杂度：$O(min(n, m))$
