### 836. Rectangle Overlap

A rectangle is represented as a list [x1, y1, x2, y2], where (x1, y1) are the coordinates of its bottom-left corner, and (x2, y2) are the coordinates of its top-right corner.

Two rectangles overlap if the area of their intersection is positive.  To be clear, two rectangles that only touch at the corner or edges do not overlap.

Given two (axis-aligned) rectangles, return whether they overlap.

**Example 1:**
```
Input: rec1 = [0,0,2,2], rec2 = [1,1,3,3]
Output: true
```

**Example 2:**
```
Input: rec1 = [0,0,1,1], rec2 = [1,0,2,1]
Output: false
```

**Notes:**
- Both rectangles rec1 and rec2 are lists of 4 integers.
- All coordinates in rectangles will be between -10^9 and 10^9.

**Idea**
```
我们尝试分析在什么情况下，矩形 rec1 和 rec2 没有重叠。

想象一下，如果我们在平面中放置一个固定的矩形 rec2，那么矩形 rec1 必须要出现在 rec2 的「四周」，也就是说，矩形 rec1 需要满足以下四种情况中的至少一种：

矩形 rec1 在矩形 rec2 的左侧；

矩形 rec1 在矩形 rec2 的右侧；

矩形 rec1 在矩形 rec2 的上方；

矩形 rec1 在矩形 rec2 的下方。
```

**Solution**
```Python
class Solution(object):
    def isRectangleOverlap(self, rec1, rec2):
        """
        :type rec1: List[int]
        :type rec2: List[int]
        :rtype: bool
        """
        [x_a_1, y_a_1, x_a_2, y_a_2] = rec1
        [x_b_1, y_b_1, x_b_2, y_b_2] = rec2

        if x_a_2 <= x_b_1 or x_a_1 >= x_b_2 or y_a_1 >= y_b_2 or y_a_2 <= y_b_1:
            return False
        
        return True
```