## Description
Given two strings source and target. Return the minimum substring of source which contains each char of target.

## Example
Example 1:

Input:

source = "abc"

target = "ac"

Output:

"abc"

Explanation:

"abc" is the minimum substring of source string which contains each char of target "ac".

Example 2:

Input:

source = "adobecodebanc"

target = "abc"

Output:

"banc"

Explanation:

"banc" is the minimum substring of source string which contains each char of target "abc".
## 思路：
>统计出现在target中的字符数量

>使用双指针算法

>如果当前的字符数量，恰好满足或者恰好不满足要求，更新计数器

> 对于合适的子串，更新子穿的起点和长度

> 将答案更新为更短的字符

## 时间复杂度o(n+m)
```
class Solution:
    """
    @param source : A string
    @param target: A string
    @return: A string denote the minimum window, return "" if there is no such a string
    """
    def minWindow(self, s , t):
        # 初始化,need 的初始化是t的字符情况，在这个窗口中，这个字符，t比s少几个
        need = collections.defaultdict(int)
        for char in t:
            need[char] += 1
        needCNT = len(t)
        i = 0
        res = (0,float('inf'))

        #遍历s,把s的字符情况统计到need里, 如果s的情况是多余，那就-; 如果刚好，那need[char]减到0；
        #只要S的这个字符在t里出现过，那distance就变短。
        for j,char in enumerate(s):
            if need[char] > 0:
                needCNT -= 1
            need[char] -= 1
            #如果distance 变为0了。那说明是完整的区间，我们需要通过移动i剪掉多余的字符
            if needCNT == 0:
                while need[s[i]] != 0: #value！=0；说明是多余的
                    need[s[i]] += 1 # s里i移动的同时，这个字符的频次就比t中出现的少一个
                    i += 1
                if j-i<res[1]-res[0]:   #记录结果
                    res=(i,j)
                # i向右移动（+1），那就是t中这个字符多出来一个，距离（needCNT）+1
                need[s[i]] += 1
                needCNT += 1
                i += 1
        return '' if res[1]>len(s) else s[res[0]:res[1]+1] 

```
