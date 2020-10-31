# *Problem Statement :*

There are `n` computers numbered from `0` to `n-1` connected by ethernet cables `connections` forming a network where `connections[i] = [a, b]` represents a connection between computers `a` and `b`. Any computer can reach any other computer directly or indirectly through the network.

Given an initial computer network `connections`. 

You can extract certain cables between two directly connected computers, and place them between any pair of disconnected computers to make them directly connected. 

Return the *minimum number of times* you need to do this in order to make all the computers connected. If it's not possible, return -1.



## Sample Input

```cpp
Input: n = 4, connections = [[0,1],[0,2],[1,2]]
```

## Sample Output

```cpp
Output: 1
Explanation: Remove cable between computer 1 and 2 and place between computers 1 and 3.
```

[Number of Operations to Make Network Connected - LeetCode](https://leetcode.com/problems/number-of-operations-to-make-network-connected/)

# *Solution 1 :*

## Explanation :

Well - commented code

## Code :

```cpp
class Solution(object):
    
    def makeConnected(self, n, connections):
        id = {}
        sz = []
        
        #Initialization
        for i in range(n):
            id.setdefault(i,i)
            sz.append(1)
        
        #UnionFind Logic
        def find(x):
            return x if id[x]==x else find(id[x])
        
        def connected(x,y):
            return find(x) == find(y)
        
        def union(i,j):
            if(connected(i,j)):
                return
            
            i = find(i)
            j = find(j)
           
            id[i] = j
            sz[j] += sz[i]
            
        #Call UnionFind
        for i,j in connections:
            union(i,j)
            
        #Total Components
        components = len({find(x) for x in id})
        
        #Edges needed for N computers is N-1
        EdgesNeededForNewConnections = components - 1
        
        #Total Connections - Connections Utilized
        connectionsleft = len(connections) - (max(sz) - 1)
        
        isConnectionPossible = connectionsleft >= EdgesNeededForNewConnections 
        
        return EdgesNeededForNewConnections if isConnectionPossible else -1
```

## Optimal Time Space Complexity :

Amortized O ( N ) TIME with Path Compression and O ( N ^ 2 ) TIME without