# 1021 移除最外层的括号 Remove Outermost Parentheses



A valid parentheses string is either empty `("")`, `"(" + A + ")"`, or `A + B`, where `A` and `B` are valid parentheses strings, and `+` represents string concatenation. For example, `""`, `"()"`, `"(())()"`, and `"(()(()))"` are all valid parentheses strings.

A valid parentheses string `S` is **primitive** if it is nonempty, and there does not exist a way to split it into `S = A+B`, with `A` and `B` nonempty valid parentheses strings.

Given a valid parentheses string `S`, consider its primitive decomposition: `S = P_1 + P_2 + ... + P_k`, where `P_i` are primitive valid parentheses strings.

Return `S` after removing the outermost parentheses of every primitive string in the primitive decomposition of `S`.

 

**Example 1:**

```
Input: "(()())(())"
Output: "()()()"
Explanation: 
The input string is "(()())(())", with primitive decomposition "(()())" + "(())".
After removing outer parentheses of each part, this is "()()" + "()" = "()()()".
```

**Example 2:**

```
Input: "(()())(())(()(()))"
Output: "()()()()(())"
Explanation: 
The input string is "(()())(())(()(()))", with primitive decomposition "(()())" + "(())" + "(()(()))".
After removing outer parentheses of each part, this is "()()" + "()" + "()(())" = "()()()()(())".
```

**Example 3:**

```
Input: "()()"
Output: ""
Explanation: 
The input string is "()()", with primitive decomposition "()" + "()".
After removing outer parentheses of each part, this is "" + "" = "".
```

 

**Note:**

1. `S.length <= 10000`
2. `S[i]` is `"("` or `")"`
3. `S` is a valid parentheses string



## 解法一 栈

用栈存储左括号，遍历到右括号时弹出栈顶。栈的元素大于 1 时把括号添加入 ans 中，以此去除最外层括号。

时间复杂度 O(n)， 空间复杂度 O(n)

```c++
class Solution {
public:
    string removeOuterParentheses(string S) {
        string ans;
        stack<char> st;
        for(char ch:S) {
            if(ch == '(') {
                st.push(ch);
                if(st.size() > 1)
                    ans += ch; 
            }                
            else {
                if(st.size() > 1)
                    ans += ch;
                st.pop(); 
            }              
        }
        return ans;
    }
};
```



## 解法二 计数

用 L R 计数左右括号数，第一个元素一定是左括号，从第二个元素开始遍历，左右数不相等则加入括号到 ans 中

```c++
class Solution {
public:
    string removeOuterParentheses(string S) {
int L=1;int R=0;
        string ans;
        for(int i=1;i<S.size();i++){
            if(S[i]=='(')L++;
            else R++;
            if(R!=L)ans.push_back(S[i]);
            else {
                i++;L=1;R=0;
            }
        }
        return ans;

    }
};
```

