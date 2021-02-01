# 242 有效的字母异位词 Valid Anagram [Easy]

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的字母异位词。

**示例 1:**

```
输入: s = "anagram", t = "nagaram"
输出: true
```

**示例 2:**

```
输入: s = "rat", t = "car"
输出: false
```

**说明:**
你可以假设字符串只包含小写字母。

**进阶:**
如果输入字符串包含 unicode 字符怎么办？你能否调整你的解法来应对这种情况？





## 解法一 辅助数组

用两个数组记录字母出现次数，遍历两个数组比较对应项是否相等

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int a[26] = {0}, b[26] = {0};
        for(int i = 0; i < s.size(); ++i)
            a[s[i]-'a']++;
        for(int i = 0; i < t.size(); ++i)
            b[t[i]-'a']++;
        for(int i = 0; i < 26; ++i)
            if(a[i] != b[i]) return false;
        return true;
    }
};
```





## 解法二 排序

对两个数组进行排序，再遍历比较

时间复杂度 O(nlogn)，空间复杂度 O(1)

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if(s.size() != t.size()) return false;
        sort(s.begin(), s.end());
        sort(t.begin(), t.end());
        for(int i = 0; i < s.size(); ++i) {
            if(s[i] != t[i])
                return false;
        }
        return true;
    }
};
```

