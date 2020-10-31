# *Problem Statement :*

You're given a list of arbitrary jobs that need to completed; these jobs are represented by distinct integers. 

You're also given a list of dependencies. 

A dependency is represented as a pair of jobs where the first job is a prerequisite of the second one. 

In other words, 

- the second job depends on the first one
- it can only be completed once the first job is completed.

Write a function that takes in a list of jobs and a list of dependencies and returns a list containing a valid order in which the given jobs can completed. 

If no such order exists, the function should return an empty array.

## Sample Input

```cpp
jobs = [1, 2, 3, 4]
deps = [[1, 2], [1, 3], [3, 2], [4, 2], [4, 3]]
```

## Sample Output

```cpp
[1, 4, 3, 2] or [4, 1, 3, 2]
```

# *Solution 1 :*

## Explanation :

Topological Sort using Khans Algorithm !

**ALGORITHM**

- Find All nodes InDegree == 0

    Add all of them to the Queue

- WHILE QUEUE :

    pop the node

    Traverse edges and update InDegree of nodes 

## Code :

```cpp
from collections import deque
def topologicalSort(jobs, deps):
    
	# vertices
	N = len(jobs)
	
	# queue for nodes
	queue = deque()
	
	# initialize graph
	graph = {}
	for i in jobs:
		graph.setdefault(i,[])
		
	for i in deps:
		a = i[0] #first job
		b = i[1] #second job
		graph[a] = graph.get(a,[]) + [b]
		
	inDegree = [0 for _ in range(N+2)]
	
	# calculate and store all inDegree nodes
	for i in jobs:
		for j in graph[i]:
			inDegree[j] += 1
			
	# Enqueue all nodes with 0 inDegree
	for i in jobs:
		if inDegree[i]==0:
			queue.append(i)
			
	index = 0
	order = [-1 for _ in range(N)]
	while queue:
		t = queue.popleft()
		order[index] = t
		index+=1
		
		# check all Edges and decrement inDegree accordingly
		for i in graph[t]:
			inDegree[i] -= 1
			if inDegree[i] == 0:
				queue.append(i)
				
	if index!=N:
		return []
	return order
```

## Optimal Time Space Complexity :

O(j + d) time | O(j + d) space - where j is the number of jobs and d is the number of dependencies

or

O ( V + E ) TIME | O ( V + E ) SPACE