### 5. Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

**Example 1:**
```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**
```
Input: "cbbd"
Output: "bb"
```

**Solution**
```Python
class Solution(object):
    def len_of_palindrome(self, s, i):
        len1 = 0
        len2 = 0
        l = i
        r = i
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        len1 = r - l - 1
        
        l = i
        r = i + 1
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        len2 = r - l - 1
        
        return max(len1, len2)
        
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if len(s) <= 1:
            return s
        
        ans = ""
        for i in range(len(s)):
            length = self.len_of_palindrome(s, i)
            if length > len(ans):
                start = i- (length - 1) / 2
                ans = s[start: start + length]
        
        return ans
```