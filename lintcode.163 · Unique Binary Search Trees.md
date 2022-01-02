```
class Solution:
    # @paramn n: An integer
    # @return: An integer
    def numTrees(self, n):
        ans = {0: 1,
               1: 1,
               2: 2}
        return self.helper(n, ans)
    
    def helper(self, n, ans):
        if n in ans:
            return ans[n]
        else:
            # for each root node, there are 
            # (numTrees(left_subtree)) * (numTrees(right_subtree)) unique BST's
            res = 0
            for i in range(n):
                res += self.helper(i, ans) * self.helper(n - i - 1, ans)
            ans[n] = res
            return res
```
