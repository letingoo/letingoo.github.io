---
layout: post
title: Leetcode 134：Gas Station
---


> There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

> You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

> Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

> Note:
> The solution is guaranteed to be unique.


---

暴力求解的时间复杂度是N^2。O(N)的解法如下：

从0开始遍历数组，一个变量tank = tank + gas[i] - cost[i]。如果从0开始不能到达i，那么从0到i都不能成为起点。这用反证法可以证明：
假设从i开始，到j-1时发现不能到达j。若有一点k(i <= k <= j)可以作为起点，则
i...k...j整体为负，而k...j整体为正，则i...k-1为负，则刚才时不可能从i走到j的。

代码如下：
```
int canCompleteCircuit(int[] gas, int[] cost) {
	int total = 0, tank = 0, index = 0;
	for (int i = 0; i < cost.length; i++) {
		int cur = gas[i] - cost[i];			

		tank += cur;
		if (tank < 0) {//if sum < 0, index can only start from i + 1
			index = i + 1;
			tank = 0;
		}
		total += cur;			
	}		
	return total < 0 ? -1 : index;
}

```