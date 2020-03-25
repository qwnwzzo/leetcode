### 892. Surface Area of 3D Shapes

On a `N * N` grid, we place some `1 * 1 * 1` cubes.

Each value `v = grid[i][j]` represents a tower of v cubes placed on top of grid cell `(i, j)`.

Return the total surface area of the resulting shapes.

 

**Example 1:**
```
Input: [[2]]
Output: 10
```

**Example 2:**
```
Input: [[1,2],[3,4]]
Output: 34
```

**Example 3:**
```
Input: [[1,0],[0,2]]
Output: 16
```

**Example 4:**
```
Input: [[1,1,1],[1,0,1],[1,1,1]]
Output: 32
```

**Example 5:**
```
Input: [[2,2,2],[2,1,2],[2,2,2]]
Output: 46
```

**Note:**
- 1 <= N <= 50
- 0 <= grid[i][j] <= 50

**Idea**
```
看看有多少个立方体，总表面积是立方体的数量 × 6，但是因为相邻的会互相盖住，统计一下被盖住的面，然后减去被盖住的面就行了
```

**Solution**
```Python
class Solution(object):
    def surfaceArea(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if len(grid) == 0 or len(grid[0]) == 0:
            return 0

        n = len(grid)
        m = len(grid[0])
        block = 0
        cover = 0

        for i in range(n):
            for j in range(m):
                block += grid[i][j]
                cover += grid[i][j] - 1 if grid[i][j] > 0 else 0

                if i > 0:
                    cover += min(grid[i - 1][j], grid[i][j])
                
                if j > 0:
                    cover += min(grid[i][j - 1], grid[i][j])
        
        return block * 6 - cover * 2
```