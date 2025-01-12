---
title: 76. 最小覆盖子串
date: 2025-01-11
tags:
  - 滑动窗口
---

### 问题描述

[题目链接](https://leetcode.cn/problems/minimum-window-substring/description/)

在字符串 `s` 里，找出包含字符串 `t` 中所有字符的最短子字符串。

不在乎字符出现的顺序，参杂别的字符也行。

### 解题思路

#### 方法一

使用双指针 `left` 和 `right` 来构建一个滑动窗口。首先，`right` 指针向右移动，尽可能扩展窗口，直到窗口满足条件。一旦满足条件，就停止扩展，因为目标是找到最小的子串，继续向右扩展只会使子串变大。尝试缩小窗口的左边界，将可以丢弃的字符移出窗口，直到遇到必须保留的字符。此时，记录窗口的长度，如果比之前记录的最小长度还要小，就更新记录。接下来，右移 `left` 指针，以新的左边界为起点，重复上述步骤，寻找下一个可能的最小子串。

```java
class Solution {
    public String minWindow(String s, String t) {
        int minLen = Integer.MAX_VALUE;
        int ansLeft = -1;
        int ansRight = -1;
        int left = 0;
        int right = 0;
        int sLen = s.length();
        int tLen = t.length();
        int[] need = new int[128];
        for (char c : t.toCharArray()) {
            need[c]++;
        }
        int needCount = tLen;
        while (right < sLen) {
            char rightChar = s.charAt(right);
            if (need[rightChar] > 0) {
                needCount--;
            }
            need[rightChar]--;
            if (needCount == 0) {
                char leftChar = s.charAt(left);
                while (need[leftChar] < 0) {
                    need[leftChar]++;
                    left++;
                    leftChar = s.charAt(left);
                }
                int currStrLen = right - left + 1;
                if (currStrLen < minLen) {
                    ansLeft = left;
                    ansRight = right;
                    minLen = currStrLen;
                }
                need[leftChar]++;
                left++;
                needCount++;
            }
            right++;
        }
        return ansLeft == -1 ? "" : s.substring(ansLeft, ansRight + 1);
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
