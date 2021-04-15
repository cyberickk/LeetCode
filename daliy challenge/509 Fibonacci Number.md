# 509 Fibonacci Number



[https://leetcode.com/problems/fibonacci-number/](https://leetcode.com/problems/fibonacci-number/)

The **Fibonacci numbers**, commonly denoted `F(n)` form a sequence, called the **Fibonacci sequence**, such that each number is the sum of the two preceding ones, starting from `0`and `1`. That is,

```
F(0) = 0, F(1) = 1
F(n) = F(n - 1) + F(n - 2), for n > 1.
```

Given `n`, calculate `F(n)`.

 

**Example 1:**

```
Input: n = 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
```

**Example 2:**

```
Input: n = 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
```

**Example 3:**

```
Input: n = 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```

 

**Constraints:**

- `0 <= n <= 30`



## Solution

使用两个变量保存前两位的斐波那契数，持续迭代即可，注意迭代次数。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    int fib(int n) {
        if(n < 2)
            return n;
        int pre1 = 0, pre2 = 1, ans;
        for(int i = 1; i < n; ++i){
            ans = pre1 + pre2;
            pre1 = pre2;
            pre2 = ans;
        }
        return ans;
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Fibonacci Number.

Memory Usage: 5.9 MB, less than 75.43% of C++ online submissions for Fibonacci Number.