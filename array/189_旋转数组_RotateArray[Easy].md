# 189 旋转数组 Rotate Array [Easy]

**题目要求：** 给定一个数组，将数组中的元素向右移动 *k* 个位置，其中 *k* 是非负数。至少有三种不同的解法，要求使用空间复杂度为 O(1) 的 **原地** 算法。

**注意：** k 是非负数但可能大于数组长度，要取模才能得到有效的移动值



## 解法一 暴力算法

k 次循环，每次循环向右移动一位。时间复杂度 O(n^2)，空间复杂度 O(1)， 到第 33/34 个测试用例时超时

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) { 
        int n = nums.size();
        k %= n;
        for(int i = 0; i < k; ++i) {
            int tmp = nums[n-1];
            for(int j = n-2; j >= 0; --j) 
                nums[j+1] = nums[j];
            nums[0] = tmp;
        }
    }
};
```



## 解法二 使用辅助数组

将最右 k 位存储到辅助数组中，前 n - k 位直接向右移动 k 位，再把存储的最右 k 位放入前 k 位中。可以通过 34 个测试用例。

时间复杂度 O(n)，空间复杂度 O(n)，不符合题目的原地要求

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {        
        int n = nums.size();
        if(k == 0 || n == 0 || n == 1) return;
        vector<int> v;
        k = k % n;
        for(int i = n - k; i < n; ++i)
            v.push_back(nums[i]);
        for(int i = n - k - 1; i >= 0; --i) 
            nums[i + k] = nums[i];
        for(int i = 0; i < k; ++i)
            nums[i] = v[i];
    }
};
```



## 解法三 逆置算法

逆置前 k 位，再逆置后 n-k 位，最后整个数组逆置；或者整个数组逆置，再逆置前 n-k 位，最后逆置后 k 位。两种方法的顺序不能乱。可以自己实现逆置算法，或者直接使用 STL 的数组逆置算法 `reverse(nums.begin(), nums.end()); ` 传入两个迭代器，注意是前闭后开区间，逆置时不包含右边界

时间复杂度 O(n),  空间复杂度 O(1)

```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) { 
        int n = nums.size();
        k = k % n;
        for(int i = 0; i <= (n - 1 - k) / 2; i++) {
            swap(nums[i], nums[n - 1 - k - i]);
        }
        for(int i = n - k; i <= (n - 1 + n - k) / 2; i++) {
            swap(nums[i], nums[n - 1 + n - k - i]);
        }
        for(int i = 0; i <= (n - 1) / 2; i++) {
            swap(nums[i], nums[n - 1 - i]);
        }
    }
};
```



```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {        
        k %= nums.size();	
		reverse(nums.begin(), nums.end());
		reverse(nums.begin(), nums.begin()+k);
		reverse(nums.begin() + k, nums.end());
    }
};
```



```c++
class Solution {
public:
    void rotate(vector<int>& nums, int k) { 
        int n = nums.size();
        k %= n;       
        reverse(nums.begin(), nums.begin() + n - k);
        reverse(nums.begin() + n - k, nums.end());
        reverse(nums.begin(), nums.end());
    }
};
```



