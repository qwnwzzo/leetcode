### 692. Top K Frequent Words


Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

**Example 1:**
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
    Note that "i" comes before "love" due to a lower alphabetical order.
```

**Example 2:**
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```

**Note:**
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Input words contain only lowercase letters.

**Follow up:**
Try to solve it in O(n log k) time and O(n) extra space.

**Solution**
```Python
from Queue import PriorityQueue

class Solution(object):
    def topKFrequent(self, words, k):
        """
        :type words: List[str]
        :type k: int
        :rtype: List[str]
        """
        if len(words) == 0:
            return []
        
        freq_m = {}
        for word in words:
            if word not in freq_m:
                freq_m[word] = 0
            freq_m[word] += 1

        q = PriorityQueue()
        for word in freq_m:
            q.put([-freq_m[word], word])
        
        ans = []
        for i in range(k):
            if q.qsize() == 0:
                break
            ans.append(q.get()[1])
        
        return ans
```