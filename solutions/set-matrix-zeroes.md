---
title: 73. 矩阵置零
date: 2025-01-12
tags:
  - 矩阵
---

### 问题描述

[题目链接](https://leetcode.cn/problems/set-matrix-zeroes/description/)

如果矩阵中的一个元素为 0，就把这个元素所在的行和列全都设置为 0。

### 解题思路

#### 方法一

首先检查第一行和第一列，如果其中有 0，就用变量记录下来，标记需要将这两行/列设为 0。如果没有 0，则保持原样。接着，检查其他行列，以第一行和第一列作为标志，若对应位置为 0，则将该位置设为 0。最后，遍历第一行和第一列，将它们的标志位全部置为 0。

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int columnLen = matrix.length;
        int rowLen = matrix[0].length;
        boolean rowZero = false;
        for (int i = 0; i < rowLen; i++) {
            if (matrix[0][i] == 0) {
                rowZero = true;
            }
        }
        boolean columnZero = false;
        for (int i = 0; i < columnLen; i++) {
            if (matrix[i][0] == 0) {
                columnZero = true;
            }
        }
        for (int i = 1; i < columnLen; i++) {
            for (int j = 1; j < rowLen; j++) {
                if (matrix[i][j] == 0) {
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }
        for (int i = 1; i < columnLen; i++) {
            if (matrix[i][0] == 0) {
                for (int j = 1; j < rowLen; j++) {
                    matrix[i][j] = 0;
                }
            }
        }
        for (int i = 1; i < rowLen; i++) {
            if (matrix[0][i] == 0) {
                for (int j = 1; j < columnLen; j++) {
                    matrix[j][i] = 0;
                }
            }
        }
        if (columnZero) {
            for (int i = 0; i < columnLen; i++) {
                matrix[i][0] = 0;
            }
        }
        if (rowZero) {
            for (int i = 0; i < rowLen; i++) {
                matrix[0][i] = 0;
            }
        }
    }
}
```

**算法复杂度分析：**

时间复杂度：$O(n^2)$

空间复杂度：$O(1)$
