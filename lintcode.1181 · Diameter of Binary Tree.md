DFS
```

class Solution:
    """
    @param root: a root of binary tree
    @return: return a integer
    """
    def __init__(self):
        self.max = 0
    def diameterOfBinaryTree(self, root):

        self.helper(root)
        return self.max
 
    def helper(self, root):
        if not root:
            return 0
        left = self.helper(root.left)
        right = self.helper(root.right)
        self.max = max(self.max, left + right)
        return 1 + max(left, right)
```
