### 3. Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

**Example 1:**
```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3.
```

**Example 2:**
```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**
```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

**Solution**
```Python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        window = {}
        ans = 0
        left = 0
        right = 0

        while right < len(s):
            c = s[right]
            if c not in window:
                window[c] = 0
            window[c] += 1
            right += 1

            while window[c] > 1:
                left_c = s[left]
                window[left_c] -= 1
                left += 1
            
            ans = max(ans, right - left)
        
        return ans
```
