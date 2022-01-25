# Description
Merge k sorted linked lists and return it as one sorted list.

Analyze and describe its complexity.
# Example 1:

Input:

lists = [2->4->null,null,-1->null]

Output:

-1->2->4->null

# brute force 

Time complexity : O(NlogN) where NN is the total number of nodes.

```
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        result = []
        head = point = ListNode(0)
        for l in lists:
            while l:
                result.append(l.val)
                l = l.next
                
        for x in sorted(result):
            point.next = ListNode(x)
            point = point.next
        return head.next

```
# heap
 time complexity is O(n log k), because we have O(n) steps, where we put and remove from heap, 
 which have at most k elements. Space complexity is O(n): because we need to return newly constructed linked list.
 
> Create 'dummy' node in linked list, which will help us to deal with border cases, such as empty lists and so on.
> 'curr' is current element in linked list where are in now.
> Put all starts of 'k' linked lists to heap (actually there can be less than k, because some of lists can be empty)
> Extract 'val, ind' element from our heap: it will be current minumum element, and attach it to the end of constucted merged least so far, move 'curr' iterator to the right.
> If we still did not reach the end of current list, move one step to the right in this list and put new candidate to heap.
> Return 'dummy.next'.

```
from heapq import heappop, heappush

class Solution:
        # K 指针指向 K 条链表，每次使用小根堆求出最小值
    def mergeKLists(self, lists):
        dummy = curr = ListNode(0)
        heap = []
        for ind, el in enumerate(lists):
            if el: 
                heappush(heap, (el.val, ind))
                
        while heap:
            # 用heap把listnode按照index弹出来，再把index对应的数字返回到node
            val, ind = heappop(heap)
            curr.next = ListNode(val)
            curr = curr.next
            # 再把这个linkedlist里的下一个node放进heap里
            if lists[ind].next:
                lists[ind] = lists[ind].next
                heappush(heap, (lists[ind].val, ind))
                
        return dummy.next
```
