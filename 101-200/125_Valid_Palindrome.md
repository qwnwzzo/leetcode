### 125. Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Note:** For the purpose of this problem, we define empty string as valid palindrome.

**Example 1:**
```
Input: "A man, a plan, a canal: Panama"
Output: true
```

**Example 2:**
```
Input: "race a car"
Output: false
```

**Solution**
```Python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if len(s) == 0:
            return True

        i = 0
        j = len(s) - 1
        s = s.lower()
        while i <= j:
            if not s[i].isalnum():
                i += 1
            elif not s[j].isalnum():
                j -= 1
            elif s[i] != s[j]:
                return False
            else:
                i += 1
                j -= 1

        return True
```