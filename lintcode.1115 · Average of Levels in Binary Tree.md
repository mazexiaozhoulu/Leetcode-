```
class Solution:
    """
    @param root: the binary tree of the  root
    @return: return a list of double
    """
    def averageOfLevels(self, root):
        # write your code here
        info = []
        def dfs(node, depth = 0):
            if node:
                if len(info) <= depth:
                    info.append([0, 0])
                info[depth][0] += node.val
                info[depth][1] += 1
                dfs(node.left, depth + 1)
                dfs(node.right, depth + 1)
        dfs(root)

        return [s/float(c) for s, c in info]
```
