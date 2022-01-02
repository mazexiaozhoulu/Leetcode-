直播班21 1小时50分
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
        #在map中存入新的key->value pair
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
