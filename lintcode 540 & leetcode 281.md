lintcode 540 & leetcode 28
	
Zigzag Iterator


```
class ZigzagIterator:
    """
    @param: v1: A 1d vector
    @param: v2: A 1d vector
    """
    def __init__(self, v1, v2):
        # do intialization if necessary
        self.v1 = collections.deque(v1)
        self.v2 = collections.deque(v2)
        self.flag = 0

    

    """
    @return: An integer
    """
    def _next(self):
        # write your code here
        if self.flag % 2 == 1:
            if self.v1:
                return self.v1.popleft()
            else:
                return self.v2.popleft()
        else:
            if self.v2:
                return self.v2.popleft()
            else:
                return self.v1.popleft()

    """
    @return: True if has next
    """
    def hasNext(self):
        if len(self.v1)+len(self.v2) > 0:
            self.flag += 1
            return True
        else:
            return False
```
