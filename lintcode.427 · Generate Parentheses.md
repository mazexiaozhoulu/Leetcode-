## Description
Given n, and there are n pairs of parentheses, write a function to generate all combinations of well-formed parentheses, And return the combination result.

Example
Example 1:

Input: 3
Output: ["((()))", "(()())", "(())()", "()(())", "()()()"]

## 方法
>
```
class Solution:
    """
    @param n: n pairs
    @return: All combinations of well-formed parentheses
    """
    def generateParenthesis(self, n):
        # write your code here
        results = []
        results = self.dfs(n,[], 0, results)
        return results

    def dfs(self, n, sequence, left_paren, results):
        if len(sequence) == 2*n:
            results.append(''.join(sequence))
            return 
        if left_paren < n:
            sequence.append("(")
            self.dfs(n, sequence, left_paren + 1, results)
            sequence.pop()
        if left_paren > len(sequence) - left_paren:
            sequence.append(")")
            self.dfs(n, sequence, left_paren, results)
            sequence.pop()
        return results
```
