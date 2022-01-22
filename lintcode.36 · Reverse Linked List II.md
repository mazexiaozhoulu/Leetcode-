        #先把m—pre和n—next标记，以防丢失，再调换m和n
        #找到m_pre,标记m_pre，标记m_pre和m的关系
        #找到n_next,标记n_next，标记n_next和n的关系，独立出来m-n的部分
        #再把m-n的部分和其他连起来


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
    @param head: ListNode head is the head of the linked list 
    @param m: An integer
    @param n: An integer
    @return: The head of the reversed ListNode
    """
    def reverseBetween(self, head, m, n):
        #先把m—pre和n—next标记，以防丢失，再调换m和n
        dummy = ListNode(-1)
        dummy.next = head
        #找到m_pre,标记m_pre，标记m_pre和m的关系
        mth_pre = self.findkth(dummy, m-1)
        mth = mth_pre.next
        #找到n_next,标记n_next，标记n_next和n的关系，独立出来m-n的部分
        nth = self.findkth(dummy, n)
        nth_next = nth.next
        nth.next = None
        #再把m-n的部分和其他连起来
        self.reverse(mth)
        mth_pre.next = nth
        mth.next = nth_next
        return dummy.next

    def reverse(self, head):
        pre = None
        while head != None:
         #1:先把head move到下一个位置上，就是head.next
         #如果先把2挪到最后一个位置上，就会丢失2->3的link,找不到下一个node是谁了
            next = head.next
        #2:再把head挪到整个linkedlist最后，head.next = pre
        #head 是2，pre是none
        #就是2->None
            head.next = pre
        #3:reverse之后了，现在的head位置上就变成了pre
            pre = head
        #4:以上完成了一个move node，进行下一个head的move，就是3，这里的3就是一开始iteration保存到next的3
        #所以head = next，就是3
            head = next
        #循环停止条件就是没有node了，head = None
        return pre
# （2->3->4）                 round1                 round2                 round3                      round4 
#start>(head    pre)         (2     none)           (3     2)              (4     3)                   (head为none，停止)
#step1>(next = head.next)    (2.next是3(叫做next))   (3.next = 4(叫做next))  (4.next = none(叫做next))
#step2>(head.next = pre)     (pre(none)变成2.next)   (pre(2)变成3.next)      (pre(3)变成4.next)
#step3>(pre = head)          (head(2)位置上变成pre)   (head(3)位置上变成pre)   (head(4)位置上变成pre)
#step4>(head = next)         (head变成next上的3)     (head变成next上的4)      (head变成next上的none)
# 总结步骤
#>先把指针放到head.next叫做next，以防找不到
#>再把head的next指向pre，转换箭头方向
#>移动指针，head变成新的pre的位置
#>放了指针的next变成了新的head
    def findkth(self, head, k):
        for i in range(k):
            if head is None:
                return None
            head = head.next
        return head
```
