# 399 Evaluate Division

[https://leetcode.com/problems/evaluate-division/](https://leetcode.com/problems/evaluate-division/)

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [Ai, Bi]` and `values[i]`represent the equation `Ai / Bi = values[i]`. Each `Ai` or `Bi` is a string that represents a single variable.

You are also given some `queries`, where `queries[j] = [Cj, Dj]`represents the `jth` query where you must find the answer for `Cj / Dj= ?`.

Return *the answers to all queries*. If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

 

**Example 1:**

```
Input: equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
Output: [6.00000,0.50000,-1.00000,1.00000,-1.00000]
Explanation: 
Given: a / b = 2.0, b / c = 3.0
queries are: a / c = ?, b / a = ?, a / e = ?, a / a = ?, x / x = ?
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
```

**Example 2:**

```
Input: equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
Output: [3.75000,0.40000,5.00000,0.20000]
```

**Example 3:**

```
Input: equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
Output: [0.50000,2.00000,-1.00000,-1.00000]
```

 

**Constraints:**

- `1 <= equations.length <= 20`
- `equations[i].length == 2`
- `1 <= Ai.length, Bi.length <= 5`
- `values.length == equations.length`
- `0.0 < values[i] <= 20.0`
- `1 <= queries.length <= 20`
- `queries[i].length == 2`
- `1 <= Cj.length, Dj.length <= 5`
- `Ai, Bi, Cj, Dj` consist of lower case English letters and digits.





# Graph Solution

题目中的除法的商关系可以看作两点之间存在双向边，并且权重互为倒数。给出的 `equations & values` 构成一张有向图，根据已知信息进行查询时，相当于查询两点之间是否存在路径，如果存在则返回路径权重的乘积，否则返回 `-1.0`

注意只要一个 `query` 存在 `equations` 中没有出现过的字符串，就直接判定为 `-1.0` ，即使 `["x","x"]` 这样看起来商是 `1` ，但 `x` 没有出现在 `equations` 中，就不能得出结果。

解题分为两个步骤：

1. 根据  `equations & values`  构建图，为了便于查询，采用 `unordered_map` ，一个 `value` 形成两条边
2. 查询，首先判定除数与被除数是否出现过；使用 DFS 查询，采用一个集合 `visited` 记录访问过的节点，一个队列 `que` 记录过程中的点以及源点到该点的商，访问到 `query` 的除数时返回结果，否则返回 `-1.0`

构建图需要访问 `equations` 中的每一个值，`emplace` 的平均时间复杂度是常数级，最坏情况下是容量线性级，因此构建图的时间复杂度是 O(n)，进行一次查询的最坏时间复杂度是 O(n)，最终总的时间复杂度 O(mn)；空间复杂度 O(n)

```c++
class Solution {
public:
    vector<double> calcEquation(vector<vector<string>>& equations, vector<double>& values, vector<vector<string>>& queries) {
        vector<double> v;
        unordered_map<string, unordered_map<string, double>> graph;
        for(int i = 0; i < equations.size(); ++i){
            graph[equations[i][0]].emplace(equations[i][1], values[i]);
            graph[equations[i][1]].emplace(equations[i][0], 1.0 / values[i]);
        }
        for(vector<string> q : queries){
            v.push_back(query(q, graph));
        }
        return v;
    }
private:
    double query(vector<string>& q, unordered_map<string, unordered_map<string, double>>& graph){
        if(graph.count(q[0]) && graph.count(q[1])){
            if(q[0] == q[1])    return 1.0;
            bool flag = false;
            queue<pair<string, double>> que;
            unordered_set<string> visited;
            que.push({q[0], 1.0});
            visited.insert(q[0]);
            while(!(que.empty() || flag)){
                for(int i = que.size(); i > 0; --i){
                    auto t = que.front();
                    que.pop();
                    if(t.first == q[1])    {
                        return t.second;
                        flag = true;
                        break;
                    }
                    for(auto mi : graph[t.first]){
                        if(visited.count(mi.first)) continue;
                        visited.insert(mi.first);
                        que.push(make_pair(mi.first, mi.second * t.second));
                    }
                }
            }
        }        
        return -1.0;
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions forEvaluate Division.

Memory Usage: 8 MB, less than 87.41% of C++ online submissions forEvaluate Division.