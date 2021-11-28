如果是一个只需要层级遍历，然后不用把每一层都分出来的形式的话 [1,2,3]
#BFS
```
    def levelOrder(self, root):
        # write your code here
        if not root:
            return []
        queue = collections.deque([root])
        result = []

        while queue:
            result.append([node.val for node in queue])
            for _ in range(len(queue)):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)
        return result
```
#dfs
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
            
        self.traversal(root, result)
        return result

    def traversal(self, root, result):
        if root is None:
            return

        result.append(root.val)
        self.traversal(root.left, result)
        self.traversal(root.right, result)

        return
```


增加了 result, thislevel两个variable；result用来储存最后包含所有path的list，thislevel代表树的层级。
通过对比当前层级的值和最后的result长度来决定是否增加新的list在result。[[1],[2,3]]

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
