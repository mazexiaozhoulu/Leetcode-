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
push_back
kick(move to tail)
pop_front

接下来的操作就比较简单明了喽，无非是通过哈希表

统计capacity，
查找Node，
修改Node 数值，
更改Node在链表中的位置
这几个操作的组合
```
```
class LinkedNode:
    
    def __init__(self, key=None, value=None, next=None):
        self.key = key
        self.value = value
        self.next = next

class LRUCache:

    # @param capacity, an integer
    def __init__(self, capacity):
        self.key_to_prev = {}
        self.dummy = LinkedNode()
        self.tail = self.dummy
        #最大容量，超过就删数据
        self.capacity = capacity
        
    #把数据插入到链表尾部
    def push_back(self, node):
    #当前的tail为新的node的前一个节点
        self.key_to_prev[node.key] = self.tail
        #尾部加入新的节点
        self.tail.next = node
        #tail的指针指向新的节点
        self.tail = node
    
    def pop_front(self):
        # 删除头部节点
        head = self.dummy.next
        #在hashmap里删除节点的映射关系
        del self.key_to_prev[head.key]
        #dummy后移，指向新的头部节点
        self.dummy.next = head.next
        #再hashmap里更新新的头节点映射关系
        self.key_to_prev[head.next.key] = self.dummy
        
    # change "prev->node->next...->tail"
    # to "prev->next->...->tail->node"
    def kick(self, prev):	#将数据移动至尾部
        node = prev.next
        #如果已经在链表尾部就不用移动
        if node == self.tail:
            return
        #删除node节点
        # node前一个指向node的下一个
        prev.next = node.next
        # 更新node下一个节点对应的前导节点
        self.key_to_prev[node.next.key] = prev
        #断开node指向node下一个节点的链接
        node.next = None
        #把node放到队尾
        self.push_back(node)

   
    def get(self, key):
    #不在缓存里就返回-1
        if key not in self.key_to_prev:
            return -1
        #找到这个点的前一个节点
        prev = self.key_to_prev[key]
        current = prev.next
        #再把prev应用到kick函数
        self.kick(prev)
        return current.value

    def set(self, key, value):
    #已经存在的话就更新value
        if key in self.key_to_prev:	   
        #这个node被更新过，所以移动到链表尾端
            self.kick(self.key_to_prev[key])
            #更新节点的值
            self.key_to_prev[key].next.value = value
            return
        #不存在的话，就存入新节点
        self.push_back(LinkedNode(key, value))  
        #判断是否超出容量
        if len(self.key_to_prev) > self.capacity:		
            self.pop_front()		
    ````
