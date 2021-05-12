# 1423 Maximum Points You Can Obtain from Cards

[https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/](https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/)

There are several cards **arranged in a row**, and each card has an associated number of points The points are given in the integer array `cardPoints`.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly `k` cards.

Your score is the sum of the points of the cards you have taken.

Given the integer array `cardPoints` and the integer `k`, return the *maximum score* you can obtain.

 

**Example 1:**

```
Input: cardPoints = [1,2,3,4,5,6,1], k = 3
Output: 12
Explanation: After the first step, your score will always be 1. However, choosing the rightmost card first will maximize your total score. The optimal strategy is to take the three cards on the right, giving a final score of 1 + 6 + 5 = 12.
```

**Example 2:**

```
Input: cardPoints = [2,2,2], k = 2
Output: 4
Explanation: Regardless of which two cards you take, your score will always be 4.
```

**Example 3:**

```
Input: cardPoints = [9,7,7,9,7,7,9], k = 7
Output: 55
Explanation: You have to take all the cards. Your score is the sum of points of all cards.
```

**Example 4:**

```
Input: cardPoints = [1,1000,1], k = 1
Output: 1
Explanation: You cannot take the card in the middle. Your best score is 1. 
```

**Example 5:**

```
Input: cardPoints = [1,79,80,1,1,1,200,1], k = 3
Output: 202
```

 

**Constraints:**

- `1 <= cardPoints.length <= 10^5`
- `1 <= cardPoints[i] <= 10^4`
- `1 <= k <= cardPoints.length`



## Sliding Window Algorithm

要从两头选取共 k 个数，也就是从中间排除连续的 n-k 个数，双指针指向头和尾，依次遍历所有可能的 k 个数总和，保留最大值。重点是滑动窗口的思想以及边界取值、避免越界的问题。

时间复杂度 O(n)，空间复杂度O(1)

```c++
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int n = cardPoints.size(), presum = 0, ans = 0;
        for(int i = 0; i < k; ++i) presum += cardPoints[i];
        ans = presum;
        for(int i = k-1, j = n-1; i >= 0; i--, j--){
            presum += cardPoints[j] - cardPoints[i];
            ans = max(ans, presum);
        }
        return ans;
    }
};
```



```
Runtime: 56 ms, faster than 63.42% of C++ online submissions for Maximum Points You Can Obtain from Cards.
Memory Usage: 42.4 MB, less than 77.11% of C++ online submissions for Maximum Points You Can Obtain from Cards.
```

