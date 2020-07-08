---
layout: default
title: Single Number
tags: Algorithm
---

# Single Number

## Description

Given an vector of number. Every number appears twice times except one. Your task is to find it out.

Your algorithm should be in linear runtime complexity. And try not use extra memory.

### Code

```c++
int singleNumber(vector<int>& nums)
{
    int ans = nums[0];
    for (int i = 1; i < nums.size(); ++i)
        ans ^= nums[i];
    return ans;
}
```

We know thar `a^a=0`

> 10100111 ^ 10100111 = 00000000

> a^b^c^b^a = c

So we can figure it out.