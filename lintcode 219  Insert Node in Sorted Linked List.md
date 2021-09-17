注意 链表的增加节点。先把新节点和后面连起来，再把前部分和新节点连起来。不然会丢失掉后面的部分。
```
def insertNode(self, head, val):
        # write your code here
        dummy = ListNode(0)
        dummy.next = head
        curr = dummy

        while curr.next and curr.next.val <= val:
            curr = curr.next

        newnode = ListNode(val)
        newnode.next = curr.next
        curr.next = newnode
    
        return dummy.next
```
