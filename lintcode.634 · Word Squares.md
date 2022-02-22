## Description
Given a set of words without duplicates, find all word squares you can build from them.

A sequence of words forms a valid word square if the kth row and column read the exact same string, where 0 ≤ k < max(numRows, numColumns).

## example, 

the word sequence ["ball","area","lead","lady"] forms a word square because each word reads the same both horizontally and vertically.

b a l l

a r e a

l e a d

l a d y

## 方法
> 建立prefix_to_word的hashmap

> 循环遍历words里的每个word，放到result里

> 如果result的len == result[0]的len，则矩阵完成，这种可能性就放到results里

> 不相等的话，就要再hashmap里找单词;dfs找单词的方法是:

> >1:result的纵坐标是result[0]的横坐标
   
    >> 2:在hashmap里找纵向字母组合所对应的单词
    
    >> 有单词被找到的话，就加入并且进入新的dfs
    
    >> 找不到的话就把这层的单词pop掉，换下一个可能

```
class Solution:
    """
    @param words: a set of words without duplicates
    @return: all word squares
    """
    def wordSquares(self, words):
        # write your code here
        if not words:
            return []

        prefix_to_words = self.get_prefix_to_words(words)
        n = len(words[0])

        results = []
        for word in words:
            self.dfs([word], prefix_to_words, results)
        return results

    def get_prefix_to_words(self, words):
        prefix_to_words = {}
        for word in words:
            for i in range(len(word)):
                prefix = word[: i + 1]
                if prefix not in prefix_to_words:
                    prefix_to_words[prefix] = set()
                prefix_to_words[prefix].add(word)
        return prefix_to_words


    def dfs(self, subset, prefix_to_words, results):
        curt_len = len(subset)
        if curt_len == len(subset[0]):
            results.append(list(subset))
            return 

        prefix = ""
        for i in range(curt_len):
            prefix += subset[i][curt_len]

        for word in prefix_to_words.get(prefix, []):
            subset.append(word)
            self.dfs(subset, prefix_to_words, results)
            subset.pop()
```
