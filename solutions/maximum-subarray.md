---
title: 53. 最大子数组和
date: 2025-01-08
tags:
  - 动态规划
---

### 问题描述

[题目链接](https://leetcode.cn/problems/maximum-subarray/description/)

在数组中寻找连续的一段数，使它们的和最大。

### 解题思路

#### 方法一：动态规划

**`maxEndingHere[i]`** 表示以元素 `nums[i]` 结尾的连续子数组的最大和。

`maxEndingHere[i]` 的值有两种可能：

1. **仅包含自身（`nums[i]`）：**  
    当前面的子数组最大和（`maxEndingHere[i-1]`）为负数时，负数加上当前元素只会让总和变小，前面的最大和对当前子数组是负贡献，即 `maxEndingHere[i-1] + nums[i]` 还不如 `nums[i]` 自身大。
2. **前面的子数组最大和加上当前元素（`maxEndingHere[i-1] + nums[i]`）：**  
    当 `maxEndingHere[i-1]` 为正数时，正数加上当前元素会让总和增加，因此选择将前面的子数组最大和加入当前元素。

你是要甩开别人，还是自己单干？要么加上左边，要么就只算自己。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int[] maxEndingHere = new int[nums.length];
        int ans = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int sumWithPrev = i != 0 ? maxEndingHere[i - 1] + nums[i] : nums[i];
            int currNum = nums[i];
            if (sumWithPrev > currNum) {
                maxEndingHere[i] = sumWithPrev;
            } else {
                maxEndingHere[i] = currNum;
            }
            ans = Math.max(ans, maxEndingHere[i]);
        }
        return ans;
    }
}
```

优化：无需记录数组中以每个元素结尾的子数组最大和，只需使用一个变量动态记录前一步的最大和，并进行滚动更新即可。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int prevMax = 0;
        int ans = Integer.MIN_VALUE;
        for (int i = 0; i < nums.length; i++) {
            int sumWithPrev = prevMax + nums[i];
            int currNum = nums[i];
            int maxEndingHere = sumWithPrev > currNum ? sumWithPrev : currNum;
            ans = Math.max(ans, maxEndingHere);
            prevMax = maxEndingHere;
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
