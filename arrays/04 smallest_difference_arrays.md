# Problem Statement:

 Write a function that takes in two non-empty arrays of integers, finds the pair of numbers (one from each array) whose absolute difference is closest to zero, and returns an array containing these two numbers, with the number from the first array in the first position. 

Note that the absolute difference of two integers is the distance between them on the real number line. 

For example, the absolute difference of -5 and 5 is 10, and the absolute difference of -5 and -4 is 1. You can assume that there will only be one pair of numbers with the smallest difference.

## Sample Input

```cpp
arrayOne = [-1, 5, 10, 20, 28, 3]
arrayTwo = [26, 134, 135, 15, 17]
```

## Sample Output

```cpp
[ 28 , 26 ]
```

# *Solution 1 :*

- [x]  Done on my own

## Explanation :

## Code :

```cpp
import sys
def smallestDifference(arrayOne, arrayTwo):
    
	closestToZero = sys.maxsize
	pair = [0,0]
	
	for i in arrayOne:
		for j in arrayTwo:
			if abs(i-j) < closestToZero:
				pair = [i,j]
				closestToZero = abs(i-j)
			
	return pair
```

## Time Space Complexity :

O ( N ^ 2 ) TIME | O ( 1 ) SPACE

# *Solution 2 :*

- [ ]  Done on my own

## Explanation :

## Code :

```python
def smallestDifference(arrayOne, arrayTwo):
	
	arrayOne.sort()
	arrayTwo.sort()
	
	i = 0
	j = 0
	
	smallest = float("inf")
	current = float("inf")
	
	pair = [0,0]
	
	while i<len(arrayOne) and j<len(arrayTwo):
		a = arrayOne[i]
		b = arrayTwo[j]
		
		if a < b :
			current = b - a
			i += 1
			
		elif b < a:
			current = a - b
			j += 1
			
		else:
			return [a,b]
		
		if current < smallest:
			smallest = current
			pair = [a,b]
			
	return pair
```

## Time Space Complexity :

O ( MLOG(M) + NLOG(N) ) TIME | O ( 1 ) SPACE

nlog(n) ⇒ merge sort