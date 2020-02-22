### 650. 2 Keys Keyboard

Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step:

- `Copy All`: You can copy all the characters present on the notepad (partial copy is not allowed).
- `Paste`: You can paste the characters which are copied **last time**.
 

Given a number n. You have to get **exactly** `n` 'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get n 'A'.

**Example 1:**
```
Input: 3
Output: 3
Explanation:
Intitally, we have one character 'A'.
In step 1, we use Copy All operation.
In step 2, we use Paste operation to get 'AA'.
In step 3, we use Paste operation to get 'AAA'.
```

**Note:**
- The n will be in the range [1, 1000].

**Idea**
```
求质数因子

将所有操作分成以 copy 为首的多组，形如 (copy, paste, ..., paste)，再使用 C 代表 copy，P 代表 paste。例如操作 CPPCPPPPCP 可以分为 [CPP][CPPPP][CP] 三组。

假设每组的长度为 g_1, g_2, ...。完成第一组操作后，字符串有 g_1 个 A，完成第二组操作后字符串有 g_1 * g_2 个 A。当完成所有操作时，共有 g_1 * g_2 * ... * g_n 个 'A'。

我们最终想要 N = g_1 * g_2 * ... * g_n 个 A。如果 g_i 是合数，存在 g_i = p * q，那么这组操作可以分解为两组，第一组包含 1 个 C 和 p-1 个 P，第二组包含 1 个 C 和 q-1 个 P。

现在证明这种分割方式使用的操作最少。原本需要 pq 步操作，分解后需要 p+q 步。因为 p+q <= pq，等价于 1 <= (p-1)(q-1)，当 p >= 2 且 q >= 2 时上式永远成立。
```

**Solution**
```Python
class Solution(object):
    def minSteps(self, n):
        """
        :type n: int
        :rtype: int
        """
        ans = 0
        # 最小的质数因子
        d = 2

        while n > 1:
            while n % d == 0:
                # 如果 d 仍然是当前 n 的最小素数因子，继续遍历
                n = n / d
                ans += d
            
            # 如果此时 d 不是当前 n 的最小素数因子了，那么 d++ 继续试探
            # 其实此处应该是把 d 变为比 d 大的下一个素数，但是我们没有必要在构建出一个素数因子的数组，
            # 因为得不偿失(还需要创建一个判断是否为素数的方法)，那会花费更多的时间和空间，
            # 不如让计算机一个个去试就好了
            d += 1
        
        return ans
```