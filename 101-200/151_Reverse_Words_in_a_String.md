### 151. Reverse Words in a String

Given an input string, reverse the string word by word.

**Example 1:**
```
Input: "the sky is blue"
Output: "blue is sky the"
```

**Example 2:**
```
Input: "  hello world!  "
Output: "world! hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**
```
Input: "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

**Note:**
- A word is defined as a sequence of non-space characters.
- Input string may contain leading or trailing spaces. However, your reversed string should not contain leading or trailing spaces.
- You need to reduce multiple spaces between two words to a single space in the reversed string.
 

**Follow up:**
```
For C programmers, try to solve it in-place in O(1) extra space.
```

**Solution**
```Python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        s = s.strip()
        if len(s) == 0:
            return ""

        ans = ""
        anchor = 0
        i = 0

        while i < len(s):
            if s[i] == " ":
                ans = s[anchor: i] + " " + ans
                while s[i] == " ":
                    i += 1
                    if i == len(s):
                        break
                
                anchor = i
            else:
                i += 1
        
        ans = s[anchor:] + " " + ans
        
        return ans.strip()
```