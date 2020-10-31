# *Problem Statement :*

Given a set of `N` people (numbered `1, 2, ..., N`), we would like to split everyone into two groups of **any** size.

Each person may dislike some other people, and they should not go into the same group.

Formally, if `dislikes[i] = [a, b]`, it means it is not allowed to put the people numbered `a` and `b` into the same group.

Return `true` if and only if it is possible to split everyone into two groups in this way.

## Sample Input

```cpp
Input: N = 4, dislikes = [[1,2],[1,3],[2,4]]
```

## Sample Output

```cpp
Output: true
Explanation: group1 [1,4], group2 [2,3]
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def possibleBipartition(self, N, dislikes):
        # edge case
        if len(dislikes)<=0:
            return True
        
        # number of edges
        vertices = N
        
        graph = {}
        
        for i in range(1,N+1):
            graph.setdefault(i,[])
        
        for i,j in dislikes:
            graph[i] = graph.get(i,[]) + [j]
            graph[j] = graph.get(j,[]) + [i]
            
        # number of edges
        vertices = len(graph)
        
        # initilalize colors with -1 indicating not colored
        color = [-1 for _ in range(vertices+1)]
        
        # queue for BFS
        queue = deque()
        
        # loop over edges
        for i in range(1,vertices+1):
            
            # ignore if edge already colored 
            if color[i] != -1:
                continue
              
            # start with a color for the vertex and it to the queue
            color[i] = 1
            queue.append(i)
            
            while queue:
                z = queue.popleft()
                
                for r in graph[z]:
                    
                    if color[r] == -1:
                        # color the edge with either '1' or '0' and add to queue
                        color[r] = 1 - color[z]
                        queue.append(r)
                        
                    elif color[r]==color[z]:
                        # if at any point the colors of adjacent vertices match
                        # bipartite not possible
                        return False
        
        return True
```

## Optimal Time Space Complexity :