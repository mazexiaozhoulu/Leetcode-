
pathFinder用回溯法来写。执行时间80-90ms.
pathFinder是找出每个到这个点的path的function
再找到这两个list（p_path, q_path）的相同点
```
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        p_paths = []
        self.pathFinder(root, p, [], p_paths)
        q_paths = []
        self.pathFinder(root, q, [], q_paths)
        
        p_path, q_path = p_paths[0], q_paths[0]
        q_set = set(q_path)
        
        for i in range(-1, -len(p_path) - 1, -1):
            if p_path[i] in q_set:
                return p_path[i]
        
    def pathFinder(self, root, target, visited, res):
        visited.append(root)
        if root == target:
            res.append(visited[:])
        if root.left:
            self.pathFinder(root.left, target, visited, res)
            visited.pop()
        if root.right:
            self.pathFinder(root.right, target, visited, res)
            visited.pop()
    
```
