---
title: 49. 字母异位词分组
date: 2025-01-01
tags:
  - 哈希表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/group-anagrams/description/)

字母异位词 = 字符串的长度相同，组成字符串的字母个数也相同，只是排列的顺序不同。

边界条件：

1. 数组中的元素数量范围为 1 到 10000
2. 字符串长度范围为 0 到 100
3. 字符串仅包含 26 个小写字母

### 解题思路

#### 方法一

判断字母异位词的方法：

1. 判断字符串的长度是否相同
2. 判断字母的个数是否相同

**解题步骤：**

1. 遍历字符串数组中的每个元素
2. 将每个字符串按照字母表的顺序进行排序
3. 检查哈希表中是否已存在排序后的字符串作为键：
	- 如果不存在，就将该键添加到哈希表中，并将其值初始化为一个新的数组，同时将原始未排序的元素添加到该数组中
	- 如果已存在，则直接将原始元素添加到对应的值数组中

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> hashMap = new HashMap<>();
        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String sortedStr = new String(chars);
            if (!hashMap.containsKey(sortedStr)) {
                hashMap.put(sortedStr, new ArrayList<>());
            }
            hashMap.get(sortedStr).add(str);
        }
        return new ArrayList<>(hashMap.values());
    }
}
```

哈哈，我真是个小天才，解题思路全是我自己想出来的！有点小开心~

**算法复杂度分析：**

假设数组中有 n 个字符串，每个字符串的平均长度为 k。

时间复杂度：$O(n \times (k \log k))$

空间复杂度：$O(n \times k)$

### 刷题反思

1. 对 Java 容器 API 的掌握还不够熟练
2. 对算法复杂度分析的理解还不够透彻
