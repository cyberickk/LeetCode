# 350 两个数组的交集 Intersection of Two Arrays II [Easy]

**说明：**

- 输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。
- 我们可以不考虑输出结果的顺序。

**进阶:**

- 如果给定的数组已经排好序呢？你将如何优化你的算法？
- 如果 *nums1* 的大小比 *nums2* 小很多，哪种方法更优？
- 如果 *nums2* 的元素存储在磁盘上，磁盘内存是有限的，并且你不能一次加载所有的元素到内存中，你该怎么办？



## 解法一 排序后比较重复元素

时间复杂度 O(mlogm + nlogn + m+n),  空间复杂度 O(min(m,n))

如果已经排序，则直接比较并存入数组即可，时间复杂度 O(min(m,n))；如果两个数组大小相差很多，时间复杂度 O(mlogm + m)，或者大的排序，小的做二叉搜索，时间复杂度 O(mlogn + nlogn)；如果存储在磁盘上并且不能一次加载，那么不适用



```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        vector<int> v;
        int n1 = nums1.size(), n2 = nums2.size();
        for(int i = 0, j = 0; i < n1 && j < n2; ) {
            if(nums1[i] == nums2[j]) {
                v.push_back(nums1[i]);
                i++; j++;
            }
            else if(nums1[i] < nums2[j])
                i++;
            else
                j++;
        }
        return v;
    }
};
```



## 解法二 用 map 存放元素数量

时间复杂度 O(mlogm + n),  空间复杂度 O(m + min(m,n))， 另外可以把重复元素放入 nums1 中，无需再建立数组占用空间

如果已经排好序，时间空间复杂度均没有降低；如果 nums1 比 nums2 小很多，时间复杂度不变，空间复杂度可以减小，小的存 map; 如果 nums2 存在磁盘中，nums1 存在 map 中，分次加载元素并查找

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        int n1=nums1.size();
        int n2=nums2.size();        
        if(n1==0||n2==0)
        {
            vector<int> res(0);
            return res;
        }
        map<int,int> c;
        for(int i=0;i<n1;i++)
        {
            c[nums1[i]]++;

        }
        int number=0;
        for(int i=0;i<n2;i++)
        {
            if(c[nums2[i]]>0)
            {
                nums1[number]=nums2[i];
                number++;
                c[nums2[i]]--;
            }
        }
        vector<int> res(&nums1[0],&nums1[number]);
        return res;
    }
};
```



```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> res;
        unordered_map<int,int> m;
        for(auto n:nums1) m[n]++;
        for(auto n:nums2) {if(m.count(n)) {m[n]--;res.push_back(n);if(!m[n]) m.erase(n);}}
        return res;
    }
};
```

