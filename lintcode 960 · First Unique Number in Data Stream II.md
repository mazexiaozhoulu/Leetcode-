```

class DataStream:

    def __init__(self):
        # do intialization if necessary
        self.dummy = ListNode(0)
        self.tail = self.dummy
        self.num_to_pre = {}
        self.duplicates = set()
    """
    @param num: next number in stream
    @return: nothing
    """
    def add(self, num):
        #如果这个数字出现了2次以上，则已经在duplicated里了，就立即返回
        if num in self.duplicates:
            return
        #如果这个数字没有在num_to_pre 这个map里出现过，说明还没出想过，就把它放到我们的linkedlist里
        if num not in self.num_to_pre:
            self.add_to_list_tail(num)
            return
        #如果这个数 在duplicates没出现过，
        #在num_to_pre出现过，说明是第二次出现，就把它删掉。然后再放到duplicates里
        self.remove(num)
        self.duplicates.add(num)
    
    def remove(self, num):
        #要remove当前点，就要把之前的点找到，用get（num）找到前一个点
        prev = self.num_to_pre.get(num)
        #并且用 next.next把当前的点跳过去
        prev.next = prev.next.next

        #并且把这个映射关系删掉
        del self.num_to_pre[num]
        #如果删除的是中间点的话，则prev.next存在，并且我们新建立这个映射关系
        if prev.next:
            self.num_to_pre[prev.next.val] = prev
        #不是中间的点的话，那现在的tail，就是prev
        else:
            self.tail = prev

    def add_to_list_tail(self, num):
        self.tail.next = ListNode(num)
        self.num_to_pre[num] = self.tail
        self.tail = self.tail.next         

    """
    @return: the first unique number in stream
    """
    def firstUnique(self):
        # write your code here
        if not self.dummy.next:
            return None
        return self.dummy.next.val
```
