### 567. Permutation in String

Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

**Example 1:**
```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

**Example 2:**
```
Input:s1= "ab" s2 = "eidboaoo"
Output: False
```

**Note:**
- The input strings only contain lower case letters.
- The length of both given strings is in range [1, 10,000].

**Solution**
```Python
class Solution(object):
    def checkInclusion(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        needs = {}
        windows = {}
        match = 0
        left = 0
        right = 0

        for c in s1:
            if c not in needs:
                needs[c] = 0
                windows[c] = 0
            needs[c] += 1
        
        while right < len(s2):
            c = s2[right]
            if c in needs:
                windows[c] += 1
                if windows[c] == needs[c]:
                    match += 1
            
            right += 1

            while match == len(needs.keys()):
                if right - left == len(s1):
                    return True
                
                left_c = s2[left]
                if left_c in needs:
                    windows[left_c] -= 1
                    if windows[left_c] < needs[left_c]:
                        match -= 1
                
                left += 1
        
        return False
```