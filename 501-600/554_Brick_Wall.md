### 554. Brick Wall

There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. The bricks have the same height but different width. You want to draw a vertical line from the **top** to the **bottom** and cross the **least** bricks.

The brick wall is represented by a list of rows. Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

**You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.**

 

**Example:**
```
Input: [[1,2,2,1],
        [3,1,2],
        [1,3,2],
        [2,4],
        [3,1,2],
        [1,3,1,1]]

Output: 2
```

**Note:**
- The width sum of bricks in different rows are the same and won't exceed INT_MAX.
- The number of bricks in each row is in range [1,10,000]. The height of wall is in range [1,10,000]. Total number of bricks of the wall won't exceed 20,000.

**Idea**
```
在这种方法中，我们使用哈希表 mapmap 来保存记录 (sum, count)(sum,count) ，这里 sumsum 是当前行累积的砖头宽度， countcount 是 sumsum 对应的穿过砖头数目。

我们来看一看过程是如何进行的。我们逐一遍历墙的每一行，对于每一块砖，我们将当前行遇到的所有砖头的宽度加起来得到 sumsum，如果这个 sumsum 在 mapmap 中没有出线过，我们创建一个初始 countcount 值为 1 的相应条目。如果 sumsum 已经存在于哈希表中，我们只需要给对应的 countcount 加一。

这个过程的原理基于以下观察：我们在遍历同一行的时候不会遇到相同的 sumsum 两次。所以如果 sumsum 在遍历过程中遇到相同的值，说明一定存在别的行 sumsum 也是那些行的衔接处。所以对应的 countcount 值需要加一。

对于每一行，我们只考虑到倒数第二块砖头的 sumsum 值，因为最后一块砖头的右边界不是一个衔接处。

最后，我们从哈希表中找到最大的 countcount 值，用这个值求出垂直竖线穿过的最少砖块数。
```

**Solution**
```Python
class Solution(object):
    def leastBricks(self, wall):
        """
        :type wall: List[List[int]]
        :rtype: int
        """
        n = len(wall)
        if n == 0:
            return 0

        m = {}
        for i in range(n):
            width = 0
            for j in range(len(wall[i]) - 1):
                width += wall[i][j]
                if width not in m:
                    m[width] = 0
                m[width] += 1

        ans = n
        for width in m:
            ans = min(ans, n - m[width])
        
        return ans
```