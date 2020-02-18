### 621. Task Scheduler

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks. Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two **same tasks**, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the **least** number of intervals the CPU will take to finish all the given tasks.

 

**Example:**
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```

**Note:**
- The number of tasks is in the range [1, 10000].
- The integer n is in the range [0, 100].

**Idea**
```
- 桶思想，每个桶固定大小为 n+1（除最后一个桶之外），这样可以确保相同的任务可以分在不同的桶中
- 当然，每个任务在桶中的次序是固定的，比如说 A 在桶底，那么在每个桶中 A 都在底部，这样可以确保相同任务的间隔时间都不小于 n
- 桶的数量由 拥有最多任务数的那个任务决定，只要他保证了冷却时间，其他的一定可以
- 结果就是 (n+1) * (count - 1) + 最后一个桶的大小，count 为桶的数量，因为最后一个桶无需固定大小
- count 很好求，那最后一个桶大小如何求呢，很明显就是 拥有最多数任务的个数，比如AAABBBCCCDDEE，那最后一个桶的大小就是 3，因为 A B C 都是拥有 3 个任务数
- 如果冷却时间过短，任务数过多，也就是说桶不够用了，比如说 AAABBBCCCDDEE 且 n = 2 这种情况，此时 桶的大小为 3，桶的数量为 3。第一个桶 ABC ，第二个 ABC，第三个 ABC，此时的 D 和 E 我们可以理解为按照一定次序放在桶之上就行 ，也就是不用放到桶中，这样不会影响桶内元素
- 由于 D 和 E 的出现次数是一定小于桶的数量的，所以最多每个桶上放一个相同任务，这样 D 和 E 按次序排布是一定符合要求的
- 此时的答案就是 任务总数 了，因为所有的桶都满了，并且多出来的也是任务，没有待命时间
- 故答案就是 两个时间 的最大值

**Solution**
```Python
class Solution(object):
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        m = {}
        max_freq = 0
        for task in tasks:
            if task not in m:
                m[task] = 0
            m[task] += 1
            max_freq = max(m[task], max_freq)
        
        last = 0
        for task in m:
            if m[task] == max_freq:
                last += 1
        
        num1 = (n + 1) * (max_freq - 1) + last
        num2 = len(tasks)

        return max(num1, num2)
```