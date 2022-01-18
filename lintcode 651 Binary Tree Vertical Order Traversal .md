lintcode 651

Binary Tree Vertical Order Traversal

在用BFS的时候把每个node的index搞出来， 方法就是左子树-1， 右子树+1， 然后把这个node存到对应的index的group里面。 最后从小到大输出即可

Time Complexity: \mathcal{O}(N \log N) where N is the number of nodes in the tree.
```
class Solution:
    def verticalOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        if not root:
            return None
        result = []
        group = collections.defaultdict(list)
        queue = collections.deque([(root,0)])

        while queue:
            node, index = queue.popleft()
            group[index].append(node.val)
            if node.left:
                queue.append((node.left, index - 1))
            if node.right:
                queue.append((node.right, index + 1))
            
        answer = sorted(group.keys()) # 返回的是group的keys的list[-1, 0, 1, 2]
        print(answer)
        for col in answer:# 遍历[-1, 0, 1, 2]，result就把keys里的value都加到results里
            result.append(group[col])
        return result
```
Time Complexity: \mathcal{O}(N) where N is the number of nodes in the tree.
Following the same analysis in the previous BFS approach, the only difference is that this time we don't need the costy sorting operation (i.e. \mathcal{O}(N \log N)).

Space Complexity: \mathcal{O}(N)O(N) where NN is the number of nodes in the tree. The analysis follows the same logic as in the previous BFS approach.
```
from collections import defaultdict
class Solution:
    def verticalOrder(self, root: TreeNode) -> List[List[int]]:
        if root is None:
            return []

        columnTable = defaultdict(list)
        min_column = max_column = 0
        queue = deque([(root, 0)])

        while queue:
            node, column = queue.popleft()

            if node is not None:
                columnTable[column].append(node.val)
                min_column = min(min_column, column)
                max_column = max(max_column, column)

                queue.append((node.left, column - 1))
                queue.append((node.right, column + 1))

        return [columnTable[x] for x in range(min_column, max_column + 1)]
```
