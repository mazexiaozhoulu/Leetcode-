```
class LinkedNode:
    def __init__(self, key=None, value=None, next=None):
        self.key = key
        self.value = value
        self.next = next

class LRUCache:
    """
    @param: capacity: An integer
    """
    def __init__(self, capacity):
        # do intialization if necessary
        self.capacity = capacity
        self.dummy = LinkedNode()
        self.tail = self.dummy
        self.key_to_pre = {}
        
    """
    @param: key: An integer
    @return: An integer
    """

    def push_back(self, node):
        self.key_to_pre[node.key] = self.tail
        self.tail.next = node
        self.tail = node
    
    def pop_front(self):
        head = self.dummy.next
        del self.key_to_pre[head.key]
        self.dummy.next = head.next
        self.key_to_pre[head.next.key] = self.dummy

    """
    @param: key: An integer
    @param: value: An integer
    @return: nothing
    """
    def set(self,key,value):
        if key in self.key_to_pre:
            self.kick(key)
            self.tail.value = value
            return
        self.push_back(LinkedNode(key, value))
        if len(self.key_to_pre)>self.capacity:
            self.pop_front()
    #当前的node kick到tail，原来的tail变成倒数第二个点
    def kick(self,key):
        #首先找爸爸是谁
        prev = self.key_to_pre[key]
        key_node = prev.next
        #如果当前点就是最后一个点，就直接return
        if key_node == self.tail:
            return
        #key node 前一个节点，指向下一个节点，跳掉key node。
        #更新key node的前导节点
        #断开key node的链接，指向none
        prev.next = key_node.next
        self.key_to_pre[key_node.next.key]=prev
        key_node.next = None

        self.push_back(key_node)
    #get某个数据；不存在的返回-1， 存在的话就kick到后面去，变成tail   
    def get(self, key):
        # write your code here
        if key not in self.key_to_pre:
            return -1
        self.kick(key)
        return self.tail.value

```
OrderedDict
```
from collections import OrderedDict
class LRUCache:
    """
    @param: capacity: An integer
    """
    def __init__(self, capacity):
        # do intialization if necessary
        self.capacity = capacity
        self.cache = OrderedDict()

    """
    @param: key: An integer
    @return: An integer
    """
    def get(self, key):
        # write your code here
        if key not in self.cache:
            return -1
        value = self.cache.pop(key)
        self.cache[key] = value
        return value

    """
    @param: key: An integer
    @param: value: An integer
    @return: nothing
    """
    def set(self, key, value):
        # write your code here
        if key in self.cache:
            self.cache.pop(key)
        self.cache[key] = value
        if len(self.cache) > self.capacity:
            self.cache.popitem(last = False)

```
