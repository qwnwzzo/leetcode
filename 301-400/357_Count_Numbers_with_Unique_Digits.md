### 357. Count Numbers with Unique Digits

Given a **non-negative** integer n, count all numbers with unique digits, x, where 0 ≤ x < 10n.

**Example:**
```
Input: 2
Output: 91 
Explanation: The answer should be the total numbers in the range of 0 ≤ x < 100, 
             excluding 11,22,33,44,55,66,77,88,99
```

**Idea**
```
对于dp的做法：
设dp[i]表示i位数时满足题意的数的个数。
对于第i位，为了使得第i位与前i-1位的数字不一致，我们可以选择数字应该有10-(i-1)10−(i−1)个，因此转移方程为：dp[i]=dp[i-1]*(11-i)dp[i]=dp[i−1]∗(11−i)
```

**Solution**
```Python
class Solution(object):
    def countNumbersWithUniqueDigits(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 0:
            return 1
        
        if n == 1:
            return 10

        dp = [0] * (n + 1)
        dp[0] = 1
        dp[1] = 9

        ans = 10
        for i in range(2, n + 1):
            dp[i] = dp[i - 1] * (11 - i)
            ans += dp[i]
        
        return ans
```