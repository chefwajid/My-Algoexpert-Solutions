# *Problem Statement :*

There are a total of `n` courses you have to take labelled from `0` to `n - 1`.

Some courses may have `prerequisites`, for example, if `prerequisites[i] = [ai, bi]` this means you must take the course `bi` before the course `ai`.

Given the total number of courses `numCourses` and a list of the `prerequisite` pairs, return the ordering of courses you should take to finish all courses.

If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

## Sample Input

```cpp
Input: numCourses = 2, prerequisites = [[1,0]]
```

## Sample Output

```cpp
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution(object):
    def findOrder(self, numCourses, prerequisites):
        
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
            return []

        # all good 
        return order
```

## Optimal Time Space Complexity :