## Description
Given a string, find the length of the longest substring without repeating characters.

## Example
Example 1:

Input: "abcabcbb"

Output: 3

Explanation: The longest substring is "abc".

Example 2:

Input: "bbbbb"

Output: 1

Explanation: The longest substring is "b".

## time complexity 
O(n)


## 方法
        #>two point i,j in one direction
        #>set count char in i-j
        #>count(s[i]) > 1 then result = max(j-i,result)
```
from collections import defaultdict
class Solution:
    """
    @param s: a string
    @return: an integer
    """
    def lengthOfLongestSubstring(self, s):
        # write your code here
        if len(s) == 0:
            return 0

        n = len(s)
        count = set()
        j = 0
        result = 0
        
        for i in range(n):
            while j < n and s[j] not in count:
                count.add(s[j])
                j += 1
            result = max(j-i, result)
            count.remove(s[i])
                        
        return result
```
