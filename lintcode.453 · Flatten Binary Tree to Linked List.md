利用stack先序遍历 （根->右->左，入栈）

连接操作只需要把每个 pop 出来的node：

左子树赋为None

右子树赋为当前栈顶（如果栈顶不空），否则赋为None
```
class Solution:
    """
    @param root: a TreeNode, the root of the binary tree
    @return: nothing
    """
    def flatten(self, root):

        if not root:
            return
        
        stack = collections.deque([root])
        
        while stack:
            node = stack.pop()
            
            if node.right:
                stack.append(node.right)
            if node.left:
                stack.append(node.left)
            
            node.left = None
            
            if stack:
                node.right = stack[-1]
            else:
                node.right = None
```
