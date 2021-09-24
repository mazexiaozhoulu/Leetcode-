BFS+Linkedlist
```
class Solution:
    # @param {TreeNode} root the root of binary tree
    # @return {ListNode[]} a lists of linked list
    def binaryTreeToLists(self, root):
        # Write your code here
        res = []
        if not root:
            return res

        from queue import Queue
        que = Queue()

        que.put(root)

        while not que.empty():
            n = que.qsize()
            dummy = ListNode(-1)
            tmp = dummy
            for i in range(n):
                cur = que.get()
                tmp.next = ListNode(cur.val)
                tmp = tmp.next

                if cur.left:
                    que.put(cur.left)
                if cur.right:
                    que.put(cur.right)
            res.append(dummy.next)
        return res
```
