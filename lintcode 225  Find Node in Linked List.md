```
    def findNode(self, head, val):
        # write your code here
        if not head:
            return None
        while head:
            if val == head.val:
                return head
            else:
                head = head.next
        return head
```
