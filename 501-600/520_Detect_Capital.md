### 520. Detect Capital

Given a word, you need to judge whether the usage of capitals in it is right or not.

We define the usage of capitals in a word to be right when one of the following cases holds:
1. All letters in this word are capitals, like "USA".
2. All letters in this word are not capitals, like "leetcode".
3. Only the first letter in this word is capital, like "Google".
4. Otherwise, we define that this word doesn't use capitals in a right way.
 

**Example 1:**
```
Input: "USA"
Output: True
```

**Example 2:**
```
Input: "FlaG"
Output: False
```

**Note:** The input will be a non-empty word consisting of uppercase and lowercase latin letters.

**Solution**
```Python
class Solution(object):
    def detectCapitalUse(self, word):
        """
        :type word: str
        :rtype: bool
        """
        if len(word) == 1:
            return True
            
        if word[0].islower() and word[1].isupper():
            return False
        
        num_upper = 0
        for i in range(1, len(word)):
            if word[i].isupper():
                num_upper += 1
        
        return num_upper == 0 or num_upper == len(word) - 1
```