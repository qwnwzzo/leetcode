### 676. Implement Magic Dictionary

Implement a magic directory with `buildDict`, and `search` methods.

For the method `buildDict`, you'll be given a list of non-repetitive words to build a dictionary.

For the method `search`, you'll be given a word, and judge whether if you modify **exactly** one character into **another** character in this word, the modified word is in the dictionary you just built.

**Example 1:**
```
Input: buildDict(["hello", "leetcode"]), Output: Null
Input: search("hello"), Output: False
Input: search("hhllo"), Output: True
Input: search("hell"), Output: False
Input: search("leetcoded"), Output: False
```

**Note:**
- You may assume that all the inputs are consist of lowercase letters a-z.
- For contest purpose, the test data is rather small by now. You could think about highly efficient algorithm after the contest.
- Please remember to RESET your class variables declared in class MagicDictionary, as static/class variables are persisted across multiple test cases. Please see here for more details.

**Solution**
```Python
class TrieNode(object):
    def __init__(self):
        self.children = {}
        self.is_word = False

class Trie(object):
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        
        node.is_word = True
    
    def find(self, word, node, start_index, has_changed_char):
        if start_index == len(word):
            return node.is_word and has_changed_char
        
        not_changed_char_result = False
        changed_char_result = False
        if word[start_index] in node.children:
            # dont need to change this character
            not_changed_char_result = self.find(word, node.children[word[start_index]], start_index + 1, has_changed_char)

        # need to change this character
        # even though this character matches one word in the dict, 
        # you can still change this character to match another word in the dict
        if not has_changed_char:
            for c in node.children:
                if c != word[start_index] and self.find(word, node.children[c], start_index + 1, True):
                    changed_char_result = True
        
        return not_changed_char_result or changed_char_result

    def search(self, word):
        return self.find(word, self.root, 0, False)

class MagicDictionary(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.trie = Trie()

    def buildDict(self, dict):
        """
        Build a dictionary through a list of words
        :type dict: List[str]
        :rtype: None
        """
        for word in dict:
            self.trie.insert(word)

    def search(self, word):
        """
        Returns if there is any word in the trie that equals to the given word after modifying exactly one character
        :type word: str
        :rtype: bool
        """
        return self.trie.search(word)


# Your MagicDictionary object will be instantiated and called as such:
# obj = MagicDictionary()
# obj.buildDict(dict)
# param_2 = obj.search(word)
```