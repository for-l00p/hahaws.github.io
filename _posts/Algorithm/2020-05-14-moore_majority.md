---
layout: default
title: 摩尔投票算法 (Boyer-Moore majority vote algorithm)
tags: Algorithm
---

# 摩尔投票算法 (Boyer-Moore majority vote algorithm)

摩尔投票算法的目的是从一组数中查找大于一半的数

## 核心

对拼消耗

## 思路

我们可以用多方混战的情况来描述思路

每个数就是一个势力, 我们从第一个势力开始向后征服. 遇到相同的势力时, 这个势力的的势力值就增大

遇到不同势力时, 两个势力就发生对拼, 1对1就会同归于尽, 最后剩下的势力就是我们需要的

定义两个值, `base`表示所选的数，`cnt`用来计数

从头开始遍历, 遇到与`base`相同的数`cnt`就加1, 不同的数`cnt`减1

当`cnt`等于0时, 用下一个数替换`base`

## 代码

```cpp
int majorityElement(vector<int>& nums) {
    int base = nums[0], cnt = 1;
    for (int i = 1; i < nums.size(); ++i)
    {
        if (cnt == 0)
            base = nums[i];
        if (nums[i] == base)
            cnt += 1;
        else
            cnt -= 1;
    }

    // 检验是否符合标准(出现次数大于一半)
    // [3, 2, 1] 中没有数大于一半
    // [3, 2, 3, 1] 中没有数大于一半
    cnt = 0;
    for (auto n: nums)
        cnt += n == base ? 1 : 0;
    return cnt > nums.size() / 2 ? base : -1;

}
```

## 复杂度分析

**时间复杂度**: O(n), 只用了两次遍历

**空间复杂度**: O(1), 只使用了两个额外空间

## 总结

摩尔投票算法是极具有针对性的一种算法, 它只适用于**查找数组中出现次数大于数组一半的数**

当数组中不存在这种数时, 最后的`base`就是不是我们所需要的(就像是战场混战中最后出来收割的势力, 不能表示此势力值最大)

所以我们在最后遍历数组, 来判断返回值是否是我们所需