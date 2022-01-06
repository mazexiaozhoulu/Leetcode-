```
class Solution:
    """
    @param root: the root of the given tree
    @return: the values of the nodes you can see ordered from top to bottom
    """
    def rightSideView(self, root):
        # write your code here

        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        if root is None:
            return res
        
        level = 0
        self.DFS(root, res, level)
        
        ans = []
        for level in range(len(res)):
            ans.append(res[level][-1])
        return ans

    def DFS(self, root, res, level):
        if root is None:
            return
        if level >= len(res):
            res.append([])
        res[level].append(root.val)
        level += 1
        self.DFS(root.left, res, level)
        self.DFS(root.right, res, level)
        return res
```
