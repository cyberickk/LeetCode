# 1641 Count Sorted Vowel Strings

[https://leetcode.com/problems/count-sorted-vowel-strings/](https://leetcode.com/problems/count-sorted-vowel-strings/)



Given an integer `n`, return *the number of strings of length* `n` *that consist only of vowels (*`a`*,* `e`*,* `i`*,* `o`*,* `u`*) and are **lexicographically sorted**.*

A string `s` is **lexicographically sorted** if for all valid `i`, `s[i]` is the same as or comes before `s[i+1]` in the alphabet.

 

**Example 1:**

```
Input: n = 1
Output: 5
Explanation: The 5 sorted strings that consist of vowels only are ["a","e","i","o","u"].
```

**Example 2:**

```
Input: n = 2
Output: 15
Explanation: The 15 sorted strings that consist of vowels only are
["aa","ae","ai","ao","au","ee","ei","eo","eu","ii","io","iu","oo","ou","uu"].
Note that "ea" is not a valid string since 'e' comes after 'a' in the alphabet.
```

**Example 3:**

```
Input: n = 33
Output: 66045
```

 

**Constraints:**

- `1 <= n <= 50` 



## Dynamic Programming Solution



```c++
class Solution {
public:
    int countVowelStrings(int n) {
        vector< vector<int> > dp(n+1, vector<int> (6, 0));
        for(int i = 1; i < 6; ++i){
            dp[1][i] = 1;
            dp[1][0] += dp[1][i];
        }
        for(int i = 2; i <= n; ++i){
            for(int j = 1; j < 6; ++j){
                dp[i][j] = dp[i-1][0];
                for(int k = 1; k < j; ++k)
                    dp[i][j] -= dp[i-1][k];
                dp[i][0] += dp[i][j];
            }
        }
        return dp[n][0];
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Count Sorted Vowel Strings.

Memory Usage: 6.3 MB, less than 16.04% of C++ online submissions for Count Sorted Vowel Strings.