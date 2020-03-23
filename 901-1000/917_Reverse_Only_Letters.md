### 917. Reverse Only Letters

Given a string S, return the "reversed" string where all characters that are not a letter stay in the same place, and all letters reverse their positions.

**Example 1:**
```
Input: "ab-cd"
Output: "dc-ba"
```

**Example 2:**
```
Input: "a-bC-dEf-ghIj"
Output: "j-Ih-gfE-dCba"
```

**Example 3:**
```
Input: "Test1ng-Leet=code-Q!"
Output: "Qedo1ct-eeLg=ntse-T!"
```

**Note:**
- S.length <= 100
- 33 <= S[i].ASCIIcode <= 122 
- S doesn't contain \ or "

**Solution**
```Python
class Solution(object):
    def reverseOnlyLetters(self, S):
        """
        :type S: str
        :rtype: str
        """
        left = 0
        right = len(S) - 1
        arr = list(S)

        while left < right:
            while not arr[left].isalpha():
                if left == right:
                    break
                left += 1
            
            while not arr[right].isalpha():
                if right == left:
                    break
                right -= 1
            
            if left >= right:
                break
            
            arr[left], arr[right] = arr[right], arr[left]
            left += 1
            right -= 1
        
        return "".join(arr)
```