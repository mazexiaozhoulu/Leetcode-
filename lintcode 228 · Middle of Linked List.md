```

    def middleNode(self, head):
        # write your code here

        if not head:
            return None
        
        slow = head
        fast = head

        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        return slow
```
