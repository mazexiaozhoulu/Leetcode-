DFS + sum

注意 在找到leaf之后再把leaf放到res里，
判断leaf的语句

if not root.left and not root.right:

            
            
```
class Solution:
    """
    @param root: the root of the binary tree
    @return: An integer
    """
    def leafSum(self, root):
        res = []
        if not root:
            return 0

        self.DFS(root, res)
        return sum(res)

    def DFS(self, root, res):
        if not root:
            return 
        if not root.left and not root.right:
            res.append(root.val) 
        self.DFS(root.left, res)
        self.DFS(root.right, res)
```
