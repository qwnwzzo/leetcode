### 409. Longest Palindrome

Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

This is case sensitive, for example "Aa" is not considered a palindrome here.

**Note:**
Assume the length of given string will not exceed 1,010.

**Example:**
```
Input:
"abccccdd"

Output:
7

Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
```

**Solution**
```Python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: int
        """
        m = {}
        for c in s:
            if c not in m:
                m[c] = 0
            m[c] += 1
        
        ans = 0
        for c in m:
            if m[c] % 2 == 0:
                ans += m[c]
            elif m[c] > 1:
                ans += m[c] - 1
        
        for c in m:
            if m[c] % 2 == 1:
                ans += 1
                break
        
        return ans
```