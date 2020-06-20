---
layout: default
title: 计划递归 (Plan Recursion)
tags: Algorithm
---

# 计划递归 (Plan Recursion)

计划递归是在递归的过程中保存结果避免递归时的重复运算导致的速度过慢

## 示例

大家都知道斐波那契数列

> return fib(i - 1) + fib(i - 2) if i > 1 else 1

用python写就是

```python
def fib(n):
    if n <= 1:
        return 1
    return fib(n -1) + fib(n - 2)
```

跑一下测试速度

参数 | 时间
--- | ---
30 | 238ms
31 | 390ms
32 | 620ms
33 | 1s
34 | 1.63s
35 | 2.64s

可以发现运行时间是呈几何倍数的增长, 因为在函数执行过程中有大量的重复运算

``计划递归``就是可以在递归的过程中保存一些执行过的变量

```python
cache = {}    # 用来保存变量
def fib(n):
    if n in cache.keys():       # 重复计算读取cache
        return cache[n]
    if n <= 1:
        return 1
    cache[n] = fib(n - 1) + fib(n - 2)  # 新值存入cache
    return cache[n]
```

再看一下运行时间

参数 | 时间
--- | ---
34 | 0ms
35 | 0ms
500 | 0ms

虽然实际上是有运行时间的, 但是太快了, 所以显示0ms

由此可以看出计划递归的好处

可以用python装饰器的方法写计划递归

```python
class MyCache(object):

    def __init__(self, func):
        self.func = func
        self.cache = {}

    def __call__(self, *args):
        if args not in self.cache.keys():
            self.cache[args] = self.func(*args)
        return self.cache[args]

@MyCache
def fib(n):
    if n <= 1:
        return 1
    return fib(n - 1) + fib(n - 2)

print(fib(35))
```
