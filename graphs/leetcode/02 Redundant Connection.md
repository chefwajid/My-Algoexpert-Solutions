# *Problem Statement :*

**Medium**

In this problem, a tree is an **undirected** graph that is connected and has no cycles.

The given input is a graph that started as a tree with N nodes (with distinct values 1, 2, ..., N), with one additional edge added. The added edge has two different vertices chosen from 1 to N, and was not an edge that already existed.

The resulting graph is given as a 2D-array of `edges`. Each element of `edges` is a pair `[u, v]` with `u < v`, that represents an **undirected** edge connecting nodes `u` and `v`.

Return an edge that can be removed so that the resulting graph is a tree of N nodes. If there are multiple answers, return the answer that occurs last in the given 2D-array. The answer edge `[u, v]` should be in the same format, with `u < v`.

**Example 1:**

```
Input: [[1,2], [1,3], [2,3]]
Output: [2,3]
Explanation: The given undirected graph will be like this:
  1
 / \
2 - 3

```

**Example 2:**

```
Input: [[1,2], [2,3], [3,4], [1,4], [1,5]]
Output: [1,4]
Explanation: The given undirected graph will be like this:
5 - 1 - 2
    |   |
    4 - 3
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
class Solution {
    
    private int[] parent;
    
    public void init(int size)
    {
        parent = new int[size];
        for(int i=0;i<size;i++)
        {
						// All nodes are parent of themselves
            parent[i]=i;
        }
    }
    
    public int find(int x){
				// If their parents are themselves, that is a parent
				// else it's a child, keep searching
        return parent[x] == x ? x : find(parent[x]);
    }
    
    public int[] findRedundantConnection(int[][] edges) {
        init(edges.length*2);
        int[] res = new int[2];
        
        for(int i=0;i<edges.length;i++)
        {
            int root1 = find(edges[i][0]);
            int root2 = find(edges[i][1]);
            
            if(root1!=root2){
                parent[root1] = root2;
            }else{
                res[0] = edges[i][0];
                res[1] = edges[i][1];
            }

        }
        
        return res;
    }
}
```

## Optimal Time Space Complexity :

normal : O ( N ^ 2 )

path compression : Amortized O ( N )