# 026 删除排序数组中的重复项 Remove Duplicates from Sorted Array [Easy]

**题目分析：** 返回不重复的元素个数 cnt 并且数组前 cnt 位存放这些元素

**思路：** 遍历数组，两个“指针”索引，int i 遍历，相同元素时不操作，不同元素时存放在 pre 位置并且计数加一

**复杂度：** 时间复杂度 O(n)，空间复杂度 O(1)



```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {      
        int n = nums.size();
        if(n == 0) return 0;
        int pre = 0, cnt = 1;	//至少包含一个元素，cnt 初始值为 1
        for(int i = 1; i < n; ++i) {
            if(nums[i] != nums[pre]) {
                nums[++pre] = nums[i];
                cnt++;
            }
        }
        return cnt;
    }
};
```





```c++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int p1 = 0, p2 = 0, n = nums.size();
        while(p2 < n)
        {
            if(nums[p2] == nums[p1]) p2++;
            else                 
                nums[++p1] = nums[p2++];
        }
        return nums.empty() ? 0 : p1 + 1;
    }
};
```



