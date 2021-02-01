# 1025 Divisor Game

Alice and Bob take turns playing a game, with Alice starting first.

Initially, there is a number `N` on the chalkboard. On each player's turn, that player makes a *move* consisting of:

- Choosing any `x` with `0 < x < N` and `N % x == 0`.
- Replacing the number `N` on the chalkboard with `N - x`.

Also, if a player cannot make a move, they lose the game.

Return `True` if and only if Alice wins the game, assuming both players play optimally.



**Example 1:**

```
Input: 2
Output: true
Explanation: Alice chooses 1, and Bob has no more moves.
```

**Example 2:**

```
Input: 3
Output: false
Explanation: Alice chooses 1, Bob chooses 1, and Alice has no more moves.
```

 

**Note:**

1. `1 <= N <= 1000`



给定一个数字 N，说出它的因子 x  `0 < x < N` ，同时 N 替换为 N-x，直到结束；两人轮流，Alice 先手。判断 Alice 是否获胜。

`N = 1` 没有可供选择的因子，Alice 失败；

`N = 2` Alice说出 1，`N = 1` ，对方失败 Alice 获胜；

`N = 3` Alice 只能选择 1，`N = 2` ，同上对方获胜 Alice 失败；

`N = 4` Alice 选择 1 或 2，选择 1 则 `N = 3` ，对方失败 Alice 获胜，选择 2 则 `N = 2` 对方获胜，Alice 应该选择 1 

依次类推，游戏的关键在于谁轮到 `N = 1` 则自动失败，谁轮到 `N = 2` 可以自动成功。同时有一个前提是奇数的因子只有奇数，偶数的因子含有奇数（1）和偶数；因此 Alice 获胜的关键是确保自己得到 `N = 2` 。当面对偶数时，选择说奇数因子，偶数 - 奇数 = 奇数，对方轮到奇数；当面对奇数时，说出的因子一定是奇数，奇数 - 奇数 = 偶数，对方轮到偶数。

因此 Alice 首轮面对面对偶数，只要选择说奇数因子，把奇数传给对方，传回给自己的就一定是偶数，最终会得到 `N = 2`  取得胜利；而首轮如果是奇数，只能把偶数传给对方，对方拥有了偶数的制胜权，Alice 会失败。

确定这个逻辑后只用判断 `N` 的奇偶性就可以得到结果，一行代码的运行时间与内存消耗都可以做到 100% 击败。

```c++
class Solution {
public:
    bool divisorGame(int N) {
        if(N % 2 == 0)  return true;
        return false;
    }
};
```

