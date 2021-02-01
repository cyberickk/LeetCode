# 997 Find the Town Judge

https://leetcode.com/problems/find-the-town-judge/

In a town, there are `N` people labelled from `1` to `N`. There is a rumor that one of these people is secretly the town judge.

If the town judge exists, then:

1. The town judge trusts nobody.
2. Everybody (except for the town judge) trusts the town judge.
3. There is exactly one person that satisfies properties 1 and 2.

You are given `trust`, an array of pairs `trust[i] = [a, b]` representing that the person labelled `a` trusts the person labelled `b`.

If the town judge exists and can be identified, return the label of the town judge. Otherwise, return `-1`.

 

**Example 1:**

```
Input: N = 2, trust = [[1,2]]
Output: 2
```

**Example 2:**

```
Input: N = 3, trust = [[1,3],[2,3]]
Output: 3
```

**Example 3:**

```
Input: N = 3, trust = [[1,3],[2,3],[3,1]]
Output: -1
```

**Example 4:**

```
Input: N = 3, trust = [[1,2],[2,3]]
Output: -1
```

**Example 5:**

```
Input: N = 4, trust = [[1,3],[1,4],[2,3],[2,4],[4,3]]
Output: 3
```

 

**Constraints:**

- `1 <= N <= 1000`
- `0 <= trust.length <= 10^4`
- `trust[i].length == 2`
- `trust[i]` are all different
- `trust[i][0] != trust[i][1]`
- `1 <= trust[i][0], trust[i][1] <= N`



## basic solution

所有人信任法官，法官不信任任何人。可以看作是有向图，一个点的入度为 `N-1` ，出度为 `0`，则为法官。创建两个数组分别存储入度和出度，寻找符合条件的节点并返回下标，否则返回 `-1` 。

时间复杂度 O(n)，空间复杂度 O(n)

```c++
class Solution {
public:
    int findJudge(int N, vector<vector<int>>& trust) {
        int j = -1;
        vector<int> in(N+1, 0), out(N+1, 0);
        for(int i = 0; i < trust.size(); ++i){
            in[trust[i][1]]++;
            out[trust[i][0]]++;
        }
        for(int i = 1; i < N+1; ++i){
            if(in[i] == N - 1){
                if(out[i] == 0)
                    j = i;                   
            }
        }
        return j;
    }
};
```



Runtime: 196 ms, faster than 78.82% of C++ online submissions for Find the Town Judge.

Memory Usage: 60.9 MB, less than 88.34% of C++ online submissions for Find the Town Judge.



## optimization 1

法官的判定条件可以等价为入度与出度的差值为 `N-1` ，因此可以只使用一个数组 `diff` 存储差值。对于二维数组中的每一对下标，前者代表出度 ，后者代表入度，也就是 `diff` 中前者的值 `-1`，后者的值 `+1`，可以实现记录差值。

程序部分的优化：不需要变量 `f` 记录结果，遍历过程中可以直接返回答案；遍历二维数组时使用智能指针可以简化代码，但是会增加内存消耗约 8MB 。

时间复杂度 O(n)，空间复杂度 O(n)

```c++
class Solution {
public:
    int findJudge(int N, vector<vector<int>>& trust) {
        vector<int> diff(N+1, 0);
        for(int i = 0; i < trust.size(); ++i){		// for(auto i : trust){diff[i[0]]--; diff[i[1]]++;}
            diff[trust[i][0]]--;
            diff[trust[i][1]]++;
        }
        for(int i = 1; i < N+1; ++i){
            if(diff[i] == N-1)    return i;
        }
        return -1;
    }
};
```



Runtime: 172 ms, faster than 86.69% of C++ online submissions for Find the Town Judge.

Memory Usage: 60.7 MB, less than 91.99% of C++ online submissions for Find the Town Judge.



## thinking

- basic solution 中是否存在多个符合条件的节点？

限制条件中包含 `trust[i][0] != trust[i][1]`，如果有多于一个节点的入度为 `N-1` ，那么每一个节点的出度必然不为 `0`，所以 同时满足两个条件的节点只会是 0 或者 1 个，查找到符合条件的节点时就可以直接返回结果。

- optimization 1 中为什么判定条件可以等价为入度与出度的差值为 `N-1` ？

即证明 `in == N-1 && out == 0` 等价于 `diff == N-1`，因为 `trust` 中不存在相同的元素，也就是不存在重复的边，同时也不存在指向自身的环；当入度和出度的差值是 `N-1`时，只可能有 `in == N-1 && out == 0` 这一种情况。