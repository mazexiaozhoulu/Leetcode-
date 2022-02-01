## Description
Given a string S with only lowercase characters.

Return the number of substrings that contains at least k distinct characters.
## Example
Example 1:

Input: S = "abcabcabca", k = 4

Output: 0

Explanation: There are only three distinct characters in the string.

Example 2:

Input: S = "abcabcabcabc", k = 3

Output: 55

Explanation: Any substring whose length is not smaller than 3 contains a, b, c.

For example, there are 10 substrings whose length are 3, "abc", "bca", "cab" ... "abc"
    
There are 9 substrings whose length are 4, "abca", "bcab", "cabc" ... "cabc"

...
    
There is 1 substring whose length is 12, "abcabcabcabc"
    
So the answer is 1 + 2 + ... + 10 = 55.

## 方法：
> 同向双指针
> hash map 统计当前i-j之间的字符
> diffierent_chars记录不同字符的个数，如果当前字符在hash map里第一次出现，那就diffierent_chars += 1；如果在hashmap里归零，那就-=1
> num_of_substring += n - j + 1;n-j+1 是因为 i-j之间有了k个不同的字母，所以j之后道n之间所有的字符都可以算成新的情况，所以只要计算j到n中有多少字母就行。
```
from collections import defaultdict
class Solution:
    """
    @param s: a string
    @param k: an integer
    @return: the number of substrings there are that contain at least k distinct characters
    """

    def kDistinctCharacters(self, s, k):
        # Write your code here
        if len(s) == 0:
            return 0

        n = len(s)
        num_of_substring = 0
        diffierent_chars = 0
        counter = defaultdict(int)
        j = 0

        for i in range(n):
            while j < n and diffierent_chars < k:
                counter[s[j]] += 1
                if counter[s[j]] == 1:
                    diffierent_chars += 1
                j += 1

            if diffierent_chars == k:
                num_of_substring += n - j + 1
            #因为下一个循环是i+1，所以这里的counter[s[i]]要把当前i的数量剪掉一个
            counter[s[i]] -= 1

            if counter[s[i]] == 0:
                diffierent_chars -= 1
        return num_of_substring

```
