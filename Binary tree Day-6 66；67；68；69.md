66；前序；67:中序；68:后序：
```
class Solution:
    """
    @param root: A Tree
    @return: Preorder in ArrayList which contains node values.
    """
    def preorderTraversal(self, root):
        # write your code here
        self.results = []
        self.traverse(root)
        return self.results

    def traverse(self, root):
        if root is None:
            return
        self.results.append(root.val)
        self.traverse(root.left)
        self.traverse(root.right)
        
     def traversal(self, root):
        if root is None:
            return
        self.traversal(root.left)
        self.result.append(root.val)
        self.traversal(root.right)
        
    def traveral(self, root):
        if root is None:
            return
        self.traveral(root.left)
        self.traveral(root.right)
        self.result.append(root.val)
```

69: 层级遍历，DFS； 
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

70: 层级遍历II 给出一棵二叉树，返回其节点值从底向上的层次序遍历（按从叶节点所在层到根节点所在的层遍历，然后逐层从左往右遍历）
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
71:锯齿形遍历:
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

