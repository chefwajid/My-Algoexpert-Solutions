# *Problem Statement :*

Kadane's Algorithm Write a function that takes in a non-empty array of integers and retums the maximum sum that can be obtained by summing up all of the integers in a non-empty subarray of the input array. A subarray must only contain adjacent numbers.

## Sample Input

```cpp
array = [3, 5, -9, 1, 3, -2, 3, 4, 7, 2, -9, 6, 3, 1, -5, 4]
```

## Sample Output

```cpp
19 // [1, 3, -2, 3, 4, 7, 2, -9, 6, 3, 1]
```

# *Solution 1 :*

## Explanation :

## Code :

```cpp
#include <vector>
using namespace std;

int kadanesAlgorithm(vector<int> array) {
  
	//Calculating the max sum till now
	int maxSumSoFar = array[0];
	//Keeping track of the max sum
	int maxNumSoFar = array[0];
	
	for(int i=1 ; i<array.size() ; i++)
	{
		int num = array[i];
		maxSumSoFar = max(num , maxSumSoFar + num);
		maxNumSoFar = max(maxNumSoFar , maxSumSoFar);
	}
	
  return maxNumSoFar;
}
```

## Optimal Time Space Complexity :