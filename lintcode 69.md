增加了 result, thislevel两个variable；result用来储存最后包含所有path的list，thislevel代表树的层级。
通过对比当前层级的值和最后的result长度来决定是否增加新的list在result。

```
class Solution:
    """
    @param root: A Tree
    @return: Level order a list of lists of integer
    """
    def levelOrder(self, root):
        # write your code here
        result = []
        if root is None:
            return result
        thislevel = 0
        self.traversal(root, result, thislevel)
        return result

    def traversal(self, root, result, thislevel):
        if root is None:
            return
        if thislevel >= len(result):
            result.append([])
        result[thislevel].append(root.val)
        thislevel += 1
        self.traversal(root.left, result, thislevel)
        self.traversal(root.right, result, thislevel)

        return
```
