为了实现O(1)的time complexity,

Insert操作：list.append() / hashmap的添加

Remove操作： list.pop() / hashmap的del key=数字；value=index；

Random操作： list.choice()

最后用list保存set中的数，用hashmap保存每个数的index。

需要删除的时候，把list末尾的元素和target对调，然后pop末尾。并更新hashmap中的记录。
```
from random import choice
class RandomizedSet(object):

    def __init__(self):
        """
        Initialize your data structure here.
        """
        
        self.dict = {}
        self.list = []
    def insert(self, val):
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        :type val: int
        :rtype: bool
        """
        if val in self.dict:
            return False
        self.dict[val] = len(self.list)
        self.list.append(val)
        return True

    def remove(self, val):
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        :type val: int
        :rtype: bool
        """
        if val in self.dict:
            index = self.dict[val]
            lastElement = self.list[-1]
            self.list[index], self.dict[lastElement] = lastElement, index
            ##只保留需要留下的部分，list把最后一个字符覆盖掉要删掉的字符，再把最后一个字符删掉：比如：[1,2,3,4], 要删掉3, 通过这步就变成[1,2,4,4]，再把最后一个4删掉。dict同理
            self.list.pop()
            del self.dict[val]
            return True
        return False
            

    def getRandom(self):
        """
        Get a random element from the set.
        :rtype: int
        """
        return choice(self.list)
        


# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```
