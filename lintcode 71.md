在69的基础上，按照result里单双位置去reverse
描述
给出一棵二叉树，返回其节点值的锯齿形层次遍历（先从左往右，下一层再从右往左，层与层之间交替进行）

样例
样例 1：

输入：

tree = {1,2,3}
输出：

[[1],[3,2]]
解释：

    1
   / \
  2   3
它将被序列化为 {1,2,3}

```
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

