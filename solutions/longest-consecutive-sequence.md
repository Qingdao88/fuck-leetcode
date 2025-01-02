---
title: 128. 最长连续序列
date: 2025-01-02
tags:
  - 哈希表
---

### 问题描述

[题目链接](https://leetcode.cn/problems/longest-consecutive-sequence/description/)

数组中的数字可以组成多长的连续序列？

要求只能扫描一遍数组。

边界条件：
1. 数组长度为：0 ~ 10,0000
2. 数组中每个数字的取值范围为：-10,0000,0000 ~ 10,0000,0000

### 解题思路

#### 方法一

**解题步骤：**

此方法是我自己想出来的。

遍历数组中的每个数字，对于每个数字，首先检查它的前一个数字是否存在。如果存在，则将当前数字的序列长度设置为前一个数字的序列长度加 1。接着，继续向后查找并更新后续数字的序列长度，使其等于前一个数字的序列长度加 1。

```java
class Solution {  
    public int longestConsecutive(int[] nums) {  
        if (nums.length == 0) {  
            return 0;  
        }  
        HashMap<Integer, Integer> hashMap = new HashMap<>();  
        for (int i = 0; i < nums.length; i++) {  
            int length = 0;  
            int currNum = nums[i];  
            int prevNum = currNum - 1;  
            int nextNum = currNum + 1;  
            if (hashMap.containsKey(prevNum)) {  
                length = hashMap.get(prevNum);  
            }  
            length += 1;  
            hashMap.put(currNum, length);  
            while (hashMap.containsKey(nextNum)) {  
                prevNum = nextNum - 1;  
                hashMap.put(nextNum, hashMap.get(prevNum) + 1);  
                nextNum = nextNum + 1;  
            }  
        }  
        return Collections.max(hashMap.values());  
    }  
}
```

此追溯算法在遇到输入数据特别大的时候行不通。

73 / 78 个通过的测试用例

#### 方法二

**解题步骤：**

此方法借鉴自灵茶山艾府的[题解](https://leetcode.cn/problems/longest-consecutive-sequence/solutions/3005726/ha-xi-biao-on-zuo-fa-pythonjavacgojsrust-whop)。

以当前数字作为序列的起始点，如果前一个数字也在数组中，则跳过，这意味着当前数字在序列的中间部分，而不是序列的起始点，这样找到的序列长度不是最长的。从序列的起点开始查找，就能找到最长的连续序列。

```java
class Solution {  
    public int longestConsecutive(int[] nums) {  
        int ans = 0;  
        HashSet<Integer> hashSet = new HashSet<>();  
        for (int num : nums) {  
            hashSet.add(num);  
        }  
        for (int currNum : hashSet) {  
            if (hashSet.contains(currNum - 1)) {  
                continue;  
            }  
            int nextNum = currNum + 1;  
            while (hashSet.contains(nextNum)) {  
                nextNum += 1;  
            }  
            int length = nextNum - currNum;  
            ans = Math.max(ans, length);  
        }  
        return ans;  
    }  
}
```

中途卡在了最后一个数据规模更大的测试用例。我把灵的代码提交能通过，但是我的代码却超时，于是我把我们的代码丢给 ChatGPT，让它找不同。最终发现，问题出在我遍历的是原数组，而不是已经去除重复元素的 `hashSet`。

**算法复杂度分析：**

时间复杂度：$O(n)$

空间复杂度：$O(n)$

### 刷题反思

1. 要注意容易出错的边界条件。
2. 需要加强 Java 内置数据结构的学习。
3. 这样边刷题边写题解有点耗时，我要思考这样做有没有意义。
4. 记录错误的思路也是很有意义的。
5. 及时把代码的思路解释清楚，否则过一会再回来写就会模糊不清。
