### 921. Minimum Add to Make Parentheses Valid

Given a string S of '(' and ')' parentheses, we add the minimum number of parentheses ( '(' or ')', and in any positions ) so that the resulting parentheses string is valid.

Formally, a parentheses string is valid if and only if:

It is the empty string, or
It can be written as AB (A concatenated with B), where A and B are valid strings, or
It can be written as (A), where A is a valid string.
Given a parentheses string, return the minimum number of parentheses we must add to make the resulting string valid.

**Example 1:**
```
Input: "())"
Output: 1
```

**Example 2:**
```
Input: "((("
Output: 3
```

**Example 3:**
```
Input: "()"
Output: 0
```

**Example 4:**
```
Input: "()))(("
Output: 4
```

**Note:**
- S.length <= 1000
- S only consists of '(' and ')' characters.

**Solution**
```Python
class Solution(object):
    def minAddToMakeValid(self, S):
        """
        :type S: str
        :rtype: int
        """
        if len(S) <= 1:
            return len(S)

        stack = []
        ans = 0
        for c in S:
            if c == "(":
                stack.append(c)
            else:
                if len(stack) == 0 or stack[-1] != "(":
                    ans += 1
                else:
                    stack.pop()
        
        return ans + len(stack)
```