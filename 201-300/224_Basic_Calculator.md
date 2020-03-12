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
class Solution(object):
    def calculate(self, s):
        """
        :type s: str
        :rtype: int
        """
        stack = []

        for c in s:
            if c != " ":
                if c.isdigit():
                    if len(stack) == 0 or type(stack[-1]) != int:
                        stack.append(int(c))
                    else:
                        stack[-1] = stack[-1] * 10 + int(c)
                elif c == "+" or c == "-" or c == "(":
                    stack.append(c)
                elif c == ")":
                    temp = 0
                    cur = stack.pop()
                    op = stack.pop()

                    while op != '(':
                        if op == "+":
                            temp += cur
                        else:
                            temp += cur * -1
                        
                        cur = stack.pop()
                        op = stack.pop()
                    
                    temp += cur
                    stack.append(temp)
        
        ans = 0
        while len(stack) > 1:
            cur = stack.pop()
            op = stack.pop()
            if op == "+":
                ans += cur
            else:
                ans += cur * -1
        
        ans += stack.pop()

        return ans
```