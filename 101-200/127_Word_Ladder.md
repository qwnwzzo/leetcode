### 127. Word Ladder

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

**Note:**
```
Return 0 if there is no such transformation sequence.
All words have the same length.
All words contain only lowercase alphabetic characters.
You may assume no duplicates in the word list.
You may assume beginWord and endWord are non-empty and are not the same.
```

**Example 1:**
```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```

**Example 2:**
```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

**Solution**
```Python
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        l = len(beginWord)
        m = {}
        for s in wordList:
            for i in range(l):
                convert_s = s[:i] + "*" + s[i + 1:]
                if convert_s not in m:
                    m[convert_s] = []
                m[convert_s].append(s)

        queue = [(beginWord, 1)]
        visited = set([beginWord])

        while len(queue) > 0:
            word, level = queue.pop(0)

            for i in range(l):
                general_word = word[:i] + "*" + word[i + 1:]
                if general_word in m:
                    for w in m[general_word]:
                        if w == endWord:
                            return level + 1
                        if w not in visited:
                            queue.append((w, level + 1))
                            visited.add(w)
                    
                    m[general_word] = []

        return 0
```