### 347. Top K Frequent Elements

Given a non-empty array of integers, return the k most frequent elements.

**Example 1:**
```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

**Example 2:**
```
Input: nums = [1], k = 1
Output: [1]
```

**Note:**
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

**Solution**
```Python
from Queue import PriorityQueue

class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        m = {}
        for num in nums:
            if num not in m:
                m[num] = 0
            m[num] += 1
        
        q = PriorityQueue()
        for num in m:
            q.put([m[num], num])
            if q.qsize() > k:
                q.get()
        
        ans = []
        while q.qsize() > 0:
            ans.append(q.get()[1])

        return ans
```