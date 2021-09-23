首先是一个dfs的recursive
在这个过程中把target = root.val的值保存起来，然后在backtracking
```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def pathSum(self, root, targetSum):
        """
        :type root: TreeNode
        :type targetSum: int
        :rtype: List[List[int]]
        """
        if not root:
            return []
        res = []
        self.traverse(root, res, [], targetSum)
        return res
    
    def traverse(self, root, res, path, target):
        if not root:
            return []
        path.append(root.val)
        
        if not root.left and not root.right and target == root.val:
            res.append(path[:])
            
        if root.left:
            self.traverse(root.left, res, path, target - root.val)
            path.pop()
        if root.right:
            self.traverse(root.right, res, path, target - root.val)
            path.pop()
```
