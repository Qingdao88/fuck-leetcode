---
title: 3280. 将日期转换为二进制表示
date: 2025-01-01
tags: 位运算
---

### 问题描述

[题目链接](https://leetcode.cn/problems/convert-date-to-binary/description/)

如何把十进制数字转化为二进制形式？

注意：二进制形式截止到最高位的 1，不要前导 0。

边界条件：无

### 解题思路

#### 方法一

**解题步骤：**

1. 分割字符串。
2. 把字符串转化为十进制数字。
3. 把十进制数字转化为二进制形式。
4. 重新拼成字符串返回。

```java
class Solution {  
    public String convertDateToBinary(String date) {  
        String[] numbers = date.split("-");  
        int year = Integer.parseInt(numbers[0]);  
        int month = Integer.parseInt(numbers[1]);  
        int day = Integer.parseInt(numbers[2]);  
        return String.format("%s-%s-%s", convertDecimalToBinary(year), convertDecimalToBinary(month), convertDecimalToBinary(day));  
    }  
  
    private String convertDecimalToBinary(int decimal) {  
        StringBuffer binaryString = new StringBuffer();  
        while (decimal != 0) {  
            if ((decimal & 1) != 0) {  
                binaryString.append("1");  
            } else {  
                binaryString.append("0");  
            }  
            decimal >>= 1;  
        }  
        return binaryString.reverse().toString();  
    }  
}
```

补充：
1. `Integer.toBinaryString(int i)` 可以把 i 转化为二进制形式的字符串
2. `Integer.toString(int i, int radix)`可以把 i 转化为 radix 形式的字符串

**算法复杂度分析：**

时间复杂度：$O(1)$

空间复杂度：$O(1)$

### 刷题反思

1. 首先要会使用内置的方法，这是最基本的。
2. 内置的方法不仅要熟练使用，而且还要知道如何实现。
3. 一段时间不学算法，就会忘记。
4. 刷过的编程题要经常拿出来复习。
