# 797 All Paths From Source to Target

Given a directed acyclic graph (**DAG**) of `n` nodes labeled from 0 to n - 1, find all possible paths from node `0` to node `n - 1`, and return them in any order.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2020/09/28/all_1.jpg)

```
Input: graph = [[1,2],[3],[3],[]]
Output: [[0,1,3],[0,2,3]]
Explanation: There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2020/09/28/all_2.jpg)

```
Input: graph = [[4,3,1],[3,2,4],[3],[4],[]]
Output: [[0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4]]
```

**Example 3:**

```
Input: graph = [[1],[]]
Output: [[0,1]]
```

**Example 4:**

```
Input: graph = [[1,2,3],[2],[3],[]]
Output: [[0,1,2,3],[0,2,3],[0,3]]
```

**Example 5:**

```
Input: graph = [[1,3],[2],[3],[]]
Output: [[0,1,2,3],[0,3]]
```

 

**Constraints:**

- `n == graph.length`
- `2 <= n <= 15`
- `0 <= graph[i][j] < n`
- `graph[i][j] != i` (i.e., there will be no self-loops).
- The input graph is **guaranteed** to be a **DAG**.



## recursive solution



```c++
class Solution {
public:
    vector<vector<int>> allPathsSourceTarget(vector<vector<int>>& graph) {
        vector<vector<int>> v;
        visitNext(graph, {}, 0, v);
        return v;
    }
    void visitNext(vector<vector<int>>& graph, vector<int> path, int cur, vector<vector<int>>& v){
        path.push_back(cur);
        if(cur == graph.size()-1)   v.push_back(path);
        else{
            for(int i : graph[cur]){
                visitNext(graph, path, i, v);
            }
        }
    }
};
```



Runtime: 32 ms, faster than 44.21% of C++ online submissions for All Paths From Source to Target.

Memory Usage: 15.3 MB, less than 44.93% of C++ online submissions for All Paths From Source to Target.