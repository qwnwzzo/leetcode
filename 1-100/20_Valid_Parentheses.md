### 20. Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

**Example 1:**
```
Input: "()"
Output: true
```

**Example 2:**
```
Input: "()[]{}"
Output: true
```

**Example 3:**
```
Input: "(]"
Output: false
```

**Example 4:**
```
Input: "([)]"
Output: false
```

**Example 5:**
```
Input: "{[]}"
Output: true
```

**Solution**
```Python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        if s is None or len(s) % 2 == 1:
            return False
        
        if s == "":
            return True

        stack = []
        for c in s:
            if c == "(" or c == "[" or c == "{":
                stack.append(c)
            elif len(stack) == 0:
                return False
            elif c == ")":
                if stack.pop() != "(":
                    return False
            elif c == "]":
                if stack.pop() != "[":
                    return False
            elif c == "}":
                if stack.pop() != "{":
                    return False
        
        return len(stack) == 0
```