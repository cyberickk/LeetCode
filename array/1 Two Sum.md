# 1 Two Sum

[https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

<br>

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly\* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

 

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

 

**Constraints:**

- `2 <= nums.length <= 104`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **Only one valid answer exists.**

<br>

## Basic Solution

二重循环，穷举遍历找到两个下标，没有超时。

时间复杂度 O(n^2)，空间复杂度 O(1)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        int n = nums.size();
        for(int i = 0; i < n; ++i){
            for(int j = i+1; j < n; ++j){
                if(nums[i] + nums[j] == target){
                    ans.push_back(i);
                    ans.push_back(j);
                    return ans;
                }
            }
        }
        return ans;
    }
};
```

Runtime: 544 ms, faster than 6.18% of C++ online submissions for Two Sum.

Memory Usage: 10.2 MB, less than 77.93% of C++ online submissions for Two Sum.



## Optimized Solution

遍历一次，同时用 map 记录已经遍历过的数值和下标；每次检查当前数字的“另一半”是否已经存在，如果存在则返回两个下标。

对于数字重复的情况也适用，具体分为两种：两个相同数字组成 `target` ，那么这两个下标会一起返回；重复数字与另一数字组成 `target`，由于题目规定答案唯一，因此这种情况不成立。

遍历的时间复杂度 O(n)，unordered_map 查询的时间复杂度接近 O(1)（最差情况下 O(n)），总的时间复杂度 O(n)，空间复杂度 O(n)

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        unordered_map<int, int> mp;
        int n = nums.size();
        for(int i = 0; i < n; ++i){
            if(mp.count(target - nums[i])){
                ans.push_back(mp[target-nums[i]]);
                ans.push_back(i);  
                return ans;
            }
            mp[nums[i]] = i;
        }
        return ans;
    }
};
```

Runtime: 8 ms, faster than 94.73% of C++ online submissions for Two Sum.

Memory Usage: 10.6 MB, less than 60.09% of C++ online submissions for Two Sum.

