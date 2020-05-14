---
layout: default
title: string-rotation-lcci
tags: LeetCode
---

## 01.09. string-rotation-lcci

字符串轮转

### [题目描述](https://leetcode-cn.com/problems/string-rotation-lcci/)

### 思路

假如`s2`是由`s1`旋转生成的，那么`s2`长度与`s1`相同，且`s1`在`s2+s2`中

s1 = waterbottle，s2 = erbottlewat

s2 + s2 = erbottle`waterbottle`wat

### 解决方案

```cpp
class Solution {
public:
    bool isFlipedString(string s1, string s2) {
        return s1.size() == s2.size() && (s2 + s2).find(s1) != string::npos;
        //string::nops表示是一个常数，表示不存在的位置
    }
};
```

