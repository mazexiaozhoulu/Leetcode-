利用 dfs+回溯，把每个root->leaf的 path都归出来存到list里，再找出最小长度的path
```
class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        
        paths = []
        self.find_paths(root, [root], paths)
        return min(paths)
    
    def find_paths(self, node, path, paths):
        if not node:
            return
        
        if not node.left and not node.right:
            paths.append(len(path))
            
        path.append(node.left)
        self.find_paths(node.left, path, paths)
        path.pop()
        
        path.append(node.right)
        self.find_paths(node.right, path, paths)
        path.pop()
```
