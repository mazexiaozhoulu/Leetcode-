# Description
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. 

A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the root of a binary tree, return the maximum path sum of any non-empty path.

# sample

Input: root = [-10,9,20,null,null,15,7]

Output: 42

Explanation: The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.


## 方法1 divide conquer
```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""
import sys
class Solution:
    """
    @param root: The root of binary tree.
    @return: An integer
    """
    
    def maxPathSum(self, root):
        # write your code here
        # singlePath: 从root往下走到任意点的最大路径，这条路径可以不包含任何点
        # maxPath: 从树中任意到任意点的最大路径，这条路径至少包含一个点
        singlePath, maxPath = self.helper(root)
        return maxPath
        
    def helper(self, root):
        if root is None:
            return 0, -sys.maxsize -1
        
        # divdie    
        leftSinglePath, left_maxPath = self.helper(root.left)
        rightSinglePath, right_maxPath = self.helper(root.right)
        
        # conquer 
        singlePath = max(leftSinglePath, rightSinglePath) + root.val 
        singlePath = max(singlePath, 0)
        
        maxPath = max(left_maxPath, right_maxPath)
        maxPath = max(maxPath, leftSinglePath + rightSinglePath + root.val)
        
        return singlePath, maxPath
```

 
# 方法2 Recursion

# time
Time complexity: \mathcal{O}(N), where N is number of nodes, since we visit each node not more than 2 times.

Space complexity: \mathcal{O}(H), where H is a tree height,

```
class Solution:
    def __init__(self):
        self.maxSum = float("-inf")

    def maxPathSum(self, root: TreeNode) -> int:
        def maxGain(node):
            if not node:
                return 0

            # 递归计算左右子节点的最大贡献值
            # 只有在最大贡献值大于 0 时，才会选取对应子节点
            leftGain = max(maxGain(node.left), 0)
            rightGain = max(maxGain(node.right), 0)
            
            # 节点的最大路径和取决于该节点的值与该节点的左右子节点的最大贡献值
            priceNewpath = node.val + leftGain + rightGain
            
            # 更新答案
            self.maxSum = max(self.maxSum, priceNewpath)
        
            # 返回节点的最大贡献值
            return node.val + max(leftGain, rightGain)
   
        maxGain(root)
        return self.maxSum
```
