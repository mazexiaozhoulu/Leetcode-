在用BFS的时候把每个node的index搞出来， 方法就是左子树-1， 右子树+1， 然后把这个node存到对应的index的group里面。 最后从小到大输出即可

```
class Solution:
    """
    @param root: the root of tree
    @return: the vertical order traversal
    """
    def verticalOrder(self, root):
        if not root:
            return []

        results = []
        queue = collections.deque([(root, 0)])
        ##
        group = collections.defaultdict(list)
        ##
        while queue:
            node, index = queue.popleft()
            group[index].append(node.val) 
            if node.left:
                queue.append((node.left, index - 1))
            if node.right:
                queue.append((node.right, index + 1))

        answer = sorted(group.keys())
        for col in answer:
            results.append(group[col])
        return results
```
