---
layout: default
title: 八皇后问题(eight queens)
tags: Algorithm
---

# 八皇后(eight queens)

在 8 * 8 的棋盘上放置8个皇后, 使他们不会互相攻击

> 皇后会攻击同一条线上的单位, 也就是要规避皇后放在同一条横线, 竖线, 两条斜线上

## 详解
采用回溯的思想, 用深度优先搜索

用[0, 7]表示每行上皇后的所在的列

也就是我们要考虑`01234567`的全排列, 然后在其中去掉处于同一斜线的可能

从左往右有15根斜线, 从右往左也有15根斜线

用两个数组表示斜线是否用过

用横坐标与纵坐标的差值表示所在的从左往右的斜线

用横坐标与纵坐标的和表示所在的从右往左的斜线

## Code

```cpp
#include<iostream>
using namespace std;

int sx[15], sy[15], col[8];
int ans;

void dfs(int n)
{
    if (n == 8)
    {
        ans++;
        return;
    }
    for (int i = 0; i < 8; ++i)
    {
        if (!col[i] && !sx[n - i + 7] && !sy[n + i])
        {
            col[i] = 1;
            sx[n - i + 7] = 1;
            sy[n + i] = 1;
            dfs(n + 1);
            col[i] = 0;
            sx[n - i + 7] = 0;
            sy[n + i] = 0;
        }
    }
}

int main()
{
    dfs(0);
    cout << ans;
}

```
