# *Problem Statement :*

There are `N` network nodes, labelled `1` to `N`.

Given `times`, a list of travel times as **directed** edges `times[i] = (u, v, w)`, where `u` is the source node, `v` is the target node, and `w` is the time it takes for a signal to travel from source to target.

Now, we send a signal from a certain node `K`. How long will it take for all nodes to receive the signal? If it is impossible, return `1`.

## Sample Input

```cpp
Input: times = [[2,1,1],[2,3,1],[3,4,1]], N = 4, K = 2
```

## Sample Output

```cpp
Output: 2
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
# from collections import heapq
class Solution(object):
    def networkDelayTime(self, times, N, K):
       
        # heap   --> for priorityQueue
        # values --> store the time taken from starting node to reach that particular node
        # graph  --> adjacency list
        
        heap,values,graph = [(0,K)],{},collections.defaultdict(list)
        
        for u,v,w in times:
            graph[u].append((v,w))
            
        while heap:
            time , node = heapq.heappop(heap)
            
            # values may also be used to check if node has been visited
            if node not in values:
                
                values[node] = time
                
                for v,w in graph[node]:
                    
                    # push all neighbours in the heap while adding the weight
                    heapq.heappush(heap,(time+w,v))
                    
                    
        return max(values.values()) if len(values)==N else -1
```

## Optimal Time Space Complexity :