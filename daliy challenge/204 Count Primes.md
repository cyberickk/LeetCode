# 204 Count Primes

[https://leetcode.com/problems/count-primes/](https://leetcode.com/problems/count-primes/)

Count the number of prime numbers less than a non-negative number, `n`.

 

**Example 1:**

```
Input: n = 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

**Example 2:**

```
Input: n = 0
Output: 0
```

**Example 3:**

```
Input: n = 1
Output: 0
```

 

**Constraints:**

- `0 <= n <= 5 * 106`



### Basic Solution

首先判断是否为素数，也就是找因子，大于平方根的因子，其相对因子一定在小于平方根的范围内。因此只要检查平方根以内的数，都不能整除就可以确定是素数。其次对给定的 `n` 去遍历每一个数判断是否为素数。

时间复杂度 O(nlogn)，空间复杂度 O(1)

但是运行超时

```
20 / 21 test cases passed.
Last executed input:
5000000
```



```c++
class Solution {
public:
    int countPrimes(int n) {
        int cnt = 0;
        for(int i = 0; i < n; ++i)
            if(isPrime(i))
                cnt++;
        return cnt;
    }
    
    bool isPrime(int n){
        if(n < 2)   return 0;
        for(int i = 2; i * i <= n; ++i){
            if(n % i == 0)
                return 0;
        }
        return 1;
    }
};
```



### Sieve of Eratosthenes

[https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

根据其中的原理，2，3，5，7等等前面的素数作为基本的素数，把它们的倍数全部排除，剩余的就是素数。注意到倍数从平方算起，因为小于平方的倍数（2倍，3倍……）在前面就已经排除过了。按照判断一个数是否是素数的规则，检查过平方根以内的数就足够。

时间复杂度 O(n loglogn)，空间复杂度 O(n)

```c++
class Solution {
public:
    int countPrimes(int n) {
        vector<bool> isPrime(n, 1);
        for(int i = 2; i * i < n; ++i){
            if(!isPrime[i])
                continue;
            for(int j = i * i; j < n; j += i){
                isPrime[j] = 0;
            }
        }
        int cnt = 0;
        for(int i = 2; i < n; ++i)
            if(isPrime[i])
                cnt++;
        return cnt;
    }
};
```



```
Runtime: 36 ms, faster than 68.67% of C++ online submissions for Count Primes.
Memory Usage: 7.1 MB, less than 51.33% of C++ online submissions for Count Primes.
```

