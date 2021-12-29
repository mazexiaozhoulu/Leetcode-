```
    def lowestCommonAncestor3(self, root, A, B):

        a, b, node = self.helper(root, A, B)
        if a and b:
            return node 
        else:
            return None 
    
    def helper(self, root, A, B):
        if root is None:
            return False, False, None 
        
        # *****   Divide   *****
        left_a, left_b, left_node = self.helper(root.left, A, B)
        right_a, right_b, right_node = self.helper(root.right, A, B)
        # (Boolean) left_a, left_b, whether A or B exist in the left subtree
        # (Boolean) right_a, right_b, whether A or B exist in the right subtree
        # left_node, right_node,  LCA of A and B in the left and right subtree
        
        # *****   Conquer   *****
        a = left_a or right_a or root == A
        b = left_b or right_b or root == B 
        
        # 根据 a和b 是否同时存在为初级判断条件
        # 然后再在第二层分类讨论，可能会比九章给出的参考答案更加思路清晰一些？ （仅供参考，欢迎提出批评指正）
        if a and b:
            if left_node and right_node:
                # 因为左右子树都有存在的LCA，因此公共的LCA就是root本身
                return a, b, root
            elif left_node:
                return a, b, left_node
            elif right_node:
                return a, b, right_node
            else:
                # 如果左右子树的LCA都不存在，那就只能是root这种情况了
                return a, b, root
        else:
            # 如果a 或 b 中有一个为False，就说明没有LCA，返回None
            return a, b, None
```
