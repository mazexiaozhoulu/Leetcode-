## 链表的基础操作，我们设置两个指针来分别存放奇节点和偶节点，最后将偶节点的表头接在奇节点的末尾即可
```
class Solution:
    """
    @param head: a singly linked list
    @return: Modified linked list
    """
    def oddEvenList(self, head):
        # write your code here
        if head is None:
            return head
        odd = head
        evenHead = head.next
        even = evenHead
        while even and even.next:
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next
        odd.next = evenHead
        return head
```
