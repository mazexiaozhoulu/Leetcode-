回溯
```
class Solution:
    """
    @param nums: A set of numbers
    @return: A list of lists
    """
    def subsets(self, nums):
        # write your code here
        result = []
        if not nums:
            return [[]]
        if len(nums) == 0:
            return [[]]

        nums.sort()
        self.dfs(nums, 0, [], result)
        return result

    def dfs(self, nums, index, subset, results):
        results.append(subset[:])
        for i in range(index, len(nums)):
            subset.append(nums[i])
            self.dfs(nums, i+1, subset, results)
            subset.pop(-1) #backtracking
```
# 使用BFS排列的思路，queue种的每一次subset再向后进行选择，但是因为没有记录index，
# 所以用 subset[-1] < nums[i]来找index
```
            if not nums:
                return [[]]
            queue = [[]]
            index = 0
            # 把nums里出现的数字都放到queue里
            while index < len(queue):
                subset = queue[index]
                index += 1
                #
                for num in nums:
                    if subset and subset[-1] >= num:
                        continue
                    print('subset+[num]',subset+[num])
                    queue.append(subset+[num])
                    
            return queue
```
