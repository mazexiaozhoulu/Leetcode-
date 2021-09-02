二叉树和链表的结合

BST符合inorder 左中右的二叉树遍历 输出list后
再把list做成双向链表，先正向连上一遍，再反向连上一遍。最后再首尾相连。
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
    @param root: root of a tree
    @return: head node of a doubly linked list
    """
    def treeToDoublyList(self, root):
        self.result = []
        if not root:
            return None

        self.inOrderTraverse(root)

        l = len(self.result)
        for i in range(l-1):
            self.result[i].right = self.result[i+1]
            self.result[l-1-i].left = self.result[l-2-i]

        self.result[l-1].right = self.result[0]
        self.result[0].left = self.result[l-1]

        return self.result[0]

    def inOrderTraverse(self, root):
        if not root:
            return None

        self.inOrderTraverse(root.left)
        self.result.append(root)
        self.inOrderTraverse(root.right)
   ```
