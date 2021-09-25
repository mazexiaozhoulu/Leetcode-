linklist先找mid，再用中序遍历
```
class Solution(object):
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        if not head:
            return None
        mid = self.findMiddle(head)
        root = TreeNode(mid.val)
        if head == mid:
            return root
        
        root.right = self.sortedListToBST(mid.next)
        root.left = self.sortedListToBST(head)
        return root
    
    def findMiddle(self, head):

        cur = None
        slow = head
        fast = head
        
        while fast and fast.next:
            cur = slow
            slow = slow.next
            fast = fast.next.next
        if cur:
            cur.next = None
            
        return slow
```
