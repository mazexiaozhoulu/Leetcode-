# 219 · 在排序链表中插入一个节点

题目题解笔记讨论排名
描述
在链表中插入一个节点。

样例
样例 1：

输入：head = 1->4->6->8->null, val = 5
输出：1->4->5->6->8->null
样例 2：

输入：head = 1->null, val = 2
输出：1->2->null

想法: 1: 声明一个dummy，dummy是linkedlist头节点之前的节点。
2: 如果当前节点的值小于我们寻找的值，那就继续，如果等于，那就把指针指到下一个值，并把我们想要插入的值放到指针的地方。


point: 1:我们是从dummy = current 开始的，所以要注意current和current.next
2: return dummy.next 和 return head不一样。return head就是在return原来链表的第一个，但如果我们加的是一个头节点，那就得return新的头节点。所以我们要return dummy.next


```
class Solution:
    """
    @param head: The head of linked list.
    @param val: An integer.
    @return: The head of new linked list.
    """
    def insertNode(self, head, val):
        dummy = ListNode(0)
        dummy.next = head
        current = dummy

        while current.next and current.next.val <= val:
            current = current.next
        
        newNode = ListNode(val)
        newNode.next = current.next
        current.next = newNode

        return dummy.next
```        
# 174 · 删除链表中倒数第n个节点
算法
描述
给定一个链表，删除链表中倒数第n个节点，返回链表的头节点。

思路：因为我们不知道这个linkedlist有多长，所以 倒数第n个 就是 快指针先指到正数第n个，快慢指针再同时移动，当快指针指到最后一个的时候，慢指针也就指到了倒数第n个。（窗口方法）

链表中的节点个数大于等于n

样例
样例 1:
	输出: list = 1->2->3->4->5->null， n = 2
	输出: 1->2->3->5->null


样例 2:
	输入:  list = 5->4->3->2->1->null, n = 2
	输出: 5->4->3->1->null
  
  
``` 
 class Solution:
    """
    @param head: The first node of linked list.
    @param n: An integer
    @return: The head of linked list.
    """
    def removeNthFromEnd(self, head, n):
        if not head or n < 0:
            return 
        
        if n == 0:
            return head
        
        dummy = ListNode(0)
        dummy.next = head
        slow = dummy
        fast = dummy
        
        i = 0
        while i < n and fast:
            fast = fast.next
            i += 1
        # if n is greater than the total number of lists
        if i != n:
            return head

        # fast is in the end of the list
        # slow is in the previous of nth node from the end of list
        while slow.next and fast.next:
            slow = slow.next
            fast = fast.next
        
        # disconnect the node, 
        slow.next = slow.next.next
        
        return dummy.next
        
```
# 165 · 合并两个排序链表
算法

题目题解笔记讨论排名
描述
将两个排序（升序）链表合并为一个新的升序排序链表

样例
样例 1:
	输入: list1 = null, list2 = 0->3->3->null
	输出: 0->3->3->null


样例2:
	输入:  list1 =  1->3->8->11->15->null, list2 = 2->null
	输出: 1->2->3->8->11->15->null
  
思路： 新建一个linkedlist，tail,next总是指向l1和l2种更小的一个。
point： 如果l1或者l2中一个结束了，那么tail.next就指向唯一存在的一个
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
