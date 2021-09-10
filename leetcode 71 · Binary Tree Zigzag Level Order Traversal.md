```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def zigzagLevelOrder(self, root):
        # write your code here
        result = []
        if root is None:
            return result
        level = 0

        self.traversal(root, result, level)

        answer = []
        for i in range(len(result)):
            if i % 2 == 1:
                result[i].reverse()
            answer.append(result[i])
        return answer

    def traversal(self, root, result, level):
        if root is None:
            return
        if level >= len(result):
            result.append([])
        result[level].append(root.val)
        level += 1
        self.traversal(root.left, result, level)
        self.traversal(root.right, result, level)
        return result
```
