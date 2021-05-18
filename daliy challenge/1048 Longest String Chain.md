

# 1048 Longest String Chain

[https://leetcode.com/problems/longest-string-chain/](https://leetcode.com/problems/longest-string-chain/)



Given a list of words, each word consists of English lowercase letters.

Let's say `word1` is a predecessor of `word2` if and only if we can add exactly one letter anywhere in `word1` to make it equal to `word2`. For example, `"abc"` is a predecessor of `"abac"`.

A *word chain* is a sequence of words `[word_1, word_2, ..., word_k]` with `k >= 1`, where `word_1` is a predecessor of `word_2`, `word_2` is a predecessor of `word_3`, and so on.

Return the longest possible length of a word chain with words chosen from the given list of `words`.

 

**Example 1:**

```
Input: words = ["a","b","ba","bca","bda","bdca"]
Output: 4
Explanation: One of the longest word chain is "a","ba","bda","bdca".
```

**Example 2:**

```
Input: words = ["xbc","pcxbcf","xb","cxbc","pcxbc"]
Output: 5
```

 

**Constraints:**

- `1 <= words.length <= 1000`
- `1 <= words[i].length <= 16`
- `words[i]` only consists of English lowercase letters.



<br>

## Dynamic Programming Solution

前序字符串首先要求长度只相差 1，因此先把字符串按长度升序排列。

运用动态规划的思想，从前往后检查，记录以每个字符串作为终点的词链有多长，在前序字符串的结果上累加，得到全局的最大值。

- 初始值 `v[i] = 1` ，表示每个字符串为终点时，词链长度至少是 1
- 累加关系，当 i 是 j 的前序时，`v[j] = max(v[i], v[j])` 

判断两个字符串 a 和 b 是否满足前序关系：

- a 比 b 的长度小 1
- 两个指针 i, j 分别指向 a, b开头，如果两个字母相同则共同向后一位，否则 j 向后一位
- 要求只有一位字母不同，其他字母的相对顺序一致。如果满足这个条件，那么 j 到达终点后，i 也相应地到达终点，由此判断是否满足前序关系

假设共 n 个字符串，字符串长度 m，时间复杂度 O(n^2 * m)，空间复杂度 O(n)

```c++
class Solution {
public:
    int longestStrChain(vector<string>& words) {
        sort(words.begin(), words.end(), cmp);
        int n = words.size(), ans = 0;
        vector<int> v(n, 1);
        for(int i = 0; i < n; ++i){
            for(int j = i-1; j >= 0 && words[j].size() + 1 >= words[i].size(); --j)
                if(isPre(words[j], words[i]))
                    v[i] = max(v[i], v[j]+1);
            ans = max(ans, v[i]);
        }
        return ans;
    }
    
    static bool cmp(string& a, string& b){
        return a.size() < b.size();
    }
    
    static bool isPre(string& a, string& b){
        if(a.size() + 1 != b.size())
            return 0;
        int i = 0, j = 0;
        while(j < b.size()){
            if(a[i] == b[j]){
                i++; j++;
            }
            else
                j++;
        }
        return i == a.size();
    }
};
```



Runtime: 104 ms, faster than 47.54% of C++ online submissions for Longest String Chain.

Memory Usage: 13.1 MB, less than 91.49% of C++ online submissions for Longest String Chain.