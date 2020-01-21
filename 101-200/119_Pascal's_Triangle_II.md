### 119. Pascal's Triangle II

Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.

**Example:**
```
Input: 3
Output: [1,3,3,1]
```

**Solution**
```Python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        if rowIndex < 0:
            return []

        # j行的数据, 应该由j - 1行的数据计算出来.
        # 假设j - 1行为[1,3,3,1], 那么我们前面插入一个0(j行的数据会比j-1行多一个),
        # 然后执行相加[0+1,1+3,3+3,3+1,1] = [1,4,6,4,1], 最后一个1保留即可.
        row = [1]
        for i in range(1, rowIndex + 1):
            row = [0] + row
            for j in range(len(row) - 1):
                row[j] = row[j] + row[j + 1]
        
        return row
```