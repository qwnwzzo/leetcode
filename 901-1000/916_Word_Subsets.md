### 916. Word Subsets

We are given two arrays A and B of words.  Each word is a string of lowercase letters.

Now, say that word b is a subset of word a if every letter in b occurs in a, including **multiplicity**.  For example, "wrr" is a subset of "warrior", but is not a subset of "world".

Now say a word a from A is universal if for every b in B, b is a subset of a. 

Return a list of all universal words in A.  You can return the words in any order.

**Example 1:**
```
Input: A = ["amazon","apple","facebook","google","leetcode"], B = ["e","o"]
Output: ["facebook","google","leetcode"]
```

**Example 2:**
```
Input: A = ["amazon","apple","facebook","google","leetcode"], B = ["l","e"]
Output: ["apple","google","leetcode"]
```

**Example 3:**
```
Input: A = ["amazon","apple","facebook","google","leetcode"], B = ["e","oo"]
Output: ["facebook","google"]
```

**Example 4:**
```
Input: A = ["amazon","apple","facebook","google","leetcode"], B = ["lo","eo"]
Output: ["google","leetcode"]
```

**Example 5:**
```
Input: A = ["amazon","apple","facebook","google","leetcode"], B = ["ec","oc","ceo"]
Output: ["facebook","leetcode"]
``` 

**Note:**
- 1 <= A.length, B.length <= 10000
- 1 <= A[i].length, B[i].length <= 10
- A[i] and B[i] consist only of lowercase letters.
- All words in A[i] are unique: there isn't i != j with A[i] == A[j].

**Idea**
```
当我们检验 "warrior" 是否是 B = ["wrr", "wa", "or"] 的超集时，我们可以按照字母出现的最多次数将 B 中所有单词合并成一个单词 "arrow"，然后判断一次即可。
```

**Solution**
```Python
class Solution(object):
    def count_word(self, word):
        window = {}
        for c in word:
            if c not in window:
                window[c] = 0
            window[c] += 1
        
        return window

    def wordSubsets(self, A, B):
        """
        :type A: List[str]
        :type B: List[str]
        :rtype: List[str]
        """
        needs = {}
        for word in B:
            count_m = self.count_word(word)
            for c in count_m:
                if c not in needs:
                    needs[c] = count_m[c]
                else:
                    needs[c] = max(needs[c], count_m[c])
        
        ans = []
        for word in A:
            count_m = self.count_word(word)
            find_word = True
            for c in needs:
                if c not in count_m or needs[c] > count_m[c]:
                    find_word = False
                    break
            
            if find_word:
                ans.append(word)
        
        return ans
```