---
title: 560. 和为 K 的子数组
date: 2025-01-10
tags:
  - 前缀数组
---

### 问题描述

[题目链接](https://leetcode.cn/problems/subarray-sum-equals-k/description/)

在数组中找到所有和为 k 的子数组（连续的序列），返回个数。

### 解题思路

#### 方法一

此方法借鉴自该[题解](https://leetcode.cn/problems/subarray-sum-equals-k/solutions/2794955/qing-xi-de-tu-shi-tui-dao-by-shawxing-kw-crp3)。

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        HashMap<Integer, Integer> prefixSum = new HashMap<>();
        int sum = 0;
        int ans = 0;
        prefixSum.put(0, 1);
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            if (prefixSum.containsKey(sum - k)) {
                ans += prefixSum.get(sum - k);
            }
            prefixSum.put(sum, prefixSum.getOrDefault(sum, 0) + 1);
        }
        return ans;
    }
}
```

给键的值 +1 的代码可以被优化为：

```java
prefixSum.merge(sum, 1, Integer::sum);
```

`merge` 方法的作用：
- 如果 `prefixSum` 中不存在 `sum`，则插入新键值对 `sum -> 1`。
- 如果 `prefixSum` 中已存在 `sum`，则调用合并函数：取出 `prefixSum` 中键 `sum` 对应的旧值 `oldValue`。调用 `Integer::sum` 方法，计算 `oldValue + 1`，返回结果作为新值存储到 `prefixSum` 的键 `sum` 中，替换旧值。

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$
