### 827. Making A Large Island

In a 2D grid of 0s and 1s, we change at most one 0 to a 1.

After, what is the size of the largest island? (An island is a 4-directionally connected group of 1s).

**Example 1:**
```
Input: [[1, 0], [0, 1]]
Output: 3
Explanation: Change one 0 to 1 and connect two 1s, then we get an island with area = 3.
```

**Example 2:**
```
Input: [[1, 1], [1, 0]]
Output: 4
Explanation: Change the 0 to 1 and make the island bigger, only one island with area = 4.
```

**Example 3:**
```
Input: [[1, 1], [1, 1]]
Output: 4
Explanation: Can't change any 0 to 1, only one island with area = 4.
```

**Notes:**
- 1 <= grid.length = grid[0].length <= 50.
- 0 <= grid[i][j] <= 1.

**Solution**
```Python
class Solution(object):
    def paint(self, grid, color, i, j):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] != 1:
            return 0
        
        grid[i][j] = color
        return 1 + self.paint(grid, color, i - 1, j) +\
        self.paint(grid, color, i, j - 1) +\
        self.paint(grid, color, i + 1, j) +\
        self.paint(grid, color, i, j + 1)
    
    def sum_area(self, grid, index_area, i, j):
        directions = [0, 1, 0, -1, 0]
        seen = set()
        area = 0
        for index in range(4):
            r = i + directions[index]
            c = j + directions[index + 1]
            if r >= 0 and r < len(grid) and c >= 0 and c < len(grid[0]) and grid[r][c] > 1:
                seen.add(grid[r][c])
        
        for index in seen:
            area += index_area[index]
        
        return area
                
    def largestIsland(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if len(grid) == 0 or len(grid[0]) == 0:
            return 0

        n = len(grid)
        m = len(grid[0])
        index_area = {}
        color = 2
        has_ocean = False
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 1:
                    area = self.paint(grid, color, i, j)
                    index_area[color] = area
                    color += 1
                elif grid[i][j] == 0:
                    has_ocean = True
        
        if not has_ocean:
            return n * m
        
        ans = 0
        for i in range(n):
            for j in range(m):
                if grid[i][j] == 0:
                    ans = max(ans, self.sum_area(grid, index_area, i, j) + 1)
        
        return ans
```