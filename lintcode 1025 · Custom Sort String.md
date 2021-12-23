leetcode 791. Custom Sort String
建立一个新的ans list最后再转换成str
用字典统计所有存在T的char 出现的次数
再遍历s，给ans返回在出现在s里的char，并 * 字典里出现的次数，之后把出现次数归零（这样才可以避免之后计算其他的字母时，发生重复）
在计算其他的字母
```
class Solution:
    def customSortString(self, S, T):
        countT = collections.Counter(T)
        ans = []

        # Write all characters that occur in S, in the order of S.
        for char in S:
            ans.append(char * countT[char])
            countT[char] = 0

        for char in countT:
            ans.append(char * countT[char])

        return "".join(ans)
```
