### 132. Palindrome Partitioning II

Given a string s, partition s such that every substring of the partition is a palindrome.

Return the minimum cuts needed for a palindrome partitioning of s.

**Example:**
```
Input: "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
```

**Idea**
```
dp[i]表示前 i 个字符组成的子串，最少需要几次分割，才能变成都是回文串。

对于所有的 j < i， 如果s[j, i]是回文串, 且 dp[j] + 1 < dp[i] 则 dp[i] = dp[j] + 1。

初始化：dp[i] = i - 1，长度为 i 的子串，最多切 i - 1 次，都变成单个字符，就是回文串了。dp[0] = -1。
```

**Solution**
```Python
class Solution(object):
    def is_palindrome(self, s):
        return s == s[::-1]
    
    def minCut(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)
        dp = [i - 1 for i in range(n + 1)]
        
        for i in range(1, n + 1):
            if s[: i] == s[: i][::-1]:
                dp[i] = 0
            else:
                for j in range(0, i):
                    if self.is_palindrome(s[j: i]):
                        dp[i] = min(dp[i], dp[j] + 1)
        
        return dp[-1]
```