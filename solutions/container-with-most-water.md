---
title: 11. 盛最多水的容器
date: 2025-01-03
tags:
  - 双指针
---

### 问题描述

[题目链接](https://leetcode.cn/problems/container-with-most-water/description/)

找到两条线，使得这两条线与 x 轴构成的长方形面积最大。

### 解题思路

#### 方法一

此方法借鉴自 Krahets 的[题解](https://leetcode.cn/problems/container-with-most-water/solutions/11491/container-with-most-water-shuang-zhi-zhen-fa-yi-do)。

盛水的面积取决于较短的那一边，无论较长的那一边有多长，水都会从较短的边溢出。

因此，盛水的面积可以表示为：$盛水面积 = 两个板之间的距离 \times 较短的板高度$。

使用两个指针 `i` 和 `j`，其中 `i` 从最左边向右扫描，`j` 从最右边向左扫描。计算完当前的盛水面积后，移动较短的板，因为移动短板有可能找到更高的板，从而使盛水面积增大，当然也有可能不变或变小。如果移动较长的板，由于盛水面积取决于较短的板，因此面积不会增大，甚至可能减少，即使找到更长的板也没有意义。

```java
class Solution {
    public int maxArea(int[] height) {
        int i = 0;
        int j = height.length - 1;
        int ans = 0;
        while (i < j) {
            int minHeight = Math.min(height[i], height[j]);
            int area = minHeight * (j - i);
            ans = Math.max(ans, area);
            if (height[i] > height[j]) {
                j--;
            } else {
                i++;
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$

### 刷题反思

1. 一个半月没刷题了，好在我的算法思维还健在，我还记得些算法，赶紧复习！不要让它们彻底遗忘！
2. 写题解是有意义的，它能迫使我理清算法思想。
