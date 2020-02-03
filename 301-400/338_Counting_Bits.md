### 338. Counting Bits

Given a non negative integer number **num**. For every numbers i in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.

**Example 1:**
```
Input: 2
Output: [0,1,1]
```

**Example 2:**
```
Input: 5
Output: [0,1,1,2,1,2]
```

**Idea**
```
观察x 和 x' = x / 2 的关系：
x = (1001011101) 2 = (605) 10
x′= (100101110) 2 = (302) 10
​ 
​可以发现 x' 与 x 只有一位不同，这是因为x'可以看做 x 移除最低有效位的结果。

这样，我们就有了下面的状态转移函数：

P(x)=P(x/2)+(xmod2)
```

**Solution**
```Python
class Solution(object):
    def countBits(self, num):
        """
        :type num: int
        :rtype: List[int]
        """
        ans = [0] * (num + 1)
        for i in range(1, num + 1):
            # x / 2 is x >> 1 and x % 2 is x & 1
            ans[i] = ans[i >> 1] + (i & 1)
        
        return ans
```