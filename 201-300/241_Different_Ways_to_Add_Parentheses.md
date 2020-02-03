### 241. Different Ways to Add Parentheses

Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.

**Example 1:**
```
Input: "2-1-1"
Output: [0, 2]
Explanation: 
((2-1)-1) = 0 
(2-(1-1)) = 2
```

**Example 2:**
```
Input: "2*3-4*5"
Output: [-34, -14, -10, -10, 10]
Explanation: 
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```

**Idea**
```
对于一个形如 x op y（op 为运算符，x 和 y 为数） 的算式而言，它的结果组合取决于 x 和 y 的结果组合数，而 x 和 y 又可以写成形如 x op y 的算式。

因此，该问题的子问题就是 x op y 中的 x 和 y：以运算符分隔的左右两侧算式解。

然后我们来进行分治算法三步走：

1. 分解：按运算符分成左右两部分，分别求解
2. 解决：实现一个递归函数，输入算式，返回算式解
3. 合并：根据运算符合并左右两部分的解，得出最终解
```

**Solution**
```Python
class Solution(object):
    def diffWaysToCompute(self, input):
        """
        :type input: str
        :rtype: List[int]
        """
        if input.isdigit():
            return [int(input)]

        ans = []

        for i, char in enumerate(input):
            if char in ["+", "-", "*"]:
                left_ans = self.diffWaysToCompute(input[: i])
                right_ans = self.diffWaysToCompute(input[i + 1:])

                for l in left_ans:
                    for r in right_ans:
                        if char == "+":
                            ans.append(l + r)
                        elif char == "-":
                            ans.append(l - r)
                        elif char == "*":
                            ans.append(l * r)
                
        return ans
```