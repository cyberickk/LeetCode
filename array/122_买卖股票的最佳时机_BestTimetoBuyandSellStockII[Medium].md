# 122 买卖股票的最佳时机 Best Time to Buy and Sell Stock II [Medium]

**题目分析：** 可以多次买卖股票，每个上升序列的最大差值等于每两点差值之和，所以每次价格上升都把两点差值计入总利润

**复杂度：** 时间复杂度 O(n),  空间复杂度 O(1)



```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int ans = 0;
        for(int i = 1; i < prices.size(); ++i)
        {
            if(prices[i] > prices[i-1])
                ans += prices[i] - prices[i-1];
        }
        return ans;
    }
};
```

