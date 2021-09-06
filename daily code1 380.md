
注意链表的特点,只需要知道node就可以知道后面的其他node了，不需要再逐个思考。再利用set把headA里node统计一下。但凡headB里面找到了相同的值，就可以确认是当前node
```
class Solution:
    """
    @param headA: the first list
    @param headB: the second list
    @return: a ListNode
    """
    def getIntersectionNode(self, headA, headB):
        mp = set()
        while headA:
            mp.add(headA)
            headA = headA.next

        while headB:
            if headB in mp:
                return headB          
            headB = headB.next
        return headB
```
