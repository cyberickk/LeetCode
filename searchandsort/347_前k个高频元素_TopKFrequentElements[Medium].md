# 347 前k个高频元素 Top K Frequent Elements [Medium]

给定一个非空的整数数组，返回其中出现频率前 **k **高的元素。

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

**说明：**

- 你可以假设给定的 *k* 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
- 你的算法的时间复杂度**必须**优于 O(*n* log *n*) , *n* 是数组的大小。



用 unordered_map 存放元素出现次数，应用 vector 的自定义排序特性，将元素和次数组成 pair 存放在 vector 中，取前 k 位的元素放入答案数组中

存放 map 时间复杂度 O(n)，存放 pair 时间复杂度 O(n)，排序时间复杂度 O(nlogn)，得到 top k 数组 时间复杂度 O(k)，总的时间复杂度 O(nlogn)；空间复杂度 O(n)

```c++
typedef pair<int,int> PAIR;
class Solution {
public:   
    static bool cmp(const PAIR& a, const PAIR& b) {
        return a.second > b.second ? 1 : 0;
    }  //一定要有关键词 static，不能调用非静态成员函数
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> m;
        vector<int> ans;
        vector<PAIR> v;	//使用push_back()时不要设定初始大小,否则前面会存在 n 个 0
        for(int i = 0; i < nums.size(); ++i) 
            m[nums[i]]++;
        for(auto it:m) 
            v.push_back(make_pair(it.first,it.second));
        sort(v.begin(), v.end(), cmp);
        for(int i = 0; i < k; ++i) 
            ans.push_back(v[i].first);
        return ans;
    }
};
```



另外可以利用优先队列 priority_queue，使得元素按照出现次数降序排列，将前 k 位的元素存放在数组中即可。

map 时间复杂度 O(n)，queue 时间复杂度 O(nlogn)，top k 时间复杂度 O(k)，总的时间复杂度 O(nlogn)，空间复杂度 O(n)

```c++
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> m;//频率map
        priority_queue<pair<int,int>> q;//优先队列，模拟堆
        vector<int> res;
        for(auto a:nums){
            ++m[a];
        }
        for(auto it:m){
            q.push(make_pair(it.second,it.first));
        }
        for(int i=0;i<k;i++){
            res.push_back(q.top().second);
            q.pop();
        }
        return res;
    }
};
```

