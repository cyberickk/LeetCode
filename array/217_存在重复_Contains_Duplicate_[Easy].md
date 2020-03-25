# 217 存在重复 Contains Duplicate [Easy]



## 解法一 排序后查找重复

借助 STL vector sort 算法进行排序，底层是快排算法时间复杂度 O(nlogn)，再遍历数组看有无重复元素，时间复杂度 O(n),  总的时间复杂度 O(n + nlogn)， 空间复杂度 O(1)

注意涉及对比相邻元素时，遍历数组的范围是 [1, n)，可以不用单独处理数组为空的情况；用 [0, n-1) 在数组为空时会报错，所以要先判空并返回 false

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        // 先判空处理
        /*
        sort(nums.begin(), nums.end());
        if(nums.size() == 0) return false;
        for(int i = 0; i < nums.size() - 1; ++i) {
            if(nums[i] == nums[i+1])
                return true;
        }    
        return false;
        */
        sort(nums.begin(), nums.end());
        for(int i = 1; i < nums.size(); ++i)
        {
            if(nums[i] == nums[i-1]) return 1;
        }
        return 0;
    }
};
```



## 解法二 借助 set

把数组元素存入 set， 由于 set 具有元素唯一的特性，所以 set 和 vector 长度不等时代表有重复元素

时间复杂度 O(n)， 空间复杂度 O(n)

```c++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        set<int> s;
        for(int i = 0; i < nums.size(); ++i)
            s.insert(nums[i]);
        return nums.size() != s.size();
    }
};
```

