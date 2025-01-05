---
title: 42. 接雨水
date: 2025-01-05
tags:
  - 前缀数组
---

### 问题描述

[题目链接](https://leetcode.cn/problems/trapping-rain-water/description/)

计算被柱子围起来的洼地能积多少水。

### 解题思路

#### 方法一

首先，从左到右遍历数组，记录每个位置从最左端到当前位置的最高柱子高度。然后，从右到左遍历数组，记录每个位置从最右端到当前位置的最高柱子高度。最后，遍历每一个格子，当前位置能够接纳的雨水量等于其左右两侧最高高度中的较小值减去当前位置的柱子高度。

```java
class Solution {
    public int trap(int[] height) {
        int ans = 0;
        int[] prefixMax = new int[height.length];
        int[] suffixMax = new int[height.length];

        for (int i = 0; i < prefixMax.length; i++) {
            if (i == 0) {
                prefixMax[i] = height[i];
                continue;
            }
            prefixMax[i] = Math.max(prefixMax[i - 1], height[i]);
        }
        for (int i = suffixMax.length - 1; i >= 0; i--) {
            if (i == suffixMax.length - 1) {
                suffixMax[i] = height[i];
                continue;
            }
            suffixMax[i] = Math.max(suffixMax[i + 1], height[i]);
        }

        for (int i = 1; i < height.length - 1; i++) {
            int effectHeight = Math.min(prefixMax[i], suffixMax[i]);
            if (effectHeight > height[i]) {
                ans += effectHeight - height[i];
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
