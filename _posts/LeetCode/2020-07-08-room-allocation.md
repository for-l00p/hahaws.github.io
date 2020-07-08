---
layout: default
title: 162. find-peak-element
tags: LeetCode
---

## Room Allocation

### Description

[Problem Address](https://cses.fi/problemset/task/1164)

There is n customers to hotel. We know that every customer arrive time and leave time. The hotel is large enough for every customer single room

input like
```
3
1 2
2 4
4 4
```

Please figure out the maximum room will be used. And every customer's room number.

### 解决方案

```cpp
#include <bits/stdc++.h>
 
#define ar array
 
using namespace std;
 
using ll = long long;
using ull = unsigned long long;
 
const int mxN = 2e5;
 
int n, ans[mxN];    // define variable  n: number of input  ans: answer[room number]
ar<int, 3> a[mxN];  // save input [leave time, in time, order number]
 
int main()
{
    cin >> n;
    for (int i = 0; i < n; ++i)
    {
        cin >> a[i][1] >> a[i][0];
        a[i][2] = i;
    }
    sort(a, a + n); // sort by leave time
    set<ar<int, 2>> s;
    for (int i = 0; i < n; ++i)
    {
        auto it = s.lower_bound({a[i][1]}); //find leave time >= in time
        if (it != s.begin())    // has room is not used (last customer is leaved)
        {
            --it;   // move to the empty room
            ans[a[i][2]] = (*it)[1]; // allocate empty room to custom
            s.erase(it);
        }
        else
            ans[a[i][2]] = s.size();    // allocate new room
        s.insert({a[i][0], ans[a[i][2]]});
    }
    cout << s.size() << "\n";
    for (int i = 0; i < n; ++i)
        cout << ans[i] + 1 << " ";
}

```
