---
layout: default
title: Two Knights
tags: Algorithm
---

# Two Knights

[problem site](https://cses.fi/problemset/task/1072)

在棋盘上放两匹马，使他们互相之间不会攻击（国际象棋和中国象棋中马的走法是一样的，走日字）

## Solve

首先考虑两匹马总共有几种摆放方式，然后再减去这其中会互相攻击的摆法。

在`k*k`的棋盘中，第一匹马有`k*K`种摆法, 第二匹马就是`k*k-1`种摆法

总共有`(k * k) * (k * k - 1)`种摆法

但是两匹马是相同的, 所以要除以2 也就是 `(k * k) * (k * k - 1) / 2`

两匹马能相互攻击的情况是在`2 * 3`或者`3 * 2`的情况下

所以我们计算棋盘中有多少个`2 * 3`和`3 * 2`

结果就是每个有`(k - 1) * (k - 2)`个, 每个这样的日字马有两种摆放方式, 就是两个对角线摆法

所以棋盘中总共有能够互相攻击的摆法有` 2 * 2 * (k - 1) * (k - 2)`

结果就是 `(k * k) * (k * k - 1) - 4 * (k - 1) * (k - 2)`

## Code

```cpp

#include<bits/stdc++.h>

using namespace std;

using ll = long long int;
using ull = unsigned long long int;

ull n;

int main()
{
    cin >> n;
    for (ull k = 1; k <=n; ++i)
    {
        ll a1 = k*k, a2 = a1*(a1 - 1) / 2;
        if (i > 2)
            a2 = a2 - 4 * (k - 1) * (k - 2);
        cout << a2 << "\n";
    }
}

```
