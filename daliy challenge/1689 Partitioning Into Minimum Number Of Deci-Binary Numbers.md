# 1689 Partitioning Into Minimum Number Of Deci-Binary Numbers 

[https://leetcode.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/](https://leetcode.com/problems/partitioning-into-minimum-number-of-deci-binary-numbers/)

<br>

A decimal number is called **deci-binary** if each of its digits is either `0` or `1` without any leading zeros. For example, `101` and `1100`are **deci-binary**, while `112` and `3001` are not.

Given a string `n` that represents a positive decimal integer, return *the **minimum** number of positive **deci-binary** numbers needed so that they sum up to* `n`*.*

 

**Example 1:**

```
Input: n = "32"
Output: 3
Explanation: 10 + 11 + 11 = 32
```

**Example 2:**

```
Input: n = "82734"
Output: 8
```

**Example 3:**

```
Input: n = "27346209830709182346"
Output: 9
```

 

**Constraints:**

- `1 <= n.length <= 105`
- `n` consists of only digits.
- `n` does not contain any leading zeros and represents a positive integer.



<br>

## Solution

每一位只能 `0` 或者 `1`，就是看字符串中最大的一位是几，那么就需要几个  **deci-binary** 累加起来。如果某一位是 `9` 可以直接停止查询，十进制数不会有更大的数字。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    int minPartitions(string n) {
        int t = 0;
        for(int i = 0; i < n.size(); ++i){
            t = max(n[i] - '0', t);
            if(t == 9)
                break;
        }
        return t;
    }
};
```

Runtime: 36 ms, faster than 46.90% of C++ online submissions for Partitioning Into Minimum Number Of Deci-Binary Numbers.

Memory Usage: 13.5 MB, less than 29.29% of C++ online submissions for Partitioning Into Minimum Number Of Deci-Binary Numbers.