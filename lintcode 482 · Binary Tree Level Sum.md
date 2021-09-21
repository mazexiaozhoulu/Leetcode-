先用dfs把树按层遍历一遍。然后在return需要的level层数，求和
要注意
        if level > len(res) or level <= 0:
            return 0
            
```
class Solution:
    """
    @param root: the root of the binary tree
    @param level: the depth of the target level
    @return: An integer
    """
    def levelSum(self, root, level):
        # write your code here
        res = []
        if not root:
            return 0
        levelx = 0

        self.DFS(root, levelx, res)
        if level > len(res) or level <= 0:
            return 0
        return sum(res[level-1])
        
    def DFS(self, root, levelx, res):
        if not root:
            return
        if levelx >= len(res):
            res.append([])
        res[levelx].append(root.val)
        levelx += 1
        self.DFS(root.left, levelx, res)
        self.DFS(root.right, levelx, res)
```
