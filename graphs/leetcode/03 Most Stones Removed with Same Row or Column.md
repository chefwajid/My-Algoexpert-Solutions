# *Problem Statement :*

On a 2D plane, we place stones at some integer coordinate points. Each coordinate point may have at most one stone.

Now, a *move* consists of removing a stone that shares a column or row with another stone on the grid.

What is the largest possible number of moves we can make?

## Sample Input

```cpp
Input: 
// These are coordinates, not the matrix
stones = 
[
    [0,0],
    [0,1],
    [1,0],
    [1,2],
    [2,1],
    [2,2],
]
```

## Sample Output

```cpp
Output: 5
```

# *Solution 1 :*

## Explanation :

okay so most of the code is simple Union Find but WHY ~j ?????

~j ⇒ makes j NEGATIVE  and adds 1

The whole purpose of this is TO MAKE SURE I and J DONT ACCIDENTALLY COLLIDE OR END UP HAVING SAME VALUES, If this happens the union find algorithm wont work and get confused.

Also both should be very different COZ in the question it is ROW OR COLUMN

## Code :

```python
class Solution(object):
    def removeStones(self, stones):
        
        id = {}
        
        def find(x):
            return x if id[x]==x else find(id[x])
        
        def union(x,y):
            id.setdefault(x,x)
            id.setdefault(y,y)
            
            id[find(x)] = find(y)
            
        
        for i,j in stones:
            union(i,~j)
            
        return len(stones) - len({find(x) for x in id})
```

## Optimal Time Space Complexity :

Amortized O ( N ) TIME with path compression and without it is O ( N ^ 2 ) TIME