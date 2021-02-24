

# 1267 Count Servers that Communicate

[https://leetcode.com/problems/count-servers-that-communicate/](https://leetcode.com/problems/count-servers-that-communicate/)

You are given a map of a server center, represented as a `m * n`integer matrix `grid`, where 1 means that on that cell there is a server and 0 means that it is no server. Two servers are said to communicate if they are on the same row or on the same column.

Return the number of servers that communicate with any other server.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2019/11/14/untitled-diagram-6.jpg)

```
Input: grid = [[1,0],[0,1]]
Output: 0
Explanation: No servers can communicate with others.
```

**Example 2:**

**![img](https://assets.leetcode.com/uploads/2019/11/13/untitled-diagram-4.jpg)**

```
Input: grid = [[1,0],[1,1]]
Output: 3
Explanation: All three servers can communicate with at least one other server.
```

**Example 3:**

![img](https://assets.leetcode.com/uploads/2019/11/14/untitled-diagram-1-3.jpg)

```
Input: grid = [[1,1,0,0],[0,0,1,0],[0,0,1,0],[0,0,0,1]]
Output: 4
Explanation: The two servers in the first row can communicate with each other. The two servers in the third column can communicate with each other. The server at right bottom corner can't communicate with any other server.
```

 

**Constraints:**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m <= 250`
- `1 <= n <= 250`
- `grid[i][j] == 0 or 1`



# basic solution

当一行（列）中至少有两台主机时，这一行（列）中的全部主机都联通；题目比较好理解，难点在于不重复计数。因为一定要遍历完所有位置，所以时间复杂度至少是 O(mn)

第一次遍历时采用两个数组统计每行和每列的主机数量，第二次遍历时统计结果，当存在主机并且所在行或所在列不止一台主机时，这一台主机就纳入计算。

时间复杂度 O(mn)，空间复杂度 O(m+n)

```c++
class Solution {
public:
    int countServers(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size(), res = 0;
        vector<int> row(m), col(n);
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(grid[i][j]){
                    row[i]++;
                    col[j]++;
                }
            }
        }
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(grid[i][j] && (row[i] > 1 || col[j] > 1))    
                    res++;
            }
        }
        return res;
    }
};
```

Runtime: 44 ms, faster than 98.26% of C++ online submissions forCount Servers that Communicate.

Memory Usage: 22.3 MB, less than 64.42% of C++ online submissions for Count Servers that Communicate.





一个不采取辅助空间的算法是，先检查一行（列）是否达到 `2` 台主机，如果是则把这一行（列）中的所有存在主机的位置从 `1` 改成 `2` ，最后统计 `2` 的数量。

时间复杂度 O(mn)，空间复杂度 O(1)

```c++
class Solution {
public:
    int countServers(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size(), res = 0;
        for(int i = 0; i < m; ++i){
            int cnt = 0, flag = 0;
            for(int j = 0; j < n; ++j){
                if(grid[i][j]) cnt++;
                if(cnt == 2){
                    flag = 1;
                    break;
                }
            }
            if(flag){
                for(int j = 0; j < n; ++j){
                    if(grid[i][j])  grid[i][j] = 2;
                }
            }
        }
        for(int j = 0; j < n; ++j){
            int cnt = 0, flag = 0;
            for(int i = 0; i < m; ++i){
                if(grid[i][j]) cnt++;
                if(cnt == 2){
                    flag = 1;
                    break;
                }
            }
            if(flag){
                for(int i = 0; i < m; ++i){
                    if(grid[i][j])  grid[i][j] = 2;
                }
            }
        }
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                if(grid[i][j] == 2) res++;
            }
        }
        return res;
    }
};
```

Runtime: 52 ms, faster than 85.96% of C++ online submissions forCount Servers that Communicate.

Memory Usage: 22 MB, less than 99.56% of C++ online submissions forCount Servers that Communicate.