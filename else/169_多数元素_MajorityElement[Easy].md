# 169 多数元素 Majority Element [Easy]

给定一个大小为 *n* 的数组，找到其中的多数元素。多数元素是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

**示例 1:**

```
输入: [3,2,3]
输出: 3
```

**示例 2:**

```
输入: [2,2,1,1,1,2,2]
输出: 2
```



## 解法一 map

map 记录元素累计出现次数，多于 n/2 时返回即可

时间复杂度 O(n)，空间复杂度 O(n)

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int,int> m;
        int n = nums.size();
        for(auto i : nums) {
            m[i]++;
            if(m[i] > (n / 2)) return i;
        }
        return -1;
    }
};
```



## 解法二 累次计数

tmp 存放当前出现最多的元素，cnt 计数，遍历时元素与 tmp 相同则计数增加，否则计数减少，计数为 0 时更换 tmp 为当前元素值。由于出现次数大于一半，所以遍历结束时一定能找到该元素。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int tmp, cnt = 0;
        for(auto i : nums) {
            if(cnt == 0)
                tmp = i;
            if(i == tmp)
                cnt++;
            else
                cnt--;
        }
        return tmp;
    }
};
```

