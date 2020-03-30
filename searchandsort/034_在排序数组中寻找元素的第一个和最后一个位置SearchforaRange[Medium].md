# 034 在排序数组中寻找元素的第一个和最后一个位置 Search for a Range [Medium]

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 *O*(log *n*) 级别。

如果数组中不存在目标值，返回 `[-1, -1]`。

**示例 1:**

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```

**示例 2:**

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```



要求时间复杂度 O(logn)，用二分查找法，由于是排序数组，找到 target 时向前向后遍历即可找到首末位置。只需返回两个元素，可以不用建立数组，直接返回 {a,b}，默认查找失败时返回 {-1,-1}

空间复杂度 O(1)

```c++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int low = 0, high = nums.size()-1;
        if(low == high && nums[low] == target)
            return {low,low};
        while(low <= high) {		//边界是 <=
            int mid = (low + high) / 2;
            if(nums[mid] == target) {
                int begin = mid, end = mid;
                while(begin >= 0 && nums[begin] == target)
                    begin--;
                while(end < nums.size() && nums[end] == target)
                    end++;
                if(begin == end) return{begin,end};
                else return {++begin,--end};
            }
            else if(nums[mid] > target)
                high = mid-1;
            else
                low = mid+1;
        }
        return {-1,-1};
    }
};
```

