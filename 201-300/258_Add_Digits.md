### 258. Add Digits

Given a non-negative integer num, repeatedly add all its digits until the result has only one digit.

**Example:**
```
Input: 38
Output: 2 
Explanation: The process is like: 3 + 8 = 11, 1 + 1 = 2. 
             Since 2 has only one digit, return it.
```

**Follow up:**
Could you do it without any loop/recursion in O(1) runtime?

**Solution**
```Python
class Solution(object):
    def helper(self, num):
        ans = 0
        while num > 0:
            digit = num % 10
            num = num / 10
            ans += digit
        
        return ans

    def addDigits(self, num):
        """
        :type num: int
        :rtype: int
        """
        ans = self.helper(num)

        while ans / 10 > 0:
            ans = self.helper(ans)
        
        return ans
```