# 387 字符串中的第一个唯一字符 First Unique Character in a String [Easy]

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```

 

**注意事项：**您可以假定该字符串只包含小写字母。



第一次遍历字符串用数组记录出现次数，再次遍历字符串并查阅次数，为 1 则输出。

时间复杂度 O(n) ，空间复杂度 O(1)

```c++
class Solution {
public:
    int firstUniqChar(string s) {
        int a[26] = {0};
        for(int i = 0; i < s.size(); ++i)
            a[s[i] - 'a']++;
        for(int i = 0; i < s.size(); ++i)
        {
            if(a[s[i] - 'a'] == 1) return i;
        }
        return -1;
    }
};
```

