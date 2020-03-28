# 003 无重复字符的最长子串 Longest Substring Without Repeating Characters [Medium]

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```



用 begin 和 end 指示子串的头尾，用数组记录字符是否在子串中出现过。如果当前遍历到的字符 c 已经出现过，那么把 begin 到 字符 c 之间的对应数组位置都重置为 0，同时更新 begin 值到 c 的下一位。ans 记录当前无重复字符的最大子串长度，max 记录所有无重复字符子串的最大值。

时间复杂度 O(n)，空间复杂度 O(1)，仅使用常量空间

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        if(n == 0 || n == 1) return n;
        int exist[256] = {0};
        int begin = 0, end = 0, ans = 0, max = 0;
        for(int i = 0; i < n; ++i) {           
            if(exist[s[i]] != 0) {
                while(s[begin] != s[i])
                    exist[s[begin++]] = 0;
                begin++;              
            }
            exist[s[i]] = 1;
            end = i;
            ans = end - begin + 1;
            if(ans > max) max = ans;
        }
        return max;
    }
};
```



也可以不使用数组记录字符出现情况，每一轮循环都从 begin 开始检查是否出现过当前的字符，出现过则更新 begin 值。

在最坏情况下（字符串是很多个长度为 26 的无重复字符子串）每一个子串都要从头遍历到尾，不过最长子串长度也只有 26，所以时间复杂度仍然是 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        if(n == 0 || n == 1) return n;
        int begin = 0, end = 0, ans = 0, max = 0;
        for(int i = 0; i < n; ++i) {           
            for(int j = begin; j < i; ++j) {
                if(s[j] == s[i]) {
                    begin = j+1;
                    break;
                }
            }
            end = i;
            ans = end - begin + 1;
            if(ans > max) max = ans;
        }
        return max;
    }
};
```

