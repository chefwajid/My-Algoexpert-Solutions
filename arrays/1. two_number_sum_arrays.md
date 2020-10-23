# *Problem Statement :*

**1. Two Sum**

**Easy**

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have ***exactly*** one solution, and you may not use the *same* element twice.

## Sample Input

```
Given nums = [2, 7, 11, 15], target = 9,
```

## Sample Output

```
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

# *Solution 1 :*

- [x]  Got it on my own

## Explanation :

- Check sum of every possible pair in the array

Obviously brute force , O (n^2) { got this on my own }

My mistake was double checking all elements in nested for loop , instead i should have had a bubble sort type nested for loop.

WRONG ONE:

(COVERS ALL ELEMENTS TWICE SO A+B AND B+A BOTH COME DUE TO WHICH DUPLICATES ARISE)

for(int i = 0 ; i < n ; i++)
for(int j = 0 ; j < n ; j++)

CORRECT ONE:

(COVERS ALL ELEMENTS ONCE , [A+B ONLY NO B+A AGAIN] )

for(int i = 0 ; i < n ; i++)
for(int j = i+1 ; i < n ; j++)

## Code :

```
//Brute Force solution
#include <vector>
using namespace std;

vector<int> twoNumberSum(vector<int> array, int targetSum) {
  // Write your code here.
	vector<int> elements;
	
	for(auto a : array)
	{
		for(auto b : array)
		{
			bool elementNotRepeated = find(elements.begin(),elements.end(),b) == elements.end() && b !=a;
			if(elementNotRepeated)
			{
				bool isAddingUp = (a + b == targetSum);
				if(isAddingUp)
				{
					elements.push_back(a);
					elements.push_back(b);
				}
			}
		}
	}
  return elements;
}
```

## Time Space Complexity : O(n^2) with O(1) space

# *Solution 2 :*


## Explanation :

- The famous Two pointer approach , similar approach used in Three/Four Sum problems
- List should be sorted ***
- Two pointers from either side ,

    —> INCREASING                             DECREASING <—

- The value on both the pointers need an equilibrium variable to come to a conclusion

For ex : Here both values of the pointers are compared with the Target Sum

## Code :

```
#include <vector>
using namespace std;

vector<int> twoNumberSum(vector<int> array, int targetSum) {
  // Write your code here.
	vector<int> elementsToReturn;
	
	sort(array.begin(),array.end());
	int start = 0;
	int end = array.size()-1;
	
		while(start < end)
		{
			int sum = array[start] + array[end];
			bool isAddingUp = sum == targetSum;
			if(isAddingUp)
			{
				elementsToReturn.push_back(array[start]);
				elementsToReturn.push_back(array[end]);
				start++;
				
			}
			else if(sum > targetSum)
			{
				end--;
			}
			else if(sum < targetSum)
			{
				//array[start] > 0 ? end-- : start++;
				start++;
			}
				
		}
	
  return elementsToReturn;
}
```

## Time Space Complexity : O(nlogn) with O(1) space

# *Solution 3 :*


## Explanation :

- Since A + B = TargetSum  —> B = TargetSum - A
- This way we simply check if there is a corresponding B for a particular A the pointer is pointing at.
    - IF NOT: FOUND:
        - Add in hashmap
    - IF FOUND:
        - Add to result vector or return the pair (depending on problem)

## Code :

```
#include <vector>
#include <unordered_set>
using namespace std;

vector<int> twoNumberSum(vector<int> array, int targetSum) {
  // Write your code here.
	unordered_set<int> nums;
	for(int i : array)
	{
		int expectedMatch = targetSum - i;
		bool isPresent = nums.find(expectedMatch)!=nums.end();
		
		//Used to count occurrance of element generally, but 
		//since for unordered_set no duplicates are allowed it functions as find 
		//bool isPresent = nums.count(expectedMatch)!=0; 
		
		if(isPresent)
		{
			
			return vector<int>{expectedMatch,i};
			
		}else
		{
			nums.insert(i);
		}
	}
  return {};
}
```

## Time Space Complexity : O(n) with O(n) space

HashMaps reduce TimeComplexity in many cases from brute force since it gives the ability of remembering past values to a program