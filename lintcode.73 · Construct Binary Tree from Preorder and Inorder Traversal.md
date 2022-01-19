Time complexity : O(N)

space complexity : O(N)

inorder = (left, mid, right)
preorder = (mid, left, right)
postorder = (left, right, mid)
```
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder or not inorder:
            return None
        
        root = TreeNode(preorder.pop(0))
        #检查rootvalue在inorder 里的位置
        inorderindex = inorder.index(root.val)
        root.left = self.buildTree(preorder, inorder[:inorderindex])
        root.right = self.buildTree(preorder, inorder[inorderindex+1:])
        return root
```

106. Construct Binary Tree from Inorder and Postorder Traversal

```
class Solution:
    def buildTree(self, inorder, postorder):
        if not inorder or not postorder:
            return None
        
        root = TreeNode(postorder.pop())
        inorderIndex = inorder.index(root.val) # Line A

        root.right = self.buildTree(inorder[inorderIndex+1:], postorder) # Line B
        root.left = self.buildTree(inorder[:inorderIndex], postorder) # Line C

        return root
```
