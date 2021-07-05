# 556 Reshape the Matrix

[https://leetcode.com/problems/reshape-the-matrix/](https://leetcode.com/problems/reshape-the-matrix/)

In MATLAB, there is a handy function called `reshape` which can reshape an `m x n` matrix into a new one with a different size `r x c` keeping its original data.

You are given an `m x n` matrix `mat` and two integers `r` and `c` representing the row number and column number of the wanted reshaped matrix.

The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.

If the `reshape` operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/04/24/reshape1-grid.jpg)

```
Input: mat = [[1,2],[3,4]], r = 1, c = 4
Output: [[1,2,3,4]]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/04/24/reshape2-grid.jpg)

```
Input: mat = [[1,2],[3,4]], r = 2, c = 4
Output: [[1,2],[3,4]]
```

 

**Constraints:**

- `m == mat.length`
- `n == mat[i].length`
- `1 <= m, n <= 100`
- `-1000 <= mat[i][j] <= 1000`
- `1 <= r, c <= 300`



## Direct Solution

首先判断输入的 r c 是否合理，也就是两个矩阵容量相等；输入非法时直接返回原矩阵。映射到新矩阵时，按行遍历逐一存入，存满一行时将行坐标加一，列坐标清零。

时间复杂度 O(m*n)，空间复杂度 O(1)

也可以二维转一维再转二维，但这就复杂化了，还会增加空间复杂度到 O(m*n)。

```c++
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& mat, int r, int c) {
        int m = mat.size();
        int n = mat[0].size();
        int p = 0, q = 0;
        if(m * n != r * c)
            return mat;
        vector<vector<int> > newmt(r, vector<int> (c));
        for(int i = 0; i < m; ++i){
            for(int j = 0; j < n; ++j){
                newmt[p][q++] = mat[i][j];
                if(q == c){
                    p++; q = 0;
                }
            }
        }
        return newmt;
    }
};
```

Runtime: 8 ms, faster than 93.43% of C++ online submissions for Reshape the Matrix.

Memory Usage: 10.7 MB, less than 82.31% of C++ online submissions for Reshape the Matrix.