直播班21 1小时50分

时间复杂度: get O(1);set o(1); 空间复杂度 o(n)
![image](https://user-images.githubusercontent.com/60911066/147892215-85e38e4b-1c4f-42d5-847f-4261842d2244.png)

```
class LRUCache:
    """
    @param: capacity: An integer
    """
    def __init__(self, capacity):
        # do intialization if necessary
        self.capacity = capacity
        # OrderedDict 既可以储存 key->value pair, 也可以保存插入顺序
        self.cache = OrderedDict()

    """
    @param: key: An integer
    @return: An integer
    """
    def get(self, key):
        #如果这个key根本不存在，返回-1
        # write your code here
        if key not in self.cache:
            return -1
        #从map中删掉key->value pair
        value = self.cache.pop(key)
        #在map中存入新的key->value pair，加到最后
        self.cache[key] = value
        return value

    """
    @param: key: An integer
    @param: value: An integer
    @return: nothing
    """
    def set(self, key, value):
        # write your code here
        #如果key已经存在，
        if key in self.cache:
            #从map中删掉key->value pair
            self.cache.pop(key)
        self.cache[key] = value
        #如果cache满了，就把最早插入的kay->value pair删掉
        if len(self.cache) > self.capacity:
            #last = true时是FILO,last = False 是popFIFO
            self.cache.popitem(last = False)
```
# 总结一下大致思路：
```
LRUCache 初始化时设定最大容量，并且设置一前一后两个dummy node以便后面操作
设定三个辅助函数：
remove_node
move_to_tail
pop_front

接下来的操作就比较简单明了喽，无非是通过哈希表

统计capacity，
查找Node，
修改Node 数值，
更改Node在链表中的位置
这几个操作的组合
```
```
class Node:
    def __init__(self, key= None, value = None):
        self.key = key
        self.val = value
        self.prev = None
        self.next = None
        
class LRUCache:
    """
    @param: capacity: An integer
    """
    def __init__(self, capacity):
        self.capacity = capacity
        self.hash = {}
        self.head = Node(-1,-1) # dummy node
        self.tail = Node(-1, -1) # dummy node
        self.tail.prev = self.head
        self.head.next = self.tail
    """
    @param: key: An integer
    @return: An integer
    """
    def get(self, key):
        if key not in self.hash: return -1 
        node = self.hash[key]
        self.remove_node(node)
        self.move_to_tail(node)
        return node.val 
        
    """
    @param: key: An integer
    @param: value: An integer
    @return: nothing
    """
    def set(self, key, value):
        if self.get(key) != -1:
            self.hash[key].val = value
            return 
        if len(self.hash) >= self.capacity:
            self.pop_front()
        node = Node(key, value)
        self.move_to_tail(node)
        self.hash[key] = node
        
    def remove_node(self, node):
        node.prev.next = node.next
        node.next.prev = node.prev
        
    def move_to_tail(self, node):
        node.prev = self.tail.prev 
        node.next = self.tail 
        node.prev.next = node 
        self.tail.prev = node
        
    def pop_front(self):
        del self.hash[self.head.next.key]
        self.head.next = self.head.next.next
        self.head.next.prev = self.head
    ````
