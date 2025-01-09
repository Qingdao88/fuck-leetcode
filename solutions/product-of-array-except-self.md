---
title: 238. 除自身以外数组的乘积
date: 2025-01-09
tags:
  - 前缀数组
---

### 问题描述

[题目链接](https://leetcode.cn/problems/product-of-array-except-self/description/)

给定一个整数数组 `nums`，返回一个数组 `answer`，其中 `answer[i]` 等于 `nums` 中除 `nums[i]` 外所有元素的乘积。

注意：
1. 算法必须是 $O(n)$ 的。
2. 不能使用除法。

### 解题思路

#### 方法一

1. 首先扫描两遍，计算出前缀乘积数组和后缀乘积数组。
2. 然后遍历数组中的每个元素，$结果数组中的每个元素的值 = 当前位置的前缀乘积 \times 后缀乘积$。

注意：首元素和尾元素要进行特殊处理。

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] prefixProduct = new int[nums.length];
        int product = 1;
        for (int i = 1; i < nums.length; i++) {
            prefixProduct[i] = product * nums[i - 1];
            product = prefixProduct[i];
        }

        int[] suffixProduct = new int[nums.length];
        product = 1;
        for (int i = nums.length - 2; i >= 0; i--) {
            suffixProduct[i] = product * nums[i + 1];
            product = suffixProduct[i];
        }

        int[] ans = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            if (i == 0 || i == nums.length - 1) {
                ans[i] = prefixProduct[i] + suffixProduct[i];
            } else {
                ans[i] = prefixProduct[i] * suffixProduct[i];
            }
        }

        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
