BST

左子树的所有节点比他小，右子树的所有节点比他大

进行中序遍历，得到的是非降序的序列

有插入操作，一般都把新节点放到叶子结点上
```
def __add_helper(self, root, val):
    if not root:
        return TreeNode(val)
    if val < root.val:
        root.left = self.__add_helper(root.left, val)
    else:
        root.rigth - self.__add_helper(root.right, val)
    return root
```
