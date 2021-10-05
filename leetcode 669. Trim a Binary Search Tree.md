分治法：
def trim 是分。建立一个检测小树的funtion。
一个DFS中，如果节点超过high，那就返回左子树，反之亦然。

如果在范围内，那就keep going
```
class Solution(object):
    def trimBST(self, root, low, high):
        """
        :type root: TreeNode
        :type low: int
        :type high: int
        :rtype: TreeNode
        """
        def trim(node):
            if not node:
                return None
            elif node.val > high:
                return trim(node.left)
            elif node.val < low:
                return trim(node.right)
        
            else:
                node.left = trim(node.left)
                node.right = trim(node.right)
                return node
        
        return trim(root)
```
