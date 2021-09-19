dummy node的作用是为了避免处理删除head或者head.next的情况
双指针，first先找到需要删除的node的后面一个位置
然后second 从头跟着first一起往前走，当first null的时候，second 正好指向target前面一个位置，用second 指针跳过target即可
```
class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(0)
        dummy.next = head
        first = dummy
        second = dummy
        
        for i in range(n+1):
            first = first.next
        while first:
            first = first.next
            second = second.next
        
        second.next = second.next.next
        return dummy.next
```
