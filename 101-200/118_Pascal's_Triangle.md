### 118. Pascal's Triangle

**Example:**
```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

**Solution**
```Python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        if numRows == 0:
            return []

        ans = []
        for i in range(numRows):
            row = [None] * (i + 1)
            row[0] = 1
            row[-1] = 1

            for j in range(1, i):
                row[j] = ans[i - 1][j - 1] + ans[i - 1][j]
            
            ans.append(row)
        
        return ans
```