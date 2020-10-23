# Problem Statement:

 Write a function that takes in a non-empty array of distinct integers and an integer representing a target sum. 

The function should find all triplets in the array that sum up to the target sum and return a two- dimensional array of all these triplets. 

The numbers in each triplet should ordered in ascending order. and the triplets themselves should ordered in ascending order with to the they hold. 

If no three numbers sum up to the target sum, the function should return an empty array.

## Sample Input

```
array = [12, 3, 1, 2, -6, 5, -8, 6]
targetSum = 0
```

## Sample Output

```
[[-8, 2, 6], [-8, 3, 5], [-6, 1, 5]]
```

# *Solution 1 :*


## Explanation :

## Code :

```python
def threeNumberSum(array, targetSum):
	
	# Triplets to return
    nums = []
	
	# sort the array keeping the output format in mind
	array.sort()
	
	# three loops
	for i in range(len(array)):
		a = array[i]
		for j in range(i+1,len(array)):
			b = array[j]
			for k in range(j+1,len(array)):
				c = array[k]
				# check if the elements equal targetsum
				if a + b + c == targetSum:
					nums.append([a,b,c])
					
	return nums
```

## Time Space Complexity :

O ( N ^ 3 ) TIME | O ( N ) SPACE

# *Solution 2 :*


## Explanation :

## Code :

```cpp
def threeNumberSum(array, targetSum):
    
	# store all elements in a hashmap
	nums = {}
	for i in array:
		nums.setdefault(i,i)
	
	# list to store all triplets
	triplets = []
	
	for index,a in enumerate(array):
		for b in array[index+1:]:
			#l assume a + b + c = targetSum 
			#l => c =  targetSum - a + b 
			missingNum = targetSum - (a + b) 
			
			if nums.get(missingNum) is not None and missingNum != a and missingNum != b:
				triplet = [missingNum , a , b]
				# sorting is important to make sure same sets are not considered different
				# due to their arrangement
				triplet.sort()
				if triplet not in triplets:
					triplets.append(triplet)
				
	triplets.sort()			
	return triplets
```

## Time Space Complexity :

O ( N ^ 2 ) TIME | O ( N ) SPACE

# *Solution 3 :*

## Explanation :

## Code :

```cpp
def threeNumberSum(array, targetSum):
	
	# list to store triplets
	triplets = []
	
	# sort array for two pointer logic to work
	array.sort()
	
	for i in range(len(array)):
		
		start = i+1
		end = len(array) - 1
		
		while start < end :
			a = array[i]
			b = array[start]
			c = array[end]
			currentSum = a + b + c
			
			if currentSum == targetSum:
				triplet = [a,b,c]
				triplets.append([a,b,c])
				start+=1
				
			elif currentSum < targetSum:
				start += 1
				
			elif currentSum > targetSum:
				end -= 1
				
	return triplets
```

## Time Space Complexity :

O ( N ^ 2 ) TIME | O ( N ) SPACE