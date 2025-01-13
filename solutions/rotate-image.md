---
title: 48. 旋转图像
date: 2025-01-13
tags:
  - 矩阵
---

### 问题描述

[题目链接](https://leetcode.cn/problems/rotate-image/description/)

把二维数组右旋 90 度。

### 解题思路

#### 方法一

变量 i 用于处理矩阵的每一环，从外到内遍历。当矩阵的中心只有一个元素时，无需进一步处理。变量 j 则负责处理每一列的元素。

借助 AI 工具，将矩阵的初始数据和对应下标以图示的形式列出，同时观察每一层元素的数据变化过程。在表示变化时，用变量代替数值。

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        for (int i = 0; i < n / 2; i++) {
            for (int j = 0; j < (n + 1) / 2; j++) {
                int tmp = matrix[i][j]; // 0, 0 1
                matrix[i][j] = matrix[n - 1 - j][i];
                matrix[n - 1 - j][i] = matrix[n - 1 - i][n - 1 - j];
                matrix[n - 1 - i][n - 1 - j] = matrix[j][n - 1 - i];
                matrix[j][n - 1 - i] = tmp;
            }
        }
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n^2)$

空间复杂度：$O(1)$
