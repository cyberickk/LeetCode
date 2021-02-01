# 136 只出现一次的数字 Single Number [Easy]

## 解法一 异或运算

相同的两个数异或得 0， 遍历数组依次异或，出现两次的数字“消掉”，最后剩下只出现一次的数字。题目说明除了某个元素只出现一次以外，其余每个元素均出现两次，可以推测数组长度最小为1，不进行判空也可以通过所有的测试用例。

时间复杂度 O(n)， 空间复杂度 O(1)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int t = nums[0];
        for(int i = 1; i < nums.size(); ++i)
        {
            t = t ^ nums[i];
        }
        return t;
    }
};
```



## 解法二 排序后遍历

排序后步长为 2 进行遍历，对比相邻的两个元素，如果不同则找到了只出现一次的元素。

注意遍历时的边界用 [0, n-1), 对比的是 i 和 i+1，默认返回最后一位元素

时间复杂度 O(n + nlogn), 空间复杂度 O(1)

```c++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        for(int i = 0; i < nums.size() - 1; i += 2) {
            if(nums[i] != nums[i+1]) 
                return nums[i];
        }
        return nums[nums.size() - 1];
    }
};
```

