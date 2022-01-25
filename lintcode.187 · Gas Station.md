# Description
There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

# Example
Example 1:

Input:gas[i]=[1,1,3,1],cost[i]=[2,2,1,1]
Output:2
Example 2:

Input:gas[i]=[1,1,3,1],cost[i]=[2,2,10,1]
Output:-1

# complexity
o(n)
```
class Solution:

    def canCompleteCircuit(self, gas, cost):
        #只要gas 总量< cost总量，没办法完成全程
        if sum(gas) < sum(cost):
            return -1
            
        index = 0
        gas_remain = 0
        
        for i in range(len(gas)):
            #之前gas[i] - cost[i]就是剩下的油
            #再把剩下的油+新的station的油量
            gas_remain += gas[i]-cost[i]
            #如果<0，那就还原为0，index+1选下一个节点为开始点
            if gas_remain < 0:
                gas_remain = 0
                index = i+1
                
        return index
```
