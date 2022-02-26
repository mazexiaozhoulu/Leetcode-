Example 1:

Input: 1->2->1->3->3->5->6->3->null
Output: 1->2->3->5->6->null
```
class Solution:
    """
    @param head: The first node of linked list.
    @return: Head node.
    """
    def removeDuplicates(self, head):
        if head is None:
            return None
        mp = dict()
        mp[head.val] = 1 
        curr = head
        while curr.next is not None:
            if curr.next.val not in mp:
                mp[curr.next.val] = 1
                curr = curr.next
            else:
                curr.next = curr.next.next
        return head
```

Input: head = [1,2,3,2]
Output: [1,3]
Explanation: 2 appears twice in the linked list, so all 2's should be deleted. After deleting all 2's, we are left with [1,3].

```
class Solution:

    def deleteDuplicatesUnsorted(self, head: ListNode) -> ListNode:
        dict_t = collections.defaultdict(int)
        curr = head
        while (curr):
            dict_t[curr.val] += 1
            curr = curr.next
        
        dummy = ListNode()
        dummy.next = head
        prev = dummy
        while head:
            if dict_t[head.val] > 1:
                prev.next = head.next
            else:
                prev = prev.next          
            head = head.next
        return dummy.next
```
