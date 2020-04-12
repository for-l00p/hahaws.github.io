# 二分搜索

二分搜索（binary search），也称折半搜索（half-interval search）、对数搜索（logarithmic search），是一种在有序数组中查找某一特定元素的搜索算法

## 详解

二分搜索使用的前提条件是数组是**有序数组**

搜索过程从中间开始，如果中间元素小于目标元素，则在前半部分搜索，如果中间元素大于目标元素，则在后半部分搜索，中间元素等于目标元素就代表找到

### 计算步骤

```
// 伪代码
start = 0, end = size - 1;

if (start > mid) return false
mid = start + (end - start) / 2
if (mid == target) 
    return mid
else if (mid < target)
    start = mid + 1
else
    end = mid - 1
```

算法很好理解，代码也很简单

但是其中有一个细节就是使用`mid = start + (end - start) / 2`而不是`mid = (start + end) / 2`的原因就是如果范围很大，那么有可能start+end的值超过了mid类型能表示的最大值，也就是溢出了，这样程序可能报错，也可能得不到想要的结果

### 代码示例

既可以用递归的方法写，也可以用循环的方法写

```cpp
// 递归
int binarySearch(vector<int>& nums, int start, int end, int target)
{
    if(end > start) return -1;
    int mid = start + (end - start) / 2;
    if (nums[mid] == target)
        return mid;
    else if (nums[mid] < target)
        return binarySearch(nums, mid + 1, end, target);
    else
        return binarySearch(nums, start, mid - 1);
}
```

```cpp
// 循环
int binarySearch(vector<int>& nums, int target)
{
    int start = 0, end = nums.size() - 1, ans = -1;
    while (start <= end)
    {
        int mid = start + (end - start) / 2;
        if (nums[mid] < target)
            start = mid + 1;
        else if (nums[mid] > target)
            end = mid - 1;
        else
            ans = mid;
            break;
    }
    return ans;         // 程序唯一出口
}
```

### 复杂度分析

每次都把搜索范围缩小一半，时间复杂度O(logn)

空间复杂度O(1), 尾递归可以改成循环

## 重点

**二分查找的思路是很简单的，但是其中一些细节是在写代码时要时时刻刻注意，出错时检查一下是否少了个等号，或者mid是否正确改变**

发明KMP算法的大佬是这么说的

> Although the basic idea of binary search is comparatively straightforward, the details can be surprisingly tricky

> 尽管二分查找的基本思路想读简单，但是其中的一些细节却非常棘手
