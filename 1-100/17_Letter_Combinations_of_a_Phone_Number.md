### 17. Letter Combinations of a Phone Number

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

**Example:**
```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**
```
Although the above answer is in lexicographical order, your answer could be in any order you want.
```

**Solution**
```Python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if digits is None or digits == "":
            return []

        m = {
            "2": "abc",
            "3": "def",
            "4": "ghi",
            "5": "jkl",
            "6": "mno",
            "7": "pqrs",
            "8": "tuv",
            "9": "wxyz"
        }

        ans = []

        self.helper(ans, m, "", digits)

        return ans
    
    def helper(self, ans, m, s, digits):
        if len(digits) == 0:
            ans.append(s)
            return
        
        for c in m[digits[0]]:
            self.helper(ans, m, s + c, digits[1:])
```