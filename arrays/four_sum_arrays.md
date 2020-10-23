# Problem Statement:

Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. 

The function should find all quadruplets in the array that sum up to the target sum and return a two- dimensional array of all these quadruplets in no particular order. 

If no four numbers sum up to the target sum, the function should return an empty array.

## Sample Input

```cpp
array = [7, 6, 4, -1, 1, 2]
targetSUm = 16
```

## Sample Output

```cpp
[[7, 6, 4, -1], [7, 6, 1, 2]]
```

# *Solution 1 :*

- [x]  Done on my own

## Explanation :

## Code :

```cpp
def fourNumberSum(array, targetSum):
    
	fourlets = []
	
	for i in range(len(array)):
		a = array[i]
		for j in range(i+1,len(array)):
			b = array[j]
			for k in range(j+1,len(array)):
				c = array[k]
				for l in range(k+1,len(array)):
					d = array[l]
					
					if a + b + c + d == targetSum:
						fourlet = [a,b,c,d]
						fourlet.sort()
						if fourlet not in fourlets:
							fourlets.append(fourlet)
							
	return fourlets
```

## Time Space Complexity :

O ( N^4 ) TIME | O ( N^2 ) SPACE

# *Solution 2 :*

- [x]  Done on my own

## Explanation :

## Code :

```cpp
def fourNumberSum(array, targetSum):
    
	fourlets = []
	array.sort()
	
	for i in range(len(array)):
		for j in range(i+1,len(array)):
			
			a = array[i]
			b = array[j]
			
			start = j + 1
			end = len(array) - 1
			
			while start < end :
				c = array[start]
				d = array[end]
				if i==1:
					print(i,j,start,end)
					print(a,b,c,d)
					print(a + b + c + d)
				currentSum = a + b + c + d
				fourlet = [a,b,c,d]
				
				if currentSum == targetSum:
					if fourlet not in fourlets:
						fourlets.append(fourlet)
					start+=1
					
				elif currentSum > targetSum:
					end -= 1
					
				else:
					start+=1
					
	return fourlets
```

## Time Space Complexity :

O ( N ^ 3 ) TIME | O ( N^2 ) SPACE