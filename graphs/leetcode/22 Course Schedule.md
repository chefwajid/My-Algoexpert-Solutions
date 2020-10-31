# *Problem Statement :*

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite **pairs**, is it possible for you to finish all courses?

## Sample Input

```cpp
Input: numCourses = 2, prerequisites = [[1,0]]
```

## Sample Output

```cpp
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        
        # vertices of graph
        N = numCourses
        
        # adjacency list
        graph = {}
        
        # initialize graph
        for i in range(N):
            graph.setdefault(i,[])
        
        for i in prerequisites:
            a = i[0]
            b = i[1]
            graph[b] = graph.get(b,[]) + [a]
                
        # initialize indegree array
        inDegree = [0 for _ in range(N)]
        for i in range(N):
            for j in graph[i]:
                inDegree[j] += 1

        # queue for zero dependency nodes
        queue = deque()
        
        # enqueue nodes with zero dependency
        for i in range(N):
            if inDegree[i]==0:
                queue.append(i)
        
        # initialize order array
        index = 0
        order = [-1 for _ in range(N)]
        
        # loop while queue not empty
        while queue:
            t = queue.popleft()
            order[index] = t
            index += 1
            for j in graph[t]:
                # decrease neighbouring node degrees
                inDegree[j] -= 1
                # if zero dependency add in queue
                if inDegree[j]==0:
                    queue.append(j)

        # if index did not reach number of nodes, cycle exists
        if index!=N:
            return False

        # all good 
        return True
```

## Optimal Time Space Complexity :