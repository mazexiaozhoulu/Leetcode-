## 算法解释：
> 重复k次，如果k足够大，那肯定会有旋转到和原始list一样的情况，所以先找到len（listnode），在k%len，知道有效旋转次数

> 然后双指针，找到有限旋转的部分长度 输入：1->2->3->4->5  k = 2 输出：4->5->1->2->3 => 2%5 = 2； 所以有效旋转长度为2，就是1-3

> 然后把这段长度平移到末尾，slow(1)-fast(3)变成slow(3)-fast(5)

> 再rotate，把new_head放到slow.next；slow.next = none（放到尾巴）；fast.next = head(连到头)
```
"""
Definition of ListNode
class ListNode(object):
    def __init__(self, val, next=None):
        self.val = val
        self.next = next
"""

class Solution:
    """
    @param head: the List
    @param k: rotate to the right k places
    @return: the list after rotation
    """
    def rotateRight(self, head, k):
        # write your code here
        if not head or not head.next:
            return head
        
        # calculate the len
        len = 0
        tail = head
        while tail:
            tail = tail.next
            len += 1
            
        k = k % len
        if k == 0:
            return head
        
        slow, fast = head, head
        for _ in range(k):
            fast = fast.next
        
        while fast.next:
            slow = slow.next
            fast = fast.next      
        new_head = slow.next
        slow.next = None
        fast.next = head

        return new_head
 
```
