### 49. Group Anagrams

Given an array of strings, group anagrams together.

**Example:**
```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**
- All inputs will be in lowercase.
- The order of your output does not matter.

**Solution**
```Python
class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        m = {}
        for s in strs:
            key = tuple(sorted(s))
            m[key] = m.get(key, []) + [s]
        
        return m.values()
```