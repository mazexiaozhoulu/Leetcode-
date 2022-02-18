```
from lintcode import (
    TreeNode,
)

"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: root of the given tree
    @return: whether it is a mirror of itself 
    """
    def isSymmetric(self, root: TreeNode) -> bool:
        # Write your code here
        if not root:
            return True
        return self.is_Symmetric(root.left, root.right)

    def is_Symmetric(self, left_root, right_root):
        if left_root is None and right_root is None:
            return True
        if left_root is None or right_root is None:
            return False
        if left_root.val != right_root.val:
            return False
        
        left = self.is_Symmetric(left_root.left, right_root.right)
        right = self.is_Symmetric(right_root.right, left_root.left)
        return left and right
```
