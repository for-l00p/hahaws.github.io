---
layout: default
title: Maximum Subarray Sum
tags: Algorithm
---

# Maximum Subarray Sum

## Description

[problem site](https://cses.fi/problemset/task/1643)

There a array of n intergers without sorted.

Find the maximum sum of subarray

## Solve

Assume that the array is [a1, a2, a3, a4, a5]

We assume that the maximum sum of subarray which is end of a[n] is msf,and the maximum sum of hole array is ans.

When array is `[a1]`:

```
msf = a1, ans = a1
```

When array is `[a1, a2]`:

```
msf = max(a2, a2+msf(a1))
ans = max(ans([a1]), msf(a2))
```

So that when arary is `[a1, a2, a3, a4, a5]`:

```
msf = max(a5, a5+msf(a4))
ans = max(ans([a1, a2, a3, a4]), msf(a5))
```

## Code

```c++
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
 
int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    int n;
    cin >> n;
    ll ans = -1e18, msf=-1e18, a;  // -1e18 mean min of long long
    for (int i=0; i < n; ++i)
    {
        cin >> a;
        msf = max(0ll + a, msf + a);    // 0ll+a means convert to long long
        ans = max(ans, msf);
    }
    cout << ans;
    return 0;
}
```