# 844 Backspace String Compare

[https://leetcode.com/problems/backspace-string-compare/submissions/](https://leetcode.com/problems/backspace-string-compare/submissions/)

<br>

Given two strings `s` and `t`, return `true` *if they are equal when both are typed into empty text editors*. `'#'` means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

 

**Example 1:**

```
Input: s = "ab#c", t = "ad#c"
Output: true
Explanation: Both s and t become "ac".
```

**Example 2:**

```
Input: s = "ab##", t = "c#d#"
Output: true
Explanation: Both s and t become "".
```

**Example 3:**

```
Input: s = "a##c", t = "#a#c"
Output: true
Explanation: Both s and t become "c".
```

**Example 4:**

```
Input: s = "a#c", t = "b"
Output: false
Explanation: s becomes "c" while t becomes "b".
```

 

**Constraints:**

- `1 <= s.length, t.length <= 200`
- `s` and `t` only contain lowercase letters and `'#'` characters.



<br>



## Edit String Solution

按照题目要求，碰到 '#' 时删除前面一位，最后检查两个字符串是否相同。

时间复杂度 O(n)，空间复杂度 O(n)

```c++
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        string s1, s2;
        s1 = editStr(s);
        s2 = editStr(t);
        return s1 == s2;
    }
    string editStr(string& s){
        string s1;
        for(int i = 0; i < s.size(); ++i){
            if(s[i] == '#'){
                if(s1.size() < 1)
                    continue;
                else
                    s1.pop_back();
            }
            else
                s1.append(1, s[i]);
        }
        return s1;
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Backspace String Compare.

Memory Usage: 6.3 MB, less than 53.41% of C++ online submissions for Backspace String Compare.





<br>

简化版本

```c++
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        string s1, s2;
        for(int i = 0; i < s.size(); ++i){
            if(s[i] != '#')
                s1.append(1, s[i]);
            else if(s1.size() > 0)
                s1.pop_back();
        }
        for(int i = 0; i < t.size(); ++i){
            if(t[i] != '#')
                s2.append(1, t[i]);
            else if(s2.size() > 0)
                s2.pop_back();
        }
        return s1 == s2;
    }
};
```





## Two Pointers Solution







```c++
class Solution {
public:
    bool backspaceCompare(string s, string t) {
        int ptrs = s.size() -1;
        int ptrt = t.size() -1;
        int bs = 0;
        int bt = 0;
        while(ptrs >= 0 || ptrt >= 0){
            // next vaild char in s
            while(ptrs >= 0){
                if(s[ptrs] == '#'){
                    bs++;
                }else if(bs){
                    bs--;
                }else{
                    break;
                }
                ptrs--;
            }
            
            // next vaild char in t
            while(ptrt >= 0){
                if(t[ptrt] == '#'){
                    bt++;
                }else if(bt){
                    bt--;
                }else{
                    break;
                }
                ptrt--;
            }
            
            if(ptrt >= 0 && ptrs >= 0 && t[ptrt] != s[ptrs]){
                return false;
            }
            
            if( (ptrt < 0) != (ptrs < 0) ){
                return false;
            }
            ptrs--;
            ptrt--;
        }
        return true;
    }
};
```

