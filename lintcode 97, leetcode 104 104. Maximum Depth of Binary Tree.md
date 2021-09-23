DFS前序按层次排好后，再计算res的长度。
时间复杂度：o（n）+ python内置函数len(list)获取其长度的时间O(1) = o(n), 需要额外的空间保存
```
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        res = []
        if not root:
            return 0
        level = 0
        self.dfs(root, res, level)
        return len(res)
    
    def dfs(self, root, res, level):
        if not root:
            return 
        if level >= len(res):
            res.append([])
        res[level].append(root)
        level += 1
        
        self.dfs(root.left, res, level)
        self.dfs(root.right, res, level)
        
        return
```
DFS前序， 再设置一个一直用来保存最大值的height变量。
时间复杂度：o（n），但height的额外空间比上面解法少
```
    def maxDepth(self, root):
        self.max = 0
        self.dfs(root, 1)
        return self.max

    def dfs(self, root, height):
        if not root:
            return None
        self.max = max(self.max, height)
        self.dfs(root.left, height+1)
        self.dfs(root.right, height+1)
```
