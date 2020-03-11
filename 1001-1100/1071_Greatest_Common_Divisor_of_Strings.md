### 1071. Greatest Common Divisor of Strings

For strings S and T, we say "T divides S" if and only if S = T + ... + T  (T concatenated with itself 1 or more times)

Return the largest string X such that X divides str1 and X divides str2.

**Example 1:**
```
Input: str1 = "ABCABC", str2 = "ABC"
Output: "ABC"
```

**Example 2:**
```
Input: str1 = "ABABAB", str2 = "ABAB"
Output: "AB"
```

**Example 3:**
```
Input: str1 = "LEET", str2 = "CODE"
Output: ""
```

**Note:**
- 1 <= str1.length <= 1000
- 1 <= str2.length <= 1000
- str1[i] and str2[i] are English uppercase letters.


**Idea**
```
看到标题里面有最大公因子这个词，于是先默写一下 gcd 算法

const gcd = (a, b) => (0 === b ? a : gcd(b, a % b))

总有一种好像顺手就能用上的感觉呢。

其实看起来两个字符串之间能有这种神奇的关系是挺不容易的，我们希望能够找到一个简单的办法识别是否有解。

如果它们有公因子 abc，那么 str1 就是 mm 个 abc 的重复，str2 是 nn 个 abc 的重复，连起来就是 m+nm+n 个 abc，好像 m+nm+n 个 abc 跟 n+mn+m 个 abc 是一样的。

所以如果 str1 + str2 === str2 + str1 就意味着有解。

我们也很容易想到 str1 + str2 !== str2 + str1 也是无解的充要条件。

当确定有解的情况下，最优解是长度为 gcd(str1.length, str2.length) 的字符串。

这个理论最优长度是不是每次都能达到呢？是的。

因为如果能循环以它的约数为长度的字符串，自然也能够循环以它为长度的字符串，所以这个理论长度就是我们要找的最优解。
```

**Solution**
```Python
class Solution(object):
    def gcd(self, a, b):
        if b == 0:
            return a
        
        return self.gcd(b, a % b)

    def gcdOfStrings(self, str1, str2):
        """
        :type str1: str
        :type str2: str
        :rtype: str
        """
        if str1 + str2 != str2 + str1:
            return ""
        
        if len(str1) < len(str2):
            str1, str2 = str2, str1
        
        return str1[: self.gcd(len(str1), len(str2))]
```