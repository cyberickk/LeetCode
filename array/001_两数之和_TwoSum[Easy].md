# 001 两数之和 Two Sum [Easy]



给定一个整数数组 `nums` 和一个目标值 `target`，请你在该数组中找出和为目标值的那 **两个** 整数，并返回他们的数组下标。

你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

**示例:**

```
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```



第一轮遍历，map 或者 unordered_map 存放下标，用[] 下标插入时，key 相同会覆盖，仅保留最后一次的 value；第二轮遍历，如果 map 中存在成对的 target 余数则返回结果，如果是 3 + 3 = 6 的情况，由于 map 中保留的是较大的下标，遍历时遍历到较小的下标，所以两个结果值不会重复，可以正常通过测试用例。

时间复杂度 O(n)， 空间复杂度 O(n)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> m;
        vector<int> v;
        for(int i = 0; i < nums.size(); ++i) 
            m[nums[i]] = i;
        for(int i = 0; i < nums.size(); ++i) {
            if( m.count(target - nums[i]) && m[target - nums[i]] != i) {
                v.push_back(m[target - nums[i]]);
                v.push_back(i);
                return v;               
            }
        }
        return v;
    }
};
```

改进算法，由于结果只有两个元素，可以不创建 vector，直接返回两个值即可。并且可以在一轮循环中完成查找 target 余数，注意要先查找返回再插入 map，才能避免 3 + 3 = 6 返回两个相同下标或者相同 key 的不同下标被覆盖的情况

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> m;
        for(int i = 0; i < nums.size(); ++i) {
            if(m.count(target - nums[i])) 
                return {m[target - nums[i]],i};
            m[nums[i]] = i;
        }
        return {};
    }
};
```





