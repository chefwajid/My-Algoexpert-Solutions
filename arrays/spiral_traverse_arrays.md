# *Problem Statement :*

Write a function that takes in an n x m two-dimensional array (that can be square-shaped when n m) and returns a one-dimensional array of all the array's elements in spiral order. 

Spiral order starts at the top left corner of the two-dimensional array, goes to the right, and proceeds in a spiral pattern all the way until every element has been visited.

## Sample Input

```cpp
array = [
  [1,   2,  3, 4],
  [12, 13, 14, 5],
  [11, 16, 15, 6],
  [10,  9,  8, 7],
]
```

## Sample Output

```cpp
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16]
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
def spiralTraverse(array):
    
	i,j = 0,0
	rows,cols = len(array),len(array[0])
	startingRow,endingRow = 0,rows
	startingCol,endingCol = 0,cols
	result = []
	
	while startingRow < endingRow and startingCol < endingCol:
		
		for j in range(startingCol,endingCol):
			result.append(array[i][j])
			
		startingRow += 1
		
		for i in range(startingRow,endingRow):
			result.append(array[i][j])

		endingCol -= 1
		
		for j in reversed(range(startingCol,endingCol)):
			if startingRow >= endingRow:
				break
			result.append(array[i][j])

		endingRow -= 1
		
		for i in reversed(range(startingRow,endingRow)):
			if startingCol >= endingCol:
				break
			result.append(array[i][j])

		startingCol += 1
		
		
	return result
```

## Optimal Time Space Complexity :

O ( N^2 ) TIME | O ( N ) SPACE