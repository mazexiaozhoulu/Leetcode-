给出一棵二叉树，返回其节点值从底向上的层次序遍历（按从叶节点所在层到根节点所在的层遍历，然后逐层从左往右遍历）
在69的基础上将最后结果的list reverse

```
class Solution:
    """
    @param root: A tree
    @return: buttom-up level order a list of lists of integer
    """
    def levelOrderBottom(self, root):
        # write your code here
        result = []
        if root is None:
            return result
        thislevel = 0
        self.reDFS(root, result, thislevel)
        result.reverse()
        return result

    def reDFS(self, root, result, thislevel):
        if root is None:
            return result
        if thislevel >= len(result):
            result.append([])
        result[thislevel].append(root.val)
        thislevel += 1
        self.reDFS(root.left, result, thislevel)
        self.reDFS(root.right, result, thislevel)
        return 
```
