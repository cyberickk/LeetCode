# 066 加一 Plus One [Easy]



## 解法一

穷举各种情况，最后一位小于 9，最后一位进位中间不进位，全部进一位。

其实可以不用新开辟数组，直接修改 digits 后返回即可。

时间复杂度 O(n)，空间复杂度 O(n) 

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();
        vector<int> ans;
        if(digits[n-1] < 9)
        {
            ans.resize(n);
            ans[n - 1] = digits[n-1] + 1;
            for(int j = 0; j < n-1; ++j)
                ans[j] = digits[j];
        }
        else
        {
            ans.resize(n+1);
            ans[n] = 0;
            int flag = 1;
            for(int j = n - 2; j >= 0; --j)
            {
                if(digits[j] + flag < 10) 
                {
                    ans[j+1] = digits[j] + flag;
                    flag = 0;
                }
                else
                {
                    ans[j+1] = 0;
                    flag = 1;
                }
            }
            if(flag == 1) ans[0] = 1;
            else
            {
                for(int k = 1; k <= n; ++k)
                    ans[k-1] = ans[k];
                ans.pop_back();
            }
        }
        return ans;
    }
};
```



## 解法二

如果最后一位小于 9 则直接加一后返回；否则最后一位置 0，继续往前遍历，仍然是小于 9 就加一返回，如果每一位都产生进位，则在数组首位插入 1 并返回。

时间复杂度 O(n)，空间复杂度 O(1) 

```c++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for(int i = digits.size() - 1; i >= 0; --i) {
            if(digits[i] != 9) {
                digits[i]++;
                return digits;
            }
            else 
                digits[i] = 0;
        }
        digits.insert(digits.begin(), 1);
        return digits;
    }
};
```

