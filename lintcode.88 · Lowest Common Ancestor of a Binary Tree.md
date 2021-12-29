# 可以先用hashset()
# 如果不让用hashset 就可以倒着找到交集
# 两个节点不一定都在树里（root, q,p 但不保证root里一定有p和q）
[578 · Lowest Common Ancestor III](https://github.com/mazexiaozhoulu/Leetcode-/blob/afb425f45f4906889f1cdbe0a444271e29b7ad5e/lintcode.578%20%C2%B7%20Lowest%20Common%20Ancestor%20III.md)
# 确保两个数值都在树里
如果 A 和 B 都在，return  LCA
如果只有 A 在，return A
如果只有 B 在，return B
如果 A, B 都不在，return None
```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""


class Solution:
    """
    @param: root: The root of the binary search tree.
    @param: A: A TreeNode in a Binary.
    @param: B: A TreeNode in a Binary.
    @return: Return the least common ancestor(LCA) of the two nodes.
    """
    def lowestCommonAncestor(self, root, A, B):
        if root is None:
            return None
        if root == A or root == B:
            return root
        left = self.lowestCommonAncestor(root.left, A, B)
        right = self.lowestCommonAncestor(root.right, A, B)
        if left and right:
            return root
        if left:
            return left
        if right:
            return right
        return None
```
