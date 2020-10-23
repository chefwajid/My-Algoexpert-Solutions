# *Problem Statement :*

Write a function that takes in an array of integers and returns the length of the longest peak in the array. 

A peak is defined as adjacent integers in the array that are strictly increasing until they reach a tip (the highest value in the peak), at which point they become strictly decreasing. 

At least three integers are required to form a peak. 

For example, the integers 1, 4, 10, 2 forma peak. buttheintegers 4, e, 10 don't and neither do the integers 1, 2, 2, e . Similarly, the integers 1, 2, 3 don't forma peak because there aren't any strictly decreasing integers after the 3 .

## Sample Input

```cpp
array = [1, 2, 3, 3, 4, 0, 10, 6, 5, -1, -3, 2, 3]
```

## Sample Output

```cpp
6
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
def longestPeak(array):
	
	peakIndices = findPeaks(array)
	return longest(peakIndices,array)

# break into functions for modular and readable code

def longest(peakIndices,array):
	
	maxPeakLength = 0
	
	# spread from the peak in both directions
	for peak in peakIndices:
		peakLength = 1
		
		index = peak
		while index < len(array)-1 and array[index] > array[index+1]:
			peakLength += 1
			index += 1
			
		index = peak
		while index > 0 and array[index] > array[index-1]:
			peakLength += 1
			index -= 1
			
		maxPeakLength = max(peakLength,maxPeakLength)
		
	return maxPeakLength

def findPeaks(array):
	
	peaks = []
	for i in range(1,len(array)-1):
		
		if array[i-1] < array[i] > array[i+1]:
			peaks.append(i)
			
	return peaks
```

## Optimal Time Space Complexity :

O ( N ) TIME | O ( 1 ) SPACE