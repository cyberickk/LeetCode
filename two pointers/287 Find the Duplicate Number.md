# 287 Find the Duplicate Number

[https://leetcode.com/problems/find-the-duplicate-number/](https://leetcode.com/problems/find-the-duplicate-number/)

<br>

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return *this repeated number*.

You must solve the problem **without** modifying the array `nums` and uses only constant extra space.

 

**Example 1:**

```
Input: nums = [1,3,4,2,2]
Output: 2
```

**Example 2:**

```
Input: nums = [3,1,3,4,2]
Output: 3
```

**Example 3:**

```
Input: nums = [1,1]
Output: 1
```

**Example 4:**

```
Input: nums = [1,1,2]
Output: 1
```

 

**Constraints:**

- `2 <= n <= 105`
- `nums.length == n + 1`
- `1 <= nums[i] <= n`
- All the integers in `nums` appear only **once** except for **precisely one integer** which appears **two or more** times.

 

**Follow up:**

- How can we prove that at least one duplicate number must exist in `nums`?
- Can you solve the problem in linear runtime complexity?



## Sort Solution

排序后查找相邻位置中相等的数字。

排序时间复杂度 O(nlogn)，遍历查找的时间复杂度 O(n)，总的时间复杂度 O(nlogn)；空间复杂度 O(1)

但是不符合题目的不改变原数组的要求。

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        for(int i = 1; i < n; ++i){
            if(nums[i] == nums[i-1])
                return nums[i];
        }
        return 0;
    }
};
```

Runtime: 140 ms, faster than 19.07% of C++ online submissions for Find the Duplicate Number.

Memory Usage: 61.2 MB, less than 37.09% of C++ online submissions for Find the Duplicate Number.



## Set Solution

用一个集合记录前面存在的数字，每遍历到一位时查看是否已经在集合内，是则返回。

插入的平均复杂度 O(1)（最坏情况下 O(n))，总的时间复杂度 O(n)；空间复杂度 O(n)

不符合题目的仅使用常数级额外空间的要求

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        unordered_set<int> s;
        for(int i = 0; i < n; ++i){
            if(s.count(nums[i]))
                return nums[i];
            else
                s.insert(nums[i]);
        }
        return 0;
    }
};
```

Runtime: 184 ms, faster than 11.78% of C++ online submissions for Find the Duplicate Number.

Memory Usage: 83.9 MB, less than 10.14% of C++ online submissions for Find the Duplicate Number.





## Cycle Solution

[https://leetcode.com/problems/find-the-duplicate-number/solution/](https://leetcode.com/problems/find-the-duplicate-number/solution/)

<br>

首先用函数 `F(x) = nums[x]` 构成链表，由于重复数字的存在，链表必然会存在环；由此转化为链表中查找环的起点问题。

采用著名的 Floyd Cycle Detection 算法，龟兔赛跑两个指针，龟每次走一步，兔子每次走两步，这样兔子先进入环中开始循环，当龟兔相遇时确定了 intersection node，二者行进的步数差距是环长度的整数倍；此时将龟返回到起点，接下来龟兔同速度一步一步前进，直至相遇时该点即为环的起点。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int tortoise = nums[0];
        int hare = nums[0];
        do{
            tortoise = nums[tortoise];
            hare = nums[nums[hare]];
        }while(tortoise != hare);
        
        tortoise = nums[0];
        while(tortoise != hare){
            tortoise = nums[tortoise];
            hare = nums[hare];
        }
        return hare;
    }
};
```

Runtime: 92 ms, faster than 57.11% of C++ online submissions for Find the Duplicate Number.

Memory Usage: 61.3 MB, less than 37.09% of C++ online submissions for Find the Duplicate Number.