```
class Solution(object):
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        # print(root)
        p_paths = [] 
        self.pathFinder(root, p, [], p_paths)
        q_paths = [] 
        self.pathFinder(root, q, [], q_paths)
        
        p_path, q_path = p_paths[0], q_paths[0]
        q_set = set(q_path)
        for i in range(-1, -len(p_path) - 1, -1): #如果正着找就会返回第一个就一样的节点 3524&3527 返回3
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
