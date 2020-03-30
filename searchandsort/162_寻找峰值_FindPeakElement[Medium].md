# 162 寻找峰值 Find Peak Element [Medium]

峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 `nums`，其中 `nums[i] ≠ nums[i+1]`，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 `nums[-1] = nums[n] = -∞`。

**示例 1:**

```
输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。
```

**示例 2:**

```
输入: nums = [1,2,1,3,5,6,4]
输出: 1 或 5 
解释: 你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。
```

**说明:**

你的解法应该是 *O*(*logN*) 时间复杂度的。



## 解法一 暴力解法

遍历寻找符合条件的峰值，时间复杂度 O(n)，空间复杂度 O(1)

边界情况处理，元素个数小于2时，返回 0； 由于假设数组开区间的两个边界趋近于-∞ ，并且多个峰值的情况下返回任一个索引即可，只要倒数第一个元素大于倒数第二个元素，那么可认为它就是峰值，返回 n-1 可以成立

```c++
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size();
        if(n == 0 || n == 1) return 0;
        if(nums[n-1] > nums[n-2]) return n-1;       
        for(int i = 1; i < nums.size() - 1; ++i) {
            if(nums[i] > nums[i-1] && nums[i] > nums[i+1])
                return i;
        }
        return 0;
    }
};
```



## 解法二 二分法

时间复杂度 O(logn)，空间复杂度 O(1)

```c++
//二分法
    int findPeakElement(vector<int>& nums)
    {
        int low = 0,high = nums.size() - 1;
        while(low < high)
        {
            int mid = (low + high) / 2;
            if(mid > nums.size() - 1 || nums[mid] > nums[mid + 1]) high = mid;   //当后面比前面要小的时候，峰值一定在大的那边
            else
                low = mid + 1;
        }
        return low;
    }
```

