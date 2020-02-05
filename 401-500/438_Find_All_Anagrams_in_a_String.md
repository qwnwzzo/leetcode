### 438. Find All Anagrams in a String

Given a string **s** and a non-empty string **p**, find all the start indices of **p's** anagrams in **s**.

Strings consists of lowercase English letters only and the length of both strings **s** and **p** will not be larger than 20,100.

The order of output does not matter.

**Example 1:**
```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**
```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

**Solution**
```Python
class Solution(object):
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        ans = []
        window = {}
        needs = {}
        left = 0
        right = 0
        match = 0

        for c in p:
            if c not in needs:
                needs[c] = 0
            needs[c] += 1

        while right < len(s):
            c = s[right]
            if c in needs:
                if c not in window:
                    window[c] = 0
                window[c] += 1
                if window[c] == needs[c]:
                    match += 1

            right += 1

            while match == len(needs.keys()):
                if right - left == len(p):
                    ans.append(left)

                left_c = s[left]
                if left_c in needs:
                    window[left_c] -= 1
                    if window[left_c] < needs[left_c]:
                        match -= 1
                
                left += 1
        
        return ans
```