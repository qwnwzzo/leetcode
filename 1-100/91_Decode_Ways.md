### 91. Decode Ways

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given a non-empty string containing only digits, determine the total number of ways to decode it.

**Example 1:**
```
Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**
```
Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

**Solution**
```Python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)
        
        if n == 0 or s[0] == '0':
            return 0
        
        dp = [0 for i in range(n + 1)]
        dp[0] = 1
        dp[1] = 1
        
        for i in range(2, n + 1):
            one_digit = int(s[i - 1])
            two_digits = int(s[i - 2: i])
            
            if one_digit >= 1 and one_digit <= 9:
                dp[i] += dp[i - 1]
            
            if two_digits >= 10 and two_digits <= 26:
                dp[i] += dp[i - 2]
        
        return dp[n]
```