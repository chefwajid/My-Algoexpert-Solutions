# Problem Statement:

Write a function that takes in an array of integers and returns a boolean representing whether the array is monotonic. 

An array is said to be monotonic if its elements. from left to right are entirely non-increasing or entirely non-decreasing. 

Non-increasing elements aren't necessarily exclusively decreasing they simply don't increase. Similarly, non-decreasing elements aren't necessarily exclusively increasing they simply don't decrease. Note that empty arrays and arrays of one element are monotonic.

## Sample Input

```cpp
array = [-1, -5, -10, -1100, -1100, -1101, -1102, -9001]
```

## Sample Output

```python
True
```

# *Solution 1 :*

- [x]  Done on my own

## Explanation :

## Code :

```cpp
def isMonotonic(array):
    
	if len(array) <= 1:
		return True
	
	increasing = 0
	decreasing = 0
	equal = 0
	
	for i in range(len(array)-1):
		
		if array[i] < array[i+1]:
			increasing += 1
		elif array[i] > array[i+1]: 
			decreasing +=1
		else:
			equal += 1
			
	# if all equal
	if equal == len(array)-1:
		return True
	
	elif increasing + equal == len(array)-1:
		return True
	
	elif decreasing + equal == len(array)-1:
		return True
	
	else:
		return False
```

## Time Space Complexity :

O ( N ) TIME |  O ( 1 ) SPACE