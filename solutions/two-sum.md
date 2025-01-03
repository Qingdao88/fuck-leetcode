---
title: 1. 两数之和
date: 2025-01-03
tags:
  - 哈希表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/two-sum/description/)

在数组中找到和为 target 的两个数，返回它们的下标。

### 解题思路

#### 方法一

遍历每个元素时，计算 `target - num`，得到与当前数匹配的另一个数。然后在哈希表中查找该数，如果找到，则返回索引；如果找不到，则将当前数作为键、索引作为值，存入哈希表中。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> hashMap = new HashMap<>();
        int[] ans = new int[2];
        for (int i = 0; i < nums.length; i++) {
            int num = nums[i];
            int targetNum = target - num;
            if (hashMap.containsKey(targetNum)) {
                ans[0] = i;
                ans[1] = hashMap.get(targetNum);
                break;
            } else {
                hashMap.put(num, i);
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$

### 刷题反思

1. 一边刷题，一边写题解，记录思绪流。
2. 每天开始刷题的时候，先刷简单题可以帮助快速进入刷题状态。
