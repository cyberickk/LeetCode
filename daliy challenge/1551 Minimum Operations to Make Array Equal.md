# 1551 Minimum Operations to Make Array Equal

[https://leetcode.com/problems/minimum-operations-to-make-array-equal/](https://leetcode.com/problems/minimum-operations-to-make-array-equal/)

You have an array `arr` of length `n` where `arr[i] = (2 * i) + 1` for all valid values of `i` (i.e. `0 <= i < n`).

In one operation, you can select two indices `x` and `y` where `0 <= x, y < n`and subtract `1` from `arr[x]` and add `1` to `arr[y]` (i.e. perform `arr[x] -=1 `and `arr[y] += 1`). The goal is to make all the elements of the array **equal**. It is **guaranteed** that all the elements of the array can be made equal using some operations.

Given an integer `n`, the length of the array. Return *the minimum number of operations* needed to make all the elements of arr equal.

 

**Example 1:**

```
Input: n = 3
Output: 2
Explanation: arr = [1, 3, 5]
First operation choose x = 2 and y = 0, this leads arr to be [2, 3, 4]
In the second operation choose x = 2 and y = 0 again, thus arr = [3, 3, 3].
```

**Example 2:**

```
Input: n = 6
Output: 9
```

 

**Constraints:**

- `1 <= n <= 10^4`



## Math Solution

对于奇数的情况，最中心一位就是最终的平均值，由内向外扩展依次需要操作 2、4、6……次，求和为

$2 * (1 + 2 +...+\frac{n-1}{2}) = \frac{n-1}{2} * \frac{n+1}{2} = \frac{n^2-1}{4}$

对于偶数的情况，最中心两位操作一次，由内向外依次增加 2 次，求和为

$1 + 3 + 5 + ... +\frac{n}{2} = \frac{n^2}{4}$

时间复杂度 O(1)，空间复杂度O(1)

```c++
class Solution {
public:
    int minOperations(int n) {
        if(n % 2 == 0)  return n * n / 4;
        return (n * n - 1) / 4;
    }
};
```

```
Runtime: 0 ms, faster than 100.00% of C++ online submissions forMinimum Operations to Make Array Equal.

Memory Usage: 5.7 MB, less than 95.12% of C++ online submissions forMinimum Operations to Make Array Equal.
```



还可以进一步优化，把奇数和偶数的情况统一，因为返回值向下取整，奇数的情况也可以看作是 `n*n/4` ，除 `4` 也可写作右移 `2` 位

```c++
class Solution {
public:
    int minOperations(int n) {
        return n * n >> 2;
    }
};
```





## Programming Solution

用循环模拟逐步相加的过程，偶数的情况从 1 开始加，每次步长 `2` 位，奇数的情况从 2 开始加，每一步全都多一次，因此需要在前面的基础上再增加 `n/2` 次

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    int minOperations(int n) {
        int ans = 0;
        for(int i = 1; i < n; i += 2){
            ans += i;
        }
        if(n % 2 == 1)  ans += n/2;
        return ans;
    }
};
```



```
Runtime: 0 ms, faster than 100.00% of C++ online submissions forMinimum Operations to Make Array Equal.

Memory Usage: 5.9 MB, less than 24.65% of C++ online submissions forMinimum Operations to Make Array Equal.
```

