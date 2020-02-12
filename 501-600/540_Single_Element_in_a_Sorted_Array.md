### 540. Single Element in a Sorted Array

You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once. Find this single element that appears only once.

**Example 1:**
```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Example 2:**
```
Input: [3,3,7,7,10,11,11]
Output: 10
```

**Note:** Your solution should run in O(log n) time and O(1) space.

**Idea**
```
- 事实证明我们只需要对偶数索引进行二分搜索。这种方法与方法二都是不错的方法，但是该方法比方法二更加优雅。
- 在该算法中，我们对所有偶数索引进行搜索，直到遇到第一个其后元素不相同的索引。
- 我们可以使用二分搜索替代线性搜索。
- 在单个元素的后面，则成对的元素变为奇数索引后跟他们的同一元素。说明我们在检索单个元素后面的偶数索引时，其后都没有它的同一元素。因此，我们可以通过偶数索引确定单个元素在左侧还是右侧。

算法：
- 奇数长度的数组首尾元素索引都为偶数，因此我们可以将 lo 和 hi 设置为数组首尾。
- 我们需要确保 mid 是偶数，如果为奇数，则将其减 1。
- 然后，我们检查 mid 的元素是否与其后面的索引相同。
- 如果相同，则我们知道 mid 不是单个元素。且单个元素在 mid 之后。则我们将 lo 设置为 mid + 2。
- 如果不是，则我们知道单个元素位于 mid，或者在 mid 之前。我们将 hi 设置为 mid。
- 一旦 lo == hi，则当前搜索空间为 1 个元素，那么该元素为单个元素，我们将返回它。
```

**Solution**
```Python
class Solution(object):
    def singleNonDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        start = 0
        end = len(nums) - 1

        while start + 1 < end:
            mid = start + (end - start) / 2
            if mid % 2 == 1:
                mid -= 1
            
            if nums[mid] == nums[mid + 1]:
                start = mid + 2
            else:
                end = mid
        
        if start == end:
            return nums[start]
        elif start == 0:
            return nums[0]
        else:
            if nums[start - 1] == nums[start]:
                return nums[end]
            return nums[end]
```