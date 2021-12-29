```
class Solution:
    """
    @param root: The root of binary tree.
    @return: True if the binary tree is BST, or false
    """
    def __init__(self):
        self.res = []

    def isValidBST(self, root):
        # write your code here
        self.inorder(root)
        for i in range(1, len(self.res)):
            if self.res[i] <= self.res[i-1]:
                return False
        return True

    def inorder(self, root):
        if not root:
            return None
        self.inorder(root.left)
        self.res.append(root.val)
        self.inorder(root.right)
```
