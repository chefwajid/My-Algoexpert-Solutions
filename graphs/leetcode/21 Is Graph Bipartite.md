# *Problem Statement :*

Given an undirected `graph`, return `true` if and only if it is bipartite.

Recall that a graph is *bipartite* if we can split its set of nodes into two independent subsets A and B, such that every edge in the graph has one node in A and another node in B.

The graph is given in the following form: `graph[i]` is a list of indexes `j` for which the edge between nodes `i` and `j` exists. Each node is an integer between `0` and `graph.length - 1`. There are no self edges or parallel edges: `graph[i]` does not contain `i`, and it doesn't contain any element twice.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d710be54-7811-4fd1-910c-b3be8b7da55f/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d710be54-7811-4fd1-910c-b3be8b7da55f/Untitled.png)

## Sample Input

```cpp
Input: graph = [[1,3],[0,2],[1,3],[0,2]]
```

## Sample Output

```cpp
Output: true
Explanation: We can divide the vertices into two groups: {0, 2} and {1, 3}.
```


## Sample Input

```cpp
Input: graph = [[1,2,3],[0,2],[0,1,3],[0,2]]
```

## Sample Output

```cpp
Output: false
Explanation: We cannot find a way to divide the set of nodes into two independent subsets.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def isBipartite(self, graph):
        
        # number of edges
        vertices = len(graph)
        
        # initilalize colors with -1 indicating not colored
        color = [-1 for _ in range(vertices)]
        
        # queue for BFS
        queue = deque()
        
        # loop over edges
        for i in range(vertices):
            
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