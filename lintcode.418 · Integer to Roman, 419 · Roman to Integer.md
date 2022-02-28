## Example
Example 1:

Input: 1
Output: "I"
Example 2:

Input: 99
Output: "XCIX"

```
    def intToRoman(self, n):
        # write your code here
        rom = ["M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"]
        digit = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1]
        result = ""
        
        for d, r in zip(digit, rom):
            result += r * (n // d)
            n %= d 
        return result
```
## Example
Example 1:

Input: "IV"
Output: 4
Example 2:

Input: "XCIX"
Output: 99

```
class Solution:
    """
    @param s: Roman representation
    @return: an integer
    """
    def romanToInt(self, s: str) -> int:
        d = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        res = 0
        for i in range(len(s) - 1):
            if d[s[i]] < d[s[i + 1]]:
                res -= d[s[i]]
            else:
                res += d[s[i]]
        return res + d[s[-1]]
```
