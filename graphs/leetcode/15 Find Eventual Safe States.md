# *Problem Statement :*

In a directed graph, we start at some node and every turn, walk along a directed edge of the graph. If we reach a node that is terminal (that is, it has no outgoing directed edges), we stop.

Now, say our starting node is *eventually safe* if and only if we must eventually walk to a terminal node. More specifically, there exists a natural number `K` so that for any choice of where to walk, we must have stopped at a terminal node in less than `K` steps.

Which nodes are eventually safe? Return them as an array in sorted order.

The directed graph has `N` nodes with labels `0, 1, ..., N-1`, where `N` is the length of `graph`. 

The graph is given in the following form: `graph[i]` is a list of labels `j` such that `(i, j)` is a directed edge of the graph.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9d259d54-de55-46f8-b1ac-95ded9c05590/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9d259d54-de55-46f8-b1ac-95ded9c05590/Untitled.png)

## Sample Input

```cpp
Input: graph = [[1,2],[2,3],[5],[0],[5],[],[]]
```

## Sample Output

```cpp
Output: [2,4,5,6]
Here is a diagram of the above graph.
```

# *Solution 1 :*

## Explanation :

## Code :

PYTHON

```python
class Solution(object):
    def eventualSafeNodes(self, graph):
        
        cyclenodes = []
        safenodes = []
        
        
        def dfs(i,visited):
            
            if i in cyclenodes:
                return False
            elif i in safenodes:
                return True
            elif i in visited:
                cyclenodes.append(i)
                return False
            
            visited.append(i)
            
            for j in graph[i]:
                if not dfs(j,visited):
                    cyclenodes.append(j)
                    return False
                
            safenodes.append(i)
            return True
        
        answer=[]
        for index,elem in enumerate(graph):
            if dfs(index,[]):
                answer.append(index)
        
        return answer
```

JAVA

```cpp
class Solution {

    public List<Integer> eventualSafeNodes(int[][] graph) {
        List<Integer> res = new ArrayList<>();
        if(graph == null || graph.length == 0)  return res;
        
        int nodeCount = graph.length;
        int[] color = new int[nodeCount];
        
        for(int i = 0;i < nodeCount;i++){
            if(dfs(graph, i, color))    res.add(i);
        }
        
        return res;
    }

    public boolean dfs(int[][] graph, int start, int[] color){
        if(color[start] != 0)   return color[start] == 1;
        
        color[start] = 2;
        for(int newNode : graph[start]){
            if(!dfs(graph, newNode, color))    return false;
        }
        color[start] = 1;
        
        return true;
    }
}
```

## Optimal Time Space Complexity :