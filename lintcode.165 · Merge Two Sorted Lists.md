# Description
Merge two sorted (ascending) linked lists and return it as a new sorted list. The new sorted list should be made by splicing together the nodes of the two lists and sorted in ascending order.
# 样例 
样例 1: 输入: list1 = null, list2 = 0->3->3->null 输出: 0->3->3->null

样例2: 输入: list1 = 1->3->8->11->15->null, list2 = 2->null 输出: 1->2->3->8->11->15->null

# 思路： 
新建一个linkedlist，tail,next总是指向l1和l2种更小的一个。 point： 如果l1或者l2中一个结束了，那么tail.next就指向唯一存在的一个
```
    def mergeTwoLists(self, l1, l2):
        dummy = ListNode(None)
        tail = dummy
        
        while l1 and l2:
            if l1.val < l2.val:
                tail.next = l1
                l1 = l1.next
            else:
                tail.next = l2
                l2 = l2.next
            tail = tail.next
        if l1:
            tail.next = l1 
        if l2:
            tail.next = l2
                
        return dummy.next
 ```
