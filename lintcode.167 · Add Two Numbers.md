## Description
You have two numbers represented by a linked list, where each node contains a single digit. The digits are stored in reverse order, such that the 1's digit is at the head of the list. Write a function that adds the two numbers and returns the sum as a linked list.

Wechat reply the【BAT】get the latest frequent Interview questions of ByteDance, Alibaba, etc. (wechat id :jiuzhang15)

## Example
Example 1:

Input: 7->1->6->null, 5->9->2->null
Output: 2->1->9->null	
Explanation: 617 + 295 = 912, 912 to list:  2->1->9->null
```
class Solution:
    """
    @param l1: the first list
    @param l2: the second list
    @return: the sum list of l1 and l2 
    """
    def add_lists(self, l1: ListNode, l2: ListNode) -> ListNode:
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        ret = cur = ListNode(0); val = 0;
        while l1 or l2 or val:
            if l1: 
                val += l1.val; 
                l1 = l1.next;
            if l2: 
                val += l2.val; 
                l2 = l2.next
            cur.next = cur = ListNode(val%10); 
            val //= 10
        return ret.next
```
