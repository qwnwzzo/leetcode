### 945. Minimum Increment to Make Array Unique

Given an array of integers A, a move consists of choosing any `A[i]`, and incrementing it by `1`.

Return the least number of moves to make every value in A unique.

**Example 1:**
```
Input: [1,2,2]
Output: 1
Explanation:  After 1 move, the array could be [1, 2, 3].
```

**Example 2:**
```
Input: [3,2,1,2,1,7]
Output: 6
Explanation:  After 6 moves, the array could be [3, 4, 1, 2, 5, 7].
It can be shown with 5 or less moves that it is impossible for the array to have all unique values.
```

**Note:**
- 0 <= A.length <= 40000
- 0 <= A[i] < 40000

**Idea**
```
排序后，设定一个suppose值，如果当前值大于suppose，直接更改suppose，如果小于suppose，则move到suppose。
```

**Solution**
```Python
class Solution(object):
    def minIncrementForUnique(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        A.sort()
        suppose = 0
        ans = 0

        for i in range(len(A)):
            if A[i] > suppose:
                suppose = A[i]
            
            ans = ans + suppose - A[i]
            suppose += 1
        
        return ans
```