```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        this.val = val
        this.left, this.right = None, None
"""


class Solution:
    """
    @param: root: The root of the binary tree.
    @param: A: A TreeNode
    @param: B: A TreeNode
    @return: Return the LCA of the two nodes.
    """
    def lowestCommonAncestor3(self, root, A, B):
        # write your code here
        apath = []
        self.pathtree(root, A, [], apath)
        bpath = []
        self.pathtree(root, B, [], bpath)
        if not apath or not bpath:
            return None
        apath = apath[0]
        bpath = bpath[0]
        aset = set(apath)


        for i in range(-1, -len(bpath) - 1, -1):
            if bpath[i] in aset:
                return bpath[i]

    def pathtree(self, root, target, visit, res):
        if not root or not target:
            return None
        visit.append(root)
        if root == target:
            res.append(visit[:])
        if root.left:
            self.pathtree(root.left, target, visit, res)
            visit.pop()
        if root.right:
            self.pathtree(root.right, target, visit, res)
            visit.pop()
```
