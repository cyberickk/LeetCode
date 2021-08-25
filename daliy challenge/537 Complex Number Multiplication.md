# 537 Complex Number Multiplication



[https://leetcode.com/problems/complex-number-multiplication/](https://leetcode.com/problems/complex-number-multiplication/)

<br>



A [complex number](https://en.wikipedia.org/wiki/Complex_number) can be represented as a string on the form `"**real**+**imaginary**i"` where:

- `real` is the real part and is an integer in the range `[-100, 100]`.
- `imaginary` is the imaginary part and is an integer in the range `[-100, 100]`.
- `i2 == -1`.

Given two complex numbers `num1` and `num2` as strings, return *a string of the complex number that represents their multiplications*.

 

**Example 1:**

```
Input: num1 = "1+1i", num2 = "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
```

**Example 2:**

```
Input: num1 = "1+-1i", num2 = "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```

 

**Constraints:**

- `num1` and `num2` are valid complex numbers.





## Basic Solution

思路很简单，从两个字符串中提取出复数的实部和虚部，交叉相乘得到乘积的实部和虚部，按题目格式返回复数字符串。重点在于字符串的处理。

第一遍写得比较冗长，遍历字符串，找到 `'+'` 时分割，得到实部和虚部；返回时注意加上 `'+'` `'i'` 

时间复杂度 O(n)，空间复杂度 O(1)

```cpp
class Solution {
public:
    string complexNumberMultiply(string num1, string num2) {
        int a1, b1, a2, b2, c1, c2;
        string s, ans;
        for(int i = 0; i < num1.size(); ++i){
            if(num1[i] == '+'){
                a1 = stoi(num1.substr(0, i));
                s = num1.substr(i+1);
                s.pop_back();
                b1 = stoi(s);
                break;
            }
        }
        for(int i = 0; i < num2.size(); ++i){
            if(num2[i] == '+'){
                a2 = stoi(num2.substr(0, i));
                s = num2.substr(i+1);
                s.pop_back();
                b2 = stoi(s);
                break;
            }
        }
        c1 = a1 * a2 - b1 * b2;
        c2 = a1 * b2 + a2 * b1;
        ans = to_string(c1);
        s = to_string(c2);
        ans.append(1, '+');		// ans.push_back('+');
        ans += s;
        ans.append(1, 'i');		// ans.push_back('i');
        return ans;
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Complex Number Multiplication.

Memory Usage: 5.9 MB, less than 61.85% of C++ online submissions for Complex Number Multiplication.

<br>

## Optimization

代码可以写得很精炼，利用 `sscanf` 直接得到整数部分，返回时也可以直接完成字符串拼接操作。重点是 c_str 的格式化读取。

```cpp
class Solution {
public:
    string complexNumberMultiply(string num1, string num2) {
        int a1, b1, a2, b2;
        sscanf(num1.c_str(), "%d+%di", &a1, &b1);
        sscanf(num2.c_str(), "%d+%di", &a2, &b2);
        return to_string(a1 * a2 - b1 * b2) + "+" + to_string(a1 * b2 + a2 * b1) + "i";
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Complex Number Multiplication.

Memory Usage: 6 MB, less than 61.85% of C++ online submissions for Complex Number Multiplication.

