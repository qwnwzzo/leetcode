### 279. Perfect Squares

Given a positive integer n, find the least number of perfect square numbers (for example, `1, 4, 9, 16, ...`) which sum to n.

**Example 1:**
```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```

**Example 2:**
```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```

**Solution**
```Python
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp = [float("inf")] * (n + 1)
        i = 0
        while i * i <= n:
            dp[i * i] = 1
            i += 1

        for i in range(n + 1):
            j = 1
            while j * j <= i:
                dp[i] = min(dp[i - j * j] + 1, dp[i])
                j += 1

        return dp[-1]        
```