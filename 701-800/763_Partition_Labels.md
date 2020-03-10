### 763. Partition Labels

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example 1:**
```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

**Note:**
- S will have length in range [1, 500].
- S will consist of lowercase letters ('a' to 'z') only.

**Solution**
```Python
class Solution(object):
    def partitionLabels(self, S):
        """
        :type S: str
        :rtype: List[int]
        """
        m = {S[i]: i for i in range(len(S))}
        left = 0
        right = 0
        ans = []

        for i in range(len(S)):
            right = max(right, m[S[i]])
            if right == i:
                ans.append(right - left + 1)
                left = right + 1
        
        return ans
```