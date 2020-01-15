### 22. Generate Parentheses

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]

**Idea**
```
只有在我们知道序列仍然保持有效时才添加 '(' or ')'
我们可以通过跟踪到目前为止放置的左括号和右括号的数目来做到这一点
如果我们还剩一个位置，我们可以开始放一个左括号。 如果它不超过左括号的数量，我们可以放一个右括号。
```

**Solution**
```Python
class Solution(object):
    def helper(self, ans, option, n_open, n_close, n_max):
        if len(option) == n_max * 2:
            ans.append(option)
            return
        
        if n_open < n_max:
            self.helper(ans, option + "(", n_open + 1, n_close, n_max)
        
        if n_close < n_open:
            self.helper(ans, option + ")", n_open, n_close + 1, n_max)

    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        if n <= 0:
            return []

        ans = []
        option = ""

        self.helper(ans, option, 0, 0, n)

        return ans
```