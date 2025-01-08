---
title: 189. 轮转数组
date: 2025-01-08
tags:
  - 找规律
---

### 问题描述

[题目链接](https://leetcode.cn/problems/rotate-array/description/)

将数组元素向后移动，若超出边界，则从头开始循环。

不要用额外的空间，就原地操作。

### 解题思路

#### 方法一

这个[视频](https://www.bilibili.com/video/BV12g411p7CC/)的讲解做得是真好，我可以借鉴他的方式——用 iPad + Apple Pencil 来制作题解视频。

对于数组 `1, 2, 3, 4, 5, 6, 7`，当 `k = 3` 时，可以将数组分为两部分：`1, 2, 3, 4` 和 `5, 6, 7`。最终结果是：`5, 6, 7` 和 `1, 2, 3, 4`。那么如何得出这个结果呢？通过观察结果数组和原数组之间的规律可以发现，这一过程包括两个步骤：首先将整个数组反转，然后再分别对两个部分进行反转，从而得到最终结果。

```java
class Solution {
    public void rotate(int[] nums, int k) {
        if (k == 0) {
            return;
        }
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    private void reverse(int[] nums, int left, int right) {
        while (left < right) {
            int temp = nums[left];
            nums[left] = nums[right];
            nums[right] = temp;
            left++;
            right--;
        }
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(1)$
