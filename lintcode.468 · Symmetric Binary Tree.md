```
class Solution:
    """
    @param root: the root of binary tree.
    @return: true if it is a mirror of itself, or false.
    """
    def isSymmetric(self, root):
        # write your code here
        if not root:
            return True
        return self.helper( root.left, root.right )
        
    def helper(self, left, right):
        if not left and not right:
            return True
        elif not (left and right):
            return False
        return left.val == right.val and \
               self.helper(left.left, right.right) and \
               self.helper(left.right, right.left)
```
