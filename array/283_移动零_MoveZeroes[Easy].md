# 283 移动零 Move Zeroes [Easy]

给定一个数组 `nums`，编写一个函数将所有 `0` 移动到数组的末尾，同时保持非零元素的相对顺序。

**示例:**

```
输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
```

**说明**:

1. 必须在原数组上操作，不能拷贝额外的数组。
2. 尽量减少操作次数。



## 解法一 

遍历数组，计数非零元素的个数同时往前移，遍历完成后把最后几位置 0 即可

时间复杂度 O(n)， 空间复杂度 O(1)

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int cnt = 0, n = nums.size();
        for(int i = 0; i < n; ++i) {
            if(nums[i] != 0)
                nums[cnt++] = nums[i];
        }
        for(int i = cnt; i < n; ++i)
            nums[i] = 0;
    }
};
```



## 解法二 

遍历时碰到非零元素直接和上一次记录的位置交换，这样 0 就都交换到末尾

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        for(int i = 0, last = 0; i < nums.size(); ++i) {
            if(nums[i] != 0) 
                swap(nums[i], nums[last++]);
        }
    }
};
```

