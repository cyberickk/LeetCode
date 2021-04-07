# 1704 Determine if String Halves Are Alike

[https://leetcode.com/problems/determine-if-string-halves-are-alike/](https://leetcode.com/problems/determine-if-string-halves-are-alike/)

You are given a string `s` of even length. Split this string into two halves of equal lengths, and let `a` be the first half and `b` be the second half.

Two strings are **alike** if they have the same number of vowels (`'a'`, `'e'`, `'i'`, `'o'`, `'u'`, `'A'`, `'E'`, `'I'`, `'O'`, `'U'`). Notice that `s` contains uppercase and lowercase letters.

Return `true` *if* `a` *and* `b` *are **alike***. Otherwise, return `false`.

 

**Example 1:**

```
Input: s = "book"
Output: true
Explanation: a = "bo" and b = "ok". a has 1 vowel and b has 1 vowel. Therefore, they are alike.
```

**Example 2:**

```
Input: s = "textbook"
Output: false
Explanation: a = "text" and b = "book". a has 1 vowel whereas b has 2. Therefore, they are not alike.
Notice that the vowel o is counted twice.
```

**Example 3:**

```
Input: s = "MerryChristmas"
Output: false
```

**Example 4:**

```
Input: s = "AbCdEfGh"
Output: true
```

 

**Constraints:**

- `2 <= s.length <= 1000`
- `s.length` is even.
- `s` consists of **uppercase and lowercase** letters.



## Solution

直接拆分出两个字符串，分别数元音字母的个数。可以用 `set` 存储字母用来检查。

时间复杂度 O(n)，空间复杂度 O(n)

```c++
class Solution {
public:
    bool halvesAreAlike(string s) {
        set<char> vowel;
        string vowels = "aeiouAEIOU";
        for(int i = 0; i <  10; ++i)
            vowel.insert(vowels[i]);
        int acnt = 0, bcnt = 0;
        int n = s.size();
        string a = s.substr(0, n/2);
        string b = s.substr(n/2, n/2);
        for(int i = 0; i < n/2; ++i){
            if(vowel.count(a[i]))   ++acnt;
            if(vowel.count(b[i]))   ++bcnt;
        }
        return acnt == bcnt;
    }
};
```

Runtime: 4 ms, faster than 73.02% of C++ online submissions forDetermine if String Halves Are Alike.

Memory Usage: 6.9 MB, less than 9.14% of C++ online submissions forDetermine if String Halves Are Alike.



除了用 `set` 存储，也可以直接罗列十个字母进行判定，同时不需要存储两个子字符串，直接用下标定位即可，减少空间占用。

时间复杂度 O(n)，空间复杂度 O(1)

```c++
class Solution {
public:
    bool halvesAreAlike(string s) {
        int acnt = 0, bcnt = 0;
        int n = s.size();
        for(int i = 0; i < n/2; ++i){            if(s[i]=='a'||s[i]=='A'||s[i]=='e'||s[i]=='E'||s[i]=='i'||s[i]=='I'||s[i]=='o'||s[i]=='O'||s[i]=='u'||s[i]=='U')
    ++acnt;
        }
        for(int i = n/2; i < n; ++i){            if(s[i]=='a'||s[i]=='A'||s[i]=='e'||s[i]=='E'||s[i]=='i'||s[i]=='I'||s[i]=='o'||s[i]=='O'||s[i]=='u'||s[i]=='U')
    ++bcnt;
        }
        return acnt == bcnt;
    }
};
```

Runtime: 4 ms, faster than 73.02% of C++ online submissions forDetermine if String Halves Are Alike.

Memory Usage: 6.5 MB, less than 86.72% of C++ online submissions forDetermine if String Halves Are Alike.