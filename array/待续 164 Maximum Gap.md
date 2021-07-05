# 164 Maximum Gap

[https://leetcode.com/problems/maximum-gap/](https://leetcode.com/problems/maximum-gap/)

Given an integer array `nums`, return *the maximum difference between two successive elements in its sorted form*. If the array contains less than two elements, return `0`.

You must write an algorithm that runs in linear time and uses linear extra space.

 

**Example 1:**

```
Input: nums = [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either (3,6) or (6,9) has the maximum difference 3.
```

**Example 2:**

```
Input: nums = [10]
Output: 0
Explanation: The array contains less than 2 elements, therefore return 0.
```

 

**Constraints:**

- `1 <= nums.length <= 104`
- `0 <= nums[i] <= 109`



<br>

## Solution

数组排序后找出最大的相邻差值

时间复杂度 O(nlogn)，空间复杂度 O(1)

但题目要求线性时间，所以用 STL 自定义的排序不符合条件，需要重新写排序算法。

```c++
class Solution {
public:
    int maximumGap(vector<int>& nums) {
        if(nums.size() < 2)
            return 0;        
        sort(nums.begin(), nums.end());
        int ans = 0;
        for(int i = 1; i < nums.size(); ++i){
            ans = max(ans, nums[i] - nums[i-1]);
        }
        return ans;
    }
};
```

