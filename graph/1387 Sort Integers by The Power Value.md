# 1387 Sort Integers by The Power Value

The power of an integer `x` is defined as the number of steps needed to transform `x` into `1` using the following steps:

- if `x` is even then `x = x / 2`
- if `x` is odd then `x = 3 * x + 1`

For example, the power of x = 3 is 7 because 3 needs 7 steps to become 1 (3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1).

Given three integers `lo`, `hi` and `k`. The task is to sort all integers in the interval `[lo, hi]` by the power value in **ascending order**, if two or more integers have **the same** power value sort them by **ascending order**.

Return the `k-th` integer in the range `[lo, hi]` sorted by the power value.

Notice that for any integer `x` `(lo <= x <= hi)` it is **guaranteed** that `x` will transform into `1` using these steps and that the power of `x` is will **fit** in 32 bit signed integer.

 

**Example 1:**

```
Input: lo = 12, hi = 15, k = 2
Output: 13
Explanation: The power of 12 is 9 (12 --> 6 --> 3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1)
The power of 13 is 9
The power of 14 is 17
The power of 15 is 17
The interval sorted by the power value [12,13,14,15]. For k = 2 answer is the second element which is 13.
Notice that 12 and 13 have the same power value and we sorted them in ascending order. Same for 14 and 15.
```

**Example 2:**

```
Input: lo = 1, hi = 1, k = 1
Output: 1
```

**Example 3:**

```
Input: lo = 7, hi = 11, k = 4
Output: 7
Explanation: The power array corresponding to the interval [7, 8, 9, 10, 11] is [16, 3, 19, 6, 14].
The interval sorted by power is [8, 10, 11, 7, 9].
The fourth number in the sorted array is 7.
```

**Example 4:**

```
Input: lo = 10, hi = 20, k = 5
Output: 13
```

**Example 5:**

```
Input: lo = 1, hi = 1000, k = 777
Output: 570
```

 

**Constraints:**

- `1 <= lo <= hi <= 1000`
- `1 <= k <= hi - lo + 1`



# basic solution

计算 `lo`  -`hi` 中每个数字的 `power`，并把数字和它的 `power` 组成结构体存入数组中，调用 `std::sort` 按照题目要求升序排列，返回第 `k` 个值。

构造数组的时间复杂度是 O(mlogn)，排序的时间复杂度是 O(mlogm)，总的时间复杂度可以看作 O(nlogn)，空间复杂度 O(n)

```c++
class Solution {
public:  
    int getKth(int lo, int hi, int k) {
        if(lo == hi)    return lo;
        vector<dp> v;
       for(int i = lo; i <= hi; ++i){
            v.push_back(dp{i, getPower(i)});
        }
        sort(v.begin(), v.end(), cmp);
        return v[k-1].d;
    }
private:
    struct dp{
        int d, p;
    };
    static bool cmp(dp& a, dp& b){
        if(a.p == b.p)  return a.d < b.d;
        return a.p < b.p;
    }
    int getPower(int d){
        int p = 0;
        while(d != 1){
            if(d % 2 == 0)  d = d / 2;
            else    d = 3 * d + 1;
            ++p;
        }
        return p;
    }
};
```

Runtime: 28 ms, faster than 80.07% of C++ online submissions for Sort Integers by The Power Value.

Memory Usage: 8.8 MB, less than 75.70% of C++ online submissions for Sort Integers by The Power Value.



因为只有两个数字，也可以不定义结构体，直接构造 `pair` 存入数组中排序。

```c++
class Solution {
public:
    static bool cmp(pair<int, int>& a, pair<int, int>& b){
        if(a.second == b.second)  return a.first < b.first;
        return a.second < b.second;
    }
    int getKth(int lo, int hi, int k) {
        if(lo == hi)    return lo;
        vector<pair<int, int>> v;
       for(int i = lo; i <= hi; ++i){
            v.push_back(make_pair(i, getPower(i)));
        }
        sort(v.begin(), v.end(), cmp);
        return v[k-1].first;
    }
    int getPower(int d){
        int p = 0;
        while(d != 1){
            if(d % 2 == 0)  d = d / 2;
            else    d = 3 * d + 1;
            ++p;
        }
        return p;
    }
};
```

Runtime: 32 ms, faster than 75.42% of C++ online submissions for Sort Integers by The Power Value.

Memory Usage: 8.8 MB, less than 75.70% of C++ online submissions for Sort Integers by The Power Value.


