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

**Idea**
```
枚举, 记录每一个字母上一次出现的位置.

再设定一个左边界, 到当前枚举到的位置之间的字符串为不含重复字符的子串.

若新碰到的字符的上一次的位置在左边界右边, 则需要向右移动左边界, 枚举的过程中取最大值即可.
```

**Solution**
```Python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)
        left_border = 0
        ans = 0
        m = {}
        
        for i in range(n):
            if s[i] in m:
                left_border = max(m[s[i]] + 1, left_border)
            
            ans = max(ans, i - left_border + 1)
            m[s[i]] = i
        
        return ans
```
