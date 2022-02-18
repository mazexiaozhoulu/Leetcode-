## 分治法 o(n)
参数的组合可能性 * 每次处理时间
【问题：二叉树很深，可能会stack over flow的风险；可以用iteration的做法】
```
from lintcode import (
    TreeNode,
)

"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

class Solution:
    """
    @param root: root of the given tree
    @return: whether it is a mirror of itself 
    """
    def isSymmetric(self, root: TreeNode) -> bool:
        # Write your code here
        if not root:
            return True
        return self.is_Symmetric(root.left, root.right)

    def is_Symmetric(self, left_root, right_root):
        if left_root is None and right_root is None:
            return True
        if left_root is None or right_root is None:
            return False
        if left_root.val != right_root.val:
            return False
        
        left = self.is_Symmetric(left_root.left, right_root.right)
        right = self.is_Symmetric(right_root.right, left_root.left)
        return left and right
```
## iteration 的方法

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
    @param root: root of the given tree
    @return: whether it is a mirror of itself 
    """
    def isSymmetric(self, root):
        queue = [root]
        while queue:
            next_queue = []
            for i in range(len(queue)):
                if queue[i] is None:
                    continue
                next_queue.append(queue[i].left)
                next_queue.append(queue[i].right)
            if not self.is_mirror(next_queue):
                return False
            queue = next_queue
        return True
        
    def is_mirror(self, queue):
        left, right = 0, len(queue) - 1
        while left < right:
            if not self.is_same(queue[left], queue[right]):
                return False
            left, right = left + 1, right - 1
        return True
        
    def is_same(self, node1, node2):
        if node1 and node2:
            return node1.val == node2.val
        return node1 is None and node2 is None
```
