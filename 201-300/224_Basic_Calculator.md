### 224. Basic Calculator

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, **non-negative** integers and empty spaces .

**Example 1:**
```
Input: "1 + 1"
Output: 2
```

**Example 2:**
```
Input: " 2-1 + 2 "
Output: 3
```

**Example 3:**
```
Input: "(1+(4+5+2)-3)+(6+8)"
Output: 23
```

**Note:**
- You may assume that the given expression is always valid.
- Do not use the eval built-in library function.

**Solution**
```Python
from collections import deque

class Solution(object):
    def helper(self, arr):
        stack = []
        num = 0
        sign = "+"

        while len(arr) > 0:
            c = arr.popleft()
            if c.isdigit():
                num = num * 10 + int(c)
            
            if c == "(":
                num = self.helper(arr)
            
            if (not c.isdigit() and c != " ") or len(arr) == 0:
                if sign == "+":
                    stack.append(num)
                elif sign == "-":
                    stack.append(-num)
                
                num = 0
                sign = c
            
            if c == ")":
                break
        
        return sum(stack)

    def calculate(self, s):
        """
        :type s: str
        :rtype: int
        """
        arr = deque(list(s))
        return self.helper(arr)
```