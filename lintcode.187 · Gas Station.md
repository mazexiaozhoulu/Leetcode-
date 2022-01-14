```
class Solution:

    def canCompleteCircuit(self, gas, cost):
        
        if sum(gas) < sum(cost):
            return -1
            
        index = 0
        gas_remain = 0
        
        for i in range(len(gas)):
            
            gas_remain += gas[i]-cost[i]
            if gas_remain < 0:
                gas_remain = 0
                index = i+1
                
        return index
```
