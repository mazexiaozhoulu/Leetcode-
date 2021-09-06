如果有不平衡的“【”或者“】“就都需要给balance上+1；只有“【”就先+1，使balance变的不平衡，后面有“】”就会抵消这个1；如果balance=0就说明之前平衡掉了，出现“】”就会再次不平衡，所以+1
swap就是在出现有“】”并且不平衡的时候，需要和后面“【”调换的时候+1

```
class Solution(object):
    def minSwaps(self, s):
        """
        :type s: str
        :rtype: int
        """
        balance = 0
        swap = 0
        for i in s:
            if i == '[':
                balance += 1
            else:
                if balance > 0:
                    balance -= 1
                else:
                    balance += 1
                    swap += 1
        return swap
```
