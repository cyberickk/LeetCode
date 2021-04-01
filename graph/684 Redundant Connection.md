# 684 Redundant Connection

[https://leetcode.com/problems/redundant-connection/](https://leetcode.com/problems/redundant-connection/)

In this problem, a tree is an **undirected** graph that is connected and has no cycles.

The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.

The resulting graph is given as a 2D-array of `edges`. Each element of `edges`is a pair `[u, v]` with `u < v`, that represents an **undirected** edge connecting nodes `u` and `v`.

Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge `[u, v]` should be in the same format, with `u < v`.

**Example 1:**

```
Input: [[1,2], [1,3], [2,3]]
Output: [2,3]
Explanation: The given undirected graph will be like this:
  1
 / \
2 - 3
```



**Example 2:**

```
Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
Output: [1,4]
Explanation: The given undirected graph will be like this:
5 - 1 - 2
    |   |
    4 - 3
```



**Note:**

The size of the input 2D-array will be between 3 and 1000.

Every integer represented in the 2D-array will be between 1 and N, where N is the size of the input array.





**Update (2017-09-26):**
We have overhauled the problem description + test cases and specified clearly the graph is an ***undirected\*** graph. For the ***directed\*** graph follow up please see **[Redundant Connection II](https://leetcode.com/problems/redundant-connection-ii/description/)**). We apologize for any inconvenience caused.





## recursive solution

根据给出的边，构建邻接表，得到每一个顶点的相邻顶点集合。

冗余边加入后会构成环，检查是否为冗余边，就是检查对于一个新加入的边`(s, t)`，是否已经存在路径使得两个端点可达。可以递归地进行检查，从一个端点 `s` 出发，检查相邻顶点的集合，直到找到目标端点 `t` ，此时代表新加入的这条边会造成冗余。

在递归检查的过程中，上一轮检查的出发点需要跳过，防止陷入死循环。

时间复杂度 O(n^2)，空间复杂度 O(n)，对于同一条边会进行多次重复检查。

```c++
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        unordered_map<int, unordered_set<int>> edlist;
        for(auto e:edges){
            if(isCycle(e[0], e[1], edlist, -1))  return e;
            edlist[e[0]].insert(e[1]);
            edlist[e[1]].insert(e[0]);        
        }
        return {};
    }
private:
    bool isCycle(int cur, int target, unordered_map<int, unordered_set<int>>& edlist, int pre){        
        if(edlist[cur].count(target))   return true;
        for(auto n:edlist[cur]){
            if(n == pre)   continue;
            if(isCycle(n, target, edlist, cur)) return true;
        }
        return false;
    }
};
```

Runtime: 20 ms, faster than 13.91% of C++ online submissions forRedundant Connection.

Memory Usage: 11.4 MB, less than 14.42% of C++ online submissions for Redundant Connection.



## iterative solution

也可以采用 BFS 的思想进行检查，把相邻的顶点依次加入队列中，另外用一个集合保存已经检查过的顶点，防止死循环。当可以访问到另一个顶点时表示这条边冗余。

时间复杂度 O(n^2)，空间复杂度 O(n)，同样效率比较低。

```c++
class Solution {
public:
    vector<int> findRedundantConnection(vector<vector<int>>& edges) {
        unordered_map<int, unordered_set<int>> edlist;
        for(auto e:edges){
            queue<int> q;
            unordered_set<int> visited;
            q.push(e[0]);
            while(!q.empty()){
                int cur = q.front();
                q.pop();
                visited.insert(cur);
                for(auto node:edlist[cur]){
                    if(node == e[1])    return e;
                    if(visited.count(node)) continue;
                    q.push(node);
                }
            }
            edlist[e[0]].insert(e[1]);
            edlist[e[1]].insert(e[0]);        
        }
        return {};
    }
};
```

Runtime: 32 ms, faster than 7.41% of C++ online submissions forRedundant Connection.

Memory Usage: 20.5 MB, less than 5.01% of C++ online submissions forRedundant Connection.



## union find

