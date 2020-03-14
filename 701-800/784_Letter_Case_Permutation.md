### 784. Letter Case Permutation

Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.  Return a list of all possible strings we could create.

**Examples:**
```
Input: S = "a1b2"
Output: ["a1b2", "a1B2", "A1b2", "A1B2"]

Input: S = "3z4"
Output: ["3z4", "3Z4"]

Input: S = "12345"
Output: ["12345"]
```

**Note:**
- S will be a string with length between 1 and 12.
- S will consist only of letters or digits.

**Solution**
```Python
class Solution(object):
    def helper(self, arr, ans, index):
        if index == len(arr):
            ans.append("".join(arr))
            return
        
        if arr[index].isalpha():
            arr[index] = arr[index].lower()
            self.helper(arr, ans, index + 1)
            arr[index] = arr[index].upper()
            self.helper(arr, ans, index + 1)
        else:
            self.helper(arr, ans, index + 1)

    def letterCasePermutation(self, S):
        """
        :type S: str
        :rtype: List[str]
        """
        arr = list(S)
        ans = []

        self.helper(arr, ans, 0)

        return ans
```