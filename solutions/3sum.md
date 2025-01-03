---
title: 15. 三数之和
date: 2025-01-03
tags:
  - 双指针
---

### 问题描述

[题目链接](https://leetcode.cn/problems/3sum/description/)

在数组中找出所有索引不同且和为 0 的不重复三元素组合。

### 解题思路

#### 方法一

使用三个 `for` 循环找出所有的三元组组合。

排列数组元素的各种组合很简单，问题在于：如何对三元组进行去重呢？

在把三元组添加到 `ans` 中之前，先检查它是否重复，利用 `HashSet` 的性质。

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> ans = new HashSet<>();
        for (int i = 0; i < nums.length - 2; i++) {
            for (int j = i + 1; j < nums.length; j++) {
                for (int k = j + 1; k < nums.length; k++) {
                    if (nums[i] + nums[j] + nums[k] == 0) {
                        List<Integer> triplet = new ArrayList<>(Arrays.asList(nums[i], nums[j], nums[k]));
                        Collections.sort(triplet);
                        if (!ans.contains(triplet)) {
                            ans.add(triplet);
                        }
                    }
                }
            }
        }
        return new ArrayList<>(ans);
    }
}
```

时间复杂度太高了，此算法行不通。

308 / 313 个通过的测试用例

**算法复杂度分析：**

时间复杂度：$O(n^3)$

空间复杂度：$O(n^3)$

#### 方法二

此方法阶借鉴自 Krahets 的[题解](https://leetcode.cn/problems/3sum/solutions/11525/3sumpai-xu-shuang-zhi-zhen-yi-dong-by-jyd)。

首先将数组按从小到大的顺序排序，然后使用三个指针 `i`、`j` 和 `k`。`i` 固定在数组的左端，`j` 从 `i + 1` 开始向右扫描，`k` 从数组的末尾向左扫描。如果三元组的和大于 0，则将 `k` 左移，并跳过所有重复元素；如果三元组的和小于 0，则将 `j` 右移，并跳过所有重复元素。当 `j` 大于或等于 `k` 时，当前扫描结束，`i` 右移，并跳过所有重复的元素。

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int j = i + 1;
            int k = nums.length - 1;
            while (j < k) {
                boolean jMove = false;
                boolean kMove = false;
                if (nums[i] + nums[j] + nums[k] == 0) {
                    ans.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    jMove = true;
                    kMove = true;
                } else if (nums[i] + nums[j] + nums[k] > 0) {
                    kMove = true;
                } else {
                    jMove = true;
                }
                while (j != k && jMove) {
                    j++;
                    if (nums[j] != nums[j - 1]) {
                        jMove = false;
                    }
                }
                while (k != j && kMove) {
                    k--;
                    if (nums[k] != nums[k + 1]) {
                        kMove = false;
                    }
                }
            }
        }
        return ans;
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n^2)$

空间复杂度：$O(n)$

### 刷题反思

1. 边刷题边写题解是不是有点分散注意力？
2. 用 ChatGPT 润色文字表达 YYDS！！
