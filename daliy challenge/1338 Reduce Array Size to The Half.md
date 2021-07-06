# 1338 Reduce Array Size to The Half

[https://leetcode.com/problems/reduce-array-size-to-the-half/](https://leetcode.com/problems/reduce-array-size-to-the-half/)

<br>

Given an array `arr`. You can choose a set of integers and remove all the occurrences of these integers in the array.

Return *the minimum size of the set* so that **at least** half of the integers of the array are removed.

 

**Example 1:**

```
Input: arr = [3,3,3,3,5,5,5,2,2,7]
Output: 2
Explanation: Choosing {3,7} will make the new array [5,5,5,2,2] which has size 5 (i.e equal to half of the size of the old array).
Possible sets of size 2 are {3,5},{3,2},{5,2}.
Choosing set {2,7} is not possible as it will make the new array [3,3,3,3,5,5,5] which has size greater than half of the size of the old array.
```

**Example 2:**

```
Input: arr = [7,7,7,7,7,7]
Output: 1
Explanation: The only possible set you can choose is {7}. This will make the new array empty.
```

**Example 3:**

```
Input: arr = [1,9]
Output: 1
```

**Example 4:**

```
Input: arr = [1000,1000,3,7]
Output: 1
```

**Example 5:**

```
Input: arr = [1,2,3,4,5,6,7,8,9,10]
Output: 5
```

 

**Constraints:**

- `1 <= arr.length <= 10^5`
- `arr.length` is even.
- `1 <= arr[i] <= 10^5`



## Solution

1. 统计原数组中每个数字的词频，采用 `map` 更直接一些但是插入每个节点的效率是 O(logn)，由于题目说数值在 `10^5` 以内因此用 `vector` 存储词频，统计词频的时间复杂度 O(n)；
2. 将数字与词频的 `pair` 存入 `vector` 中，根据词频降序排列，排序的时间复杂度 O(nlogn)
3. 由高到低删除数字，删除的数量达到一半时返回删除的数值个数

总的时间复杂度 O(n + nlogn)，空间复杂度 O(n)



```cpp
class Solution {
public:
    int minSetSize(vector<int>& arr) {
        int n = arr.size();
        vector<int> freq(100005, 0);
        for(int i = 0; i < n; ++i){
            ++freq[arr[i]];
        }
        vector<pair<int, int> > numfq;
        for(int i = 0; i < freq.size(); ++i){
            if(freq[i])
                numfq.push_back(make_pair(i, freq[i]));
        }
        sort(numfq.begin(), numfq.end(), cmp);
        int cnt = 0, del = 0;
        for(int i = 0; i < numfq.size(); ++i){
            ++cnt;
            del += numfq[i].second;
            if(del * 2 >= n)
                return cnt;
        }
        return n;
    }
    static bool cmp(pair<int, int>& a, pair<int, int>& b){
        return a.second > b.second;
    }
};
```



Runtime: 136 ms, faster than 91.30% of C++ online submissions for Reduce Array Size to The Half.

Memory Usage: 74.8 MB, less than 83.88% of C++ online submissions for Reduce Array Size to The Half.



## Optimization

上述方法可以适当简化，由于检查时只需关注词频，因此将词频存入数组并排序即可，不需存储对应的数字，也进一步降低空间消耗。



```cpp
class Solution {
public:
    int minSetSize(vector<int>& arr) {
        int n = arr.size();
        vector<int> freq(100005, 0);
        for(int i = 0; i < n; ++i){
            ++freq[arr[i]];
        }
        vector<int> numfq;
        for(int i = 0; i < freq.size(); ++i){
            if(freq[i])
                numfq.push_back(freq[i]);
        }
        sort(numfq.begin(), numfq.end());
        int cnt = 0, del = 0;
        for(int i = numfq.size()-1; i >= 0; --i){
            ++cnt;
            del += numfq[i];
            if(del * 2 >= n)
                return cnt;
        }
        return n;
    }
};
```



Runtime: 100 ms, faster than 99.33% of C++ online submissions for Reduce Array Size to The Half.

Memory Usage: 71.9 MB, less than 84.35% of C++ online submissions for Reduce Array Size to The Half.