---
layout: default
title: xor-queries-of-a-subarray
tags: LeetCode
---

## 1310. xor-queries-of-a-subarray

子数组异或查询

### [题目描述](https://leetcode-cn.com/problems/xor-queries-of-a-subarray/)

### 思路

这题使用前缀和

我们使用pre数组表示arr数组的前缀异或和

已知 `a ^ a = 0`, `a ^ 0 = a`

```
pre[0] = 0
pre[i] = arr[0] ^ arr[1] ^ ... ^ arr[i - 1]

pre[i] ^ pre[j] = (arr[0] ^ ... ^ arr[i - 1]) ^ (arr[0] ^ ... ^ arr[j - 1])
                = (arr[0] ^ ... ^ arr[i - 1]) ^ (arr[0] ^ ... ^ arr[i - 1]) ^ (arr[i] ^ ... ^ arr[j - 1])
                = 0 ^ (arr[i] ^ ... ^ arr[j - 1])
                = arr[i] ^ ... ^ arr[j - 1]
```
所以

arr[i] ^ ... ^ arr[j] = pre[i] ^ pre[j + 1]

### 解决方案

```cpp
class Solution {
public:
    vector<int> xorQueries(vector<int>& arr, vector<vector<int>>& queries) {
        vector<int> pre(arr.size() + 1);
        for (int i = 1; i <= arr.size(); ++i)
        {
            pre[i] = pre[i - 1] ^ arr[i - 1];
        }
        vector<int> ans;
        for (auto que: queries)
        {
            ans.push_back(pre[que[0]] ^ pre[que[1] + 1]);
        }
        return ans;
    }
};
```