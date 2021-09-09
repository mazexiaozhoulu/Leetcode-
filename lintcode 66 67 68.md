66；前序；67:中序；68:后序：
```
class Solution:
    """
    @param root: A Tree
    @return: Preorder in ArrayList which contains node values.
    """
    def preorderTraversal(self, root):
        # write your code here
        self.results = []
        self.traverse(root)
        return self.results

    def traverse(self, root):
        if root is None:
            return
        self.results.append(root.val)
        self.traverse(root.left)
        self.traverse(root.right)
        
     def traversal(self, root):
        if root is None:
            return
        self.traversal(root.left)
        self.result.append(root.val)
        self.traversal(root.right)
        
    def traveral(self, root):
        if root is None:
            return
        self.traveral(root.left)
        self.traveral(root.right)
        self.result.append(root.val)
```
