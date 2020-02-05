### 516. Longest Palindromic Subsequence

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

**Example 1:**
```
Input:
"bbbab"

Output:
4

One possible longest palindromic subsequence is "bbbb".
```

**Example 2:**
```
Input:
"cbbd"

Output:
2

One possible longest palindromic subsequence is "bb".
```

**Solution**
```Python
class Solution(object):
    def longestPalindromeSubseq(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)
        if n == 0 or n == 1:
            return n
        
        dp = [[0] * n for _ in range(n)]
        for i in range(n):
            dp[i][i] = 1
        
        for i in range(n - 1, -1, -1):
            for j in range(i + 1, n):
                if s[i] == s[j]:
                    dp[i][j] = dp[i + 1][j - 1] + 2
                else:
                    dp[i][j] = max(dp[i][j - 1], dp[i + 1][j])
        
        return dp[0][n - 1]
```