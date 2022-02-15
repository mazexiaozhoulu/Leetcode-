## Description
To give you a string array, please group the misplaced words(refers to the same character string with different permutations).

All inputs will be in lower-case.

Example
Example 1:

Input:

["eat","tea","tan","ate","nat","bat"]

Output:

[["ate","eat","tea"],

 ["bat"],
 
 ["nat","tan"]]
 
 ## hashmap  
O(NKlogK), where N is the length of strs, and K is the maximum length of a string in strs
 ```
 class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        ans = collections.defaultdict(list)
        for s in strs:
            s1 = sorted(s)
            ans[tuple(s1)].append(s)
        return ans.values()
 ```

 
