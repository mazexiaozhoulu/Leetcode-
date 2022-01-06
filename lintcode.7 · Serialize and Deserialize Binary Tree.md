```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""


class Solution:
    """
    @param root: An object of TreeNode, denote the root of the binary tree.
    This method will be invoked first, you should design your own algorithm 
    to serialize a binary tree which denote by a root node to a string which
    can be easily deserialized by your own "deserialize" method later.
    """
    def serialize(self, root):
        # write your code here
        if root is None:
            return ''
        
        res = []
        q = collections.deque([root])
        while q:
            
            node = q.popleft()
            
            res.append(str(node.val) if node else '#')
            
            if node:
                q.append(node.left)
                q.append(node.right)
            
        return ' '.join(res)

    """
    @param data: A string serialized by your serialize method.
    This method will be invoked second, the argument data is what exactly
    you serialized at method "serialize", that means the data is not given by
    system, it's given by your own serialize method. So the format of data is
    designed by yourself, and deserialize it here as you serialize it in 
    "serialize" method.
    """
    def deserialize(self, data):
        # write your code here
        if not data:
            return None
        
        data = data.split(' ')
        root = TreeNode(data[0])
        node = root
        
        q = collections.deque([node])
        
        i = 1
        while q and i < len(data):
            node = q.popleft()
            
            if i < len(data):
                if data[i] != '#':
                    node.left = TreeNode(data[i])
                    q.append(node.left)
                else:
                    node.left = None
                i += 1
            
            if i < len(data):
                if data[i] != '#':
                    node.right = TreeNode(data[i])
                    q.append(node.right)
                else:
                    node.right = None
                i += 1
        return root
```
