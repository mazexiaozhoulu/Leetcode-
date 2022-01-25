# Description
Given two words (start and end), and a dictionary, find the shortest transformation sequence from start to end, output the length of the sequence.
Transformation rule such that:

Only one letter can be changed at a time
Each intermediate word must exist in the dictionary. (Start and end words do not need to appear in the dictionary )

# Example 2:

Input:

start ="hit"
end = "cog"
dict =["hot","dot","dog","lot","log"]
Output:

5
Explanation:

"hit"->"hot"->"dot"->"dog"->"cog"
```
class Solution:
    """
    @param: start: a string
    @param: end: a string
    @param: dict: a set of string
    @return: An integer
    """
    def ladderLength(self, start, end, dict):
        # write your code here
        dict.add(end)
        queue = collections.deque([start])
        visited = set([start])

        distance = 0
        while queue:
            distance += 1
            size = len(queue)
            for i in range(size):
                word = queue.popleft()
                if word == end:
                    return distance

                for next_word in self.get_next_words(word, dict):
                    if next_word in visited:
                        continue
                    queue.append(next_word)
                    visited.add(next_word)

    def get_next_words(self, word, dict):
        next_words = []
        for i in range(len(word)):
            left, right = word[:i],word[i + 1:]
            for char in 'abcdefghijklmnopqrstuvwxyz':
                if word[i] == char:
                    continue
                new_word = left + char + right
                if new_word in dict:
                    next_words.append(new_word)
        return next_words
            
```
