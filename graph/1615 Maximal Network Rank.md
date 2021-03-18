# 1615 Maximal Network Rank

[https://leetcode.com/problems/maximal-network-rank/](https://leetcode.com/problems/maximal-network-rank/)

There is an infrastructure of `n` cities with some number of `roads` connecting these cities. Each `roads[i] = [ai, bi]` indicates that there is a bidirectional road between cities `ai` and `bi`.

The **network rank** of **two different cities** is defined as the total number of **directly** connected roads to **either** city. If a road is directly connected to both cities, it is only counted **once**.

The **maximal network rank** of the infrastructure is the **maximum network rank** of all pairs of different cities.

Given the integer `n` and the array `roads`, return *the **maximal network rank** of the entire infrastructure*.

 

**Example 1:**

**![img](https://assets.leetcode.com/uploads/2020/09/21/ex1.png)**

```
Input: n = 4, roads = [[0,1],[0,3],[1,2],[1,3]]
Output: 4
Explanation: The network rank of cities 0 and 1 is 4 as there are 4 roads that are connected to either 0 or 1. The road between 0 and 1 is only counted once.
```

**Example 2:**

**![img](https://assets.leetcode.com/uploads/2020/09/21/ex2.png)**

```
Input: n = 5, roads = [[0,1],[0,3],[1,2],[1,3],[2,3],[2,4]]
Output: 5
Explanation: There are 5 roads that are connected to cities 1 or 2.
```

**Example 3:**

```
Input: n = 8, roads = [[0,1],[1,2],[2,3],[2,4],[5,6],[5,7]]
Output: 5
Explanation: The network rank of 2 and 5 is 5. Notice that all the cities do not have to be connected.
```

 

**Constraints:**

- `2 <= n <= 100`
- `0 <= roads.length <= n * (n - 1) / 2`
- `roads[i].length == 2`
- `0 <= ai, bi <= n-1`
- `ai != bi`
- Each pair of cities has **at most one** road connecting them.



# matrix solution

首先理解题意中的 `rank`，任意取两个点，可以直接连通到这两个点的边的数量，如果该两点之间存在边则只计算一次。那么排序依据是两点的度数之和减去边(i, j)。

邻接矩阵记录点的连通性，同时用数组记录每个点的度数。遍历 `roads` 得到邻接矩阵和度数，然后对度数数组进行双重循环的枚举，得到最大值。

遍历 `roads` 的时间复杂度 O(E)，遍历度数数组的时间复杂度 O(V^2)，总的时间复杂度 O(E + V^2)，空间复杂度 O(V^2+V)

注意二维数组的 `size` 初始化

```c++
class Solution {
public:
    int maximalNetworkRank(int n, vector<vector<int>>& roads) {
        vector<vector<int>> matrix(n, vector<int>(n, 0));
        vector<int> cnt(n, 0);
        for(auto r : roads){
            matrix[r[0]][r[1]] = 1;
            matrix[r[1]][r[0]] = 1;
            cnt[r[0]]++;
            cnt[r[1]]++;
        }
        int res = 0;
        for(int i = 0; i < n; ++i){
            for(int j = i+1; j < n; ++j){
                if(cnt[i] + cnt[j] - matrix[i][j] > res)
                    res = cnt[i] + cnt[j] - matrix[i][j];
            }
        }
        return res;
    }
};
```

Runtime: 76 ms, faster than 85.65% of C++ online submissions for Maximal Network Rank.

Memory Usage: 32.9 MB, less than 57.10% of C++ online submissions forMaximal Network Rank.





# adjacent list solution

采用邻接表存储每个点直接连通的顶点，双重循环遍历邻接表，枚举所有的 `rank`，调用 `std:find()` 查找是否有直接连通两个点的边。

时间复杂度 O(E+V^2)，空间复杂度O(V*E)

```c++
class Solution {
public:
    int maximalNetworkRank(int n, vector<vector<int>>& roads) {
        vector<vector<int>> adlist(n);
        for(auto r : roads){
            adlist[r[0]].push_back(r[1]);
            adlist[r[1]].push_back(r[0]);
        }
        int res = 0;
        for(int i = 0; i < n; ++i){
            for(int j = i + 1; j < n; ++j){
                int tres = adlist[i].size() + adlist[j].size();
                if(find(adlist[i].begin(), adlist[i].end(), j) != adlist[i].end())
                    tres--;
                res = max(res, tres);
            }
        }
        return res;
    }
};
```

Runtime: 68 ms, faster than 90.83% of C++ online submissions for Maximal Network Rank.

Memory Usage: 34 MB, less than 47.04% of C++ online submissions forMaximal Network Rank.