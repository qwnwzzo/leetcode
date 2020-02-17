### 593. Valid Square

Given the coordinates of four points in 2D space, return whether the four points could construct a square.

The coordinate (x,y) of a point is represented by an integer array with two integers.

**Example:**
```
Input: p1 = [0,0], p2 = [1,1], p3 = [1,0], p4 = [0,1]
Output: True
```

**Note:**
- All the input integers are in the range [-10000, 10000].
- A valid square has four equal sides with positive length and four equal angles (90-degree angles).
- Input points have no order.

**Solution**
```Python
class Solution(object):
    def get_distance(self, p1, p2):
        return (p1[0] - p2[0]) ** 2 + (p1[1] - p2[1]) ** 2

    def validSquare(self, p1, p2, p3, p4):
        """
        :type p1: List[int]
        :type p2: List[int]
        :type p3: List[int]
        :type p4: List[int]
        :rtype: bool
        """
        arr = [p1, p2, p3, p4]
        arr.sort()
        p1 = arr[0]
        p2 = arr[1]
        p3 = arr[2]
        p4 = arr[3]

        p12 = self.get_distance(p1, p2)
        p13 = self.get_distance(p1, p3)
        p24 = self.get_distance(p2, p4)
        p34 = self.get_distance(p3, p4)

        p14 = self.get_distance(p1, p4)
        p23 = self.get_distance(p2, p3)

        return p12 > 0 and p12 == p13 and p24 == p34 and p12 == p24 and p14 == p23
```