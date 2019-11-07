### 131. Palindrome Partitioning

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

**Example:**
```
Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```

**Solution**
```Python
class Solution(object):
    def is_palindrome(self, s):
        l = 0
        r = len(s) - 1
        while l < r:
            if s[l] != s[r]:
                return False
            l += 1
            r -= 1
        
        return True
    
    def helper(self, ans, s, subset, index):
        if index == len(s):
            ans.append(subset[:])
            return
        
        for i in range(index, len(s)):
            if self.is_palindrome(s[index: i + 1]):
                subset.append(s[index: i + 1])
                self.helper(ans, s, subset, i + 1)
                subset.pop()
        
    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        if len(s) == 0:
            return []
        
        ans = []
        self.helper(ans, s, [], 0)
            
        return ans
```