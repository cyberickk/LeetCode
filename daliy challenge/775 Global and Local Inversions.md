

# 775 Global and Local Inversions

[https://leetcode.com/problems/global-and-local-inversions/](https://leetcode.com/problems/global-and-local-inversions/)



We have some permutation `A` of `[0, 1, ..., N - 1]`, where `N` is the length of `A`.

The number of (global) inversions is the number of `i < j` with `0 <= i < j < N` and `A[i] > A[j]`.

The number of local inversions is the number of `i` with `0 <= i < N` and `A[i] > A[i+1]`.

Return `true` if and only if the number of global inversions is equal to the number of local inversions.

**Example 1:**

```
Input: A = [1,0,2]
Output: true
Explanation: There is 1 global inversion, and 1 local inversion.
```

**Example 2:**

```
Input: A = [1,2,0]
Output: false
Explanation: There are 2 global inversions, and 1 local inversion.
```

**Note:**

- `A` will be a permutation of `[0, 1, ..., A.length - 1]`.
- `A` will have length in range `[1, 5000]`.
- The time limit for this problem has been reduced.



## Basic Solution

按题目定义计算 `#local inversions ` `#global inversions` 

`#local inversions` 很好计算，遍历一次判断前一位比后一位大即可，时间复杂度 O(n)

`#global inversions` 需要双重循环，时间复杂度 O(n^2)，运行超时

```c++
class Solution {
public:
    bool isIdealPermutation(vector<int>& A) {
        int n = A.size();
        //local inversion
        int l = 0;
        for(int i = 0; i < n-1; ++i){
            if(A[i] > A[i+1])   ++l;
        }
        //global inversion
        int g = 0;
        for(int i = 0; i < n-1; ++i){
            for(int j = i+1; j < n; ++j){
                if(A[i] > A[j])  ++g;
            }
        }
        return l == g;
    }
};
```



进行优化，不直接计算 `#global inversions` ，只要在遍历时发现满足 `A[i] > A[j]` 并且此时 `global + 1` 后大于前面算出的 `#local inversions` ，就直接返回失败。

虽然理论上速度有所提升，但时间复杂度还是 O(n^2)，仍然运行超时。

```c++
class Solution {
public:
    bool isIdealPermutation(vector<int>& A) {
        int n = A.size();
        //local inversion
        int l = 0;
        for(int i = 0; i < n-1; ++i){
            if(A[i] > A[i+1])   ++l;
        }
        //global inversion
        int g = 0;
        for(int i = 0; i < n; ++i){
            for(int j = i+1; j < n; ++j){
                if(A[i] > A[j] && ++g > l)  return false;
            }
        }
        return l == g;
    }
};
```



## Input Property Solution

分析 `local inversions` 和 `global inversions` 的含义

- `local inversions` 是相邻的两位中前一位比后一位大
- `local inversions`一定属于 `global inversions` ，也就是   `#global inversions >= #local inversions`  
- 如果需要二者相等，就相当于面对一个顺序排列，进行的乱序必须符合，调换只在相邻的两位中进行；否则一次调换引起的 `global inversions `  必定超过 `1`，最终 `#global inversions > #local inversions`  

因此我们判定的条件是，只要任意一个位置上的数字与下标之差超过 `1`，就代表最终的结果不等，返回 `false`

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    bool isIdealPermutation(vector<int>& A) {
        for(int i = 0; i < A.size(); ++i){
            if(abs(A[i] - i) > 1)   return false;
        }
        return true;
    }
};
```



Runtime: 40 ms, faster than 92.41% of C++ online submissions forGlobal and Local Inversions.

Memory Usage: 35.7 MB, less than 52.90% of C++ online submissions for Global and Local Inversions.