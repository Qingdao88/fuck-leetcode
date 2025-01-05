---
title: 438. 找到字符串中所有字母异位词
date: 2025-01-05
tags:
  - 滑动窗口
---

### 问题描述

[题目链接](https://leetcode.cn/problems/find-all-anagrams-in-a-string/description/)

在字符串 `s` 中，找到所有字符出现次数与字符串 `p` 相同但排列顺序不同的子串，并返回这些子串的起始索引。

### 解题思路

#### 方法一

使用滑动窗口法，利用一个 `HashMap` 记录字符串 `p` 中每个字符的出现次数，另一个 `HashMap` 用于记录当前窗口中每个字符的出现次数。随着窗口向后移动，每次向窗口的后端加入一个新字符的同时，从窗口的前端移除一个字符，然后比较两个 `HashMap` 的内容。

```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> ans = new ArrayList<>();
        if (s.length() < p.length()) {
            return ans;
        }
        int windowSize = p.length();

        HashMap<Character, Integer> pChars = new HashMap<>();
        for (int i = 0; i < p.length(); i++) {
            char c = p.charAt(i);
            pChars.put(c, pChars.getOrDefault(c, 0) + 1);
        }

        HashMap<Character, Integer> windowChars = new HashMap<>();
        for (int i = 0; i < windowSize; i++) {
            char c = s.charAt(i);
            windowChars.put(c, windowChars.getOrDefault(c, 0) + 1);
        }

        for (int i = 0; i <= s.length() - windowSize; i++) {
            if (windowChars.equals(pChars)) {
                ans.add(i);
            }
            if (i == s.length() - windowSize) {
                break;
            }
            char newChar = s.charAt(i + windowSize);
            windowChars.put(newChar, windowChars.getOrDefault(newChar, 0) + 1);

            char currChar = s.charAt(i);
            if (windowChars.get(currChar) == 1) {
                windowChars.remove(currChar);
            } else {
                windowChars.put(currChar, windowChars.get(currChar) - 1);
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
