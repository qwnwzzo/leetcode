### 216. Combination Sum III

Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

**Note:**
- All numbers will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**
```
Input: k = 3, n = 7
Output: [[1,2,4]]
```

**Example 2:**
```
Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```

**Solution**
```Python
class Solution(object):
    def combination(self, arr, ans, subset, start_index, n, k):
        if start_index == len(arr):
            if len(subset) == k and sum(subset) == n:
                ans.append(subset[:])
            return

        if len(subset) == k:
            if sum(subset) == n:
                ans.append(subset[:])
            return
        
        for i in range(start_index, len(arr)):
            subset.append(arr[i])
            self.combination(arr, ans, subset, i + 1, n, k)
            subset.pop()

    def combinationSum3(self, k, n):
        """
        :type k: int
        :type n: int
        :rtype: List[List[int]]
        """
        arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
        ans = []
        subset = []
        self.combination(arr, ans, subset, 0, n, k)

        return ans
```