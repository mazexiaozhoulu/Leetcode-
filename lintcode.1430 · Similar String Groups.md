## Description
Two strings X and Y are similar if we can swap two letters (in different positions) of X, so that it equals Y.

For example, "tars" and "rats" are similar (swapping at positions 0 and 2), and "rats" and "arts" are similar, but "star" is not similar to "tars", "rats", or "arts".

Together, these form two connected groups by similarity: {"tars", "rats", "arts"} and {"star"}. Notice that "tars" and "arts" are in the same group even though they are not similar. Formally, each group is such that a word is in the group if and only if it is similar to at least one other word in the group.

We are given a list A of strings. Every string in A is an anagram of every other string in A. How many groups are there?

## Example
Example 1:

Input: ["tars","rats","arts","star"]
Output: 2
Example 2:

Input: ["omv","ovm"]
Output: 1

```
class Solution:
    def numSimilarGroups(self, strs):
        word_set = set(strs)
        visited = set()
        
        similar_set = 0
        for word in strs:
            if word in visited:
                continue
            similar_set += 1
            self.mark_similar_set(word, word_set, visited)
        
        return similar_set
        
    def mark_similar_set(self, word, word_set, visited):
        from collections import deque
        queue = deque([word])
        visited.add(word)
        while queue:
            word = queue.popleft()
            for neighbor in self.get_neighbor_words(word, word_set):
                if neighbor in visited:
                    continue
                queue.append(neighbor)
                visited.add(neighbor)
        
    def get_neighbor_words(self, word, word_set):
        if len(word) ** 2 < len(word_set):
            return self.get_neighbor_words1(word, word_set)
        return self.get_neighbor_words2(word, word_set)
        
    def get_neighbor_words1(self, word, word_set):
        # O(L^3)
        n = len(word)
        chars = list(word)
        neighbor_words = []
        for i in range(n):
            for j in range(i + 1, n):
                chars[i], chars[j] = chars[j], chars[i]
                anagram = ''.join(chars)
                if anagram in word_set:
                    neighbor_words.append(anagram)
                chars[i], chars[j] = chars[j], chars[i]
        return neighbor_words    

    def get_neighbor_words2(self, word, word_set):
        # O(N*L)
        neighbors = []
        for neighbor in word_set:
            if self.is_similar(word, neighbor):
                neighbors.append(neighbor)
        return neighbors

    def is_similar(self, word1, word2):
        diff = 0
        for c1, c2 in zip(word1, word2):
            if c1 != c2:
                diff += 1
        return diff == 2
```
