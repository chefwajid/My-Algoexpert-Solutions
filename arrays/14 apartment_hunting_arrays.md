# Problem Statement:

You're looking to move into a new apartment on specific street and you're given a list of contiguous blocks on that street where each block contains an apartment that you could move into.

You also have a list of requirernents: a list of buildings that are important to you. For instance. you might value having a and a gym near your apartrnent. The list of blocks that you have contains information at every block about all of the buildings that are present and absent at the block in question. 

For instance. for every block ymJ might know whether a school. a pool. an office. and a gym are present. In order to optimize your life. 

you want to pick an apartment block such that you minimize the farthest distance you'd have to walk from your aparment to reach any of your required buildings. 

Write a function that takes in a list of contiguous blocks on a specific street and a list of your required buildings and that returns the location (the index) of the blcxk that's most optimal for you. 

If there are multiple most optimal blocks. your function can return the index of any one of them.

blocks ⇒ colony

requirement ⇒ Services you want

**Input 1 :** A HashTable is given to you containing 

- All Blocks
    - Each Block contains whether or not a service is available

**Input 2 :** 

- List of requirements you care about

## Sample Input

```cpp
blocks = [ 
{ “gym” : true, “school” : true, “store” : false } ,
{ “gym” : true, “school” : true, “store” : false } ,
{ “gym” : true, “school” : true, “store” : false } ,
{ “gym” : true, “school” : true, “store” : false } ,
{ “gym” : true, “school” : true, “store” : false } 
]

requirements = [ “gym”, “school”, “store” ]
```

## Sample Output

```cpp
3 // at index 3, the farthest you'd have to walk to reach a gym, a school, or a store is 1 block; at any other index, you'd have to walk farther
```

# *Solution 1 :*

- [x]  Done on my own with small hint from clement

## Explanation :

Naive approach

3 for loops

- for every requirement ( repeat for every requirement )
    - for every block ( to fill its data )
        - search every other block ( to calculate relative distance, to block in above loop )

            check for min distance at each block

        **once min distance found, store it in distanceArray if it is greater than current element distance in that index,** VERY IMPORTANT STEP, i thought of taking the sum then choosing the minimum but we want to spend minimum energy for all three not over all.

        let me explain, consider

        gym : 1

        store : 0              

        school : 1

        AND

        gym : 0

        store : 0              

        school : 2

        Now, if you add all of them, that will be 2 but you have to choose the above one, since 

        everything is closer OVERALL, so SUM WILL NOT WORK, i was stuck here and clement suggested taking the MAX ELEMENT from all 3 and storing that in the distance array.

In the end we return the index of the minimum element in the Distance Array.

**TLDR** : store the max distance to any requirement in the Distance array and return the minimum !

## Code :

```cpp
import sys
from collections import defaultdict
def apartmentHunting(blocks, reqs):

	distanceArr = [0 for x in range(len(blocks))]

	for requirement in reqs:

		for blockIndex,block in enumerate(blocks):

			minimumDistance = sys.maxsize
			for otherBlockIndex,otherBlock in enumerate(blocks):

				if otherBlock[requirement] == True:
					minimumDistance = min(minimumDistance,abs(otherBlockIndex - blockIndex))

			distanceArr[blockIndex] =  max(distanceArr[blockIndex] ,minimumDistance) 
	
	minBlock = distanceArr.index(min(distanceArr))
	
	return minBlock
```

## Time Space Complexity :

O ( B^2 R ) Time and O ( B ) Space

B for Blocks and R for Requirement

# *Solution 2 :*

- [ ]  Done on my own

## Explanation :

How can we decrease the complexity ? think.. since previous time complexity is O ( B R^2 )

if we can implement a solution inside the O ( B R ) limit, that would be great.

(a) ⇒ All we need is an array for each requirement that tells us how far that requirement is, from each index.

Rest of the job is simple, store the max of all values at a particular index in the distance Array and return the index of the minimum element.

To implement (a) we will use the two traversal technique used in [Min Rewards [ local min/max ]](https://www.notion.so/Min-Rewards-local-min-max-c238499f8eb64797b856ccc22ed1ca66). Really awesome implementation.

Traversal 1 ⇒ Left to right , Check elements on left

- If gym in block, distance = 0
- if gym in prev block distance = 1
- if last element in the array is not None, currentDist = prevDist + 1

Traversal 2 ⇒ Right to left, check element on right

- If gym in block, distance = 0
- if gym in prev block distance = 1
- if last element in the array is not None, **currentDist = min(currentDist,prevDist + 1) MINIMUM IMPORTANT**

## Code :

```cpp
import sys
def apartmentHunting(blocks, reqs):
	
	requirements = {}
	
	for i in reqs:
		requirements.setdefault(i,[None for x in range(len(blocks))])
		
	# left to right traversal
	for i in range(1,len(blocks)):
		
		for requirement in reqs:
			
			# does the current block have the requirement?
			if blocks[i][requirement] == True:
				requirements[requirement][i] = 0
				continue
			elif blocks[i-1][requirement] == True:
				requirements[requirement][i] = 1
				continue
			elif requirements[requirement][i-1] != None:
				requirements[requirement][i] = requirements[requirement][i-1] + 1
				
	# right to left traversal
	for i in range(len(blocks)-2,-1,-1):
		
		for requirement in reqs:
			
			# does the current block have the requirement?
			if blocks[i][requirement] == True:
				requirements[requirement][i] = 0
				continue
			elif blocks[i+1][requirement] == True:
				requirements[requirement][i] = 1
				continue
			elif requirements[requirement][i+1] != None:
				if requirements[requirement][i] == None:
					requirements[requirement][i] = sys.maxsize
				requirements[requirement][i] = min(requirements[requirement][i],requirements[requirement][i+1] + 1)
				
	maxDist = [-1 for x in range(len(blocks))]
	
	for requirement,distance in requirements.items():
		
		for index,element in enumerate(distance):
			
			maxDist[index] = max(maxDist[index],element) 
	
	return maxDist.index(min(maxDist))
```

## Time Space Complexity :

O ( B R ) TIME AND O ( B ) SPACE