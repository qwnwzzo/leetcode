### 880. Decoded String at Index

An encoded string `S` is given.  To find and write the decoded string to a tape, the encoded string is read **one character at a time** and the following steps are taken:

If the character read is a letter, that letter is written onto the tape.
If the character read is a digit (say `d`), the entire current tape is repeatedly written `d-1` more times in total.
Now for some encoded string `S`, and an index `K`, find and return the `K-th` letter (1 indexed) in the decoded string.

**Example 1:**
```
Input: S = "leet2code3", K = 10
Output: "o"
Explanation: 
The decoded string is "leetleetcodeleetleetcodeleetleetcode".
The 10th letter in the string is "o".
```

**Example 2:**
```
Input: S = "ha22", K = 5
Output: "h"
Explanation: 
The decoded string is "hahahaha".  The 5th letter is "h".
```

**Example 3:**
```
Input: S = "a2345678999999999999999", K = 1
Output: "a"
Explanation: 
The decoded string is "a" repeated 8301530446056247680 times.  The 1st letter is "a".
```

**Note:**
- 2 <= S.length <= 100
- S will only contain lowercase letters and digits 2 through 9.
- S starts with a letter.
- 1 <= K <= 10^9
- The decoded string is guaranteed to have less than 2^63 letters.

**Idea**
```
如果我们有一个像 appleappleappleappleappleapple 这样的解码字符串和一个像 K=24 这样的索引，那么如果 K=4，答案是相同的。

一般来说，当解码的字符串等于某个长度为 size 的单词重复某些次数（例如 apple 与 size=5 组合重复6次）时，索引 K 的答案与索引 K % size 的答案相同。

我们可以通过逆向工作，跟踪解码字符串的大小来使用这种洞察力。每当解码的字符串等于某些单词 word 重复 d 次时，我们就可以将 k 减少到 K % (Word.Length)。
```

**Solution**
```Python
class Solution(object):
    def decodeAtIndex(self, S, K):
        """
        :type S: str
        :type K: int
        :rtype: str
        """
        size = 0
        for c in S:
            if c.isdigit():
                n = int(c)
                size *= n
            else:
                size += 1
        
        if K > size:
            return ""

        for i in range(len(S) - 1, -1, -1):
            K %= size

            if K == 0 and S[i].isalpha():
                return S[i]
            
            if S[i].isdigit():
                size /= int(S[i])
            else:
                size -= 1
        
        return ""
```