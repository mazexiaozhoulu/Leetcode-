## Description
Given a string S, find the length of the longest substring T that contains at most k distinct characters.

## Example
Example 1:

Input: S = "eceba" and k = 3

Output: 4

Explanation: T = "eceb"

Example 2:

Input: S = "WORLD" and k = 4

Output: 4

Explanation: T = "WORL" or "ORLD"

## time
O(n) time

```
from collections import defaultdict
class Solution:
    # @param s : A string
    # @return : An integer
    
    def lengthOfLongestSubstringKDistinct(self, s, k):

        if k == 0 or len(s) == 0:
            return 0


        char_set = defaultdict(int)
        i, j = 0, 0
        cnt, ans = 0, 0
        
        while j < len(s):
            # 统计right指向的字符
            # 当字符在窗口内第一次出现时，字符种类数+1，该字符出现次数+1
            if s[j] not in char_set or char_set[s[j]] == 0:
                cnt += 1
            char_set[s[j]] += 1
            j += 1
            
            # 向右移动left，保持窗口内只有k种不同的字符
            while cnt > k:
                char_set[s[i]] -= 1;
                if char_set[s[i]] == 0:
                    cnt -= 1
                i += 1
            # 更新答案
            ans = max(ans, j - i)
        
        return ans
```
