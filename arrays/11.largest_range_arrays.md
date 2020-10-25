# *Problem Statement :*

Write a function that takes in an array of integers and returns an array of length 2 representing the largest range of integers contained in that array. 

The first number in the output array should be the first number in the range, while the second number should the last number in the range. 

A range of numbers is defined as a set of numbers that come right after each other in the set of real integers. For instance. theoutputarray [2, 6] represents the range {2, 3, 4, 5, 6} , which isa range of length 5. 

Note that numbers don't need to sorted or adjacent in the input array in order to form a range. You can assume that there will only one largest range.

## Sample Input

```cpp
array = [1, 11, 3, 0, 15, 5, 2, 4, 10, 7, 12, 6]
```

## Sample Output

```cpp
[0, 7]
```

# *Solution 1 :*

## Explanation :

The idea is to perform two traversals.

- First Traversal

    → Find the minimum and maximum element

    → Store all elements in a hashtable

- Second Traversal

    → initialize a pair with [ minNumber , maxNumber ]

    → Traverse from MinNumber —> MaxNumber and keep updating the rightNumber

    → if number not found at any point, update leftIndex to i+1

    → at the end of every check update pair if count > maxCount of range elements

## Code :

```cpp
def largestRange(array):
	
	minNumber = float("inf")
	maxNumber = float("-inf")
	numbers = {}
	
	for i in array:
		numbers.update({i:i})
		minNumber = min(minNumber,i)
		maxNumber = max(maxNumber,i)
		
	leftNumber = minNumber
	rightNumber = leftNumber
	count = 0
	maxCount = 0
	pair = [minNumber,maxNumber]
				 
	for i in range(minNumber,maxNumber+1):
		
		if numbers.get(i) is None:
			leftNumber = i+1
			count = 0
			
		else:
			count += 1
			rightNumber = i
			maxCount = max(count,maxCount)
			
		if count >= maxCount:
				pair = [ leftNumber , rightNumber ]	
	
				 
	return pair
```

## Optimal Time Space Complexity :

O ( N ) TIME | O ( N ) SPACE