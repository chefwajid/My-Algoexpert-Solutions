# *Problem Statement :*

There are *N* children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

What is the minimum candies you must give?

**Leetcode Solution section and Algoexpert Video have great explanations. Also present in record book.**

## Sample Input

```cpp
Input: [1,0,2]
```

## Sample Output

```cpp
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
```

# *Solution 1 :*

Double Pass [ Most elegant ]

## Explanation :

In the first traversal we only focus on the LEFT & CURRENT STUDENT relationship.

- If current student has more marks (compared to left), give it (left + 1) rewards
- If left has more marks, ignore. [It will be dealt in next iteration]

In the Second traversal we only focus on the RIGHT & CURRENT STUDENT relationship

- If current student has more marks (compared to right),

    GIVE IT MAX OF ( RIGHT+1 , EXISITING VALUE )

    Now why max ? because if a Hill / positive slope is already formed, then changing it to something

    minimum would disturb every other element after it and it wont be obeying the conditions. 

    The condition is STRICTLY GREATER than adjacent if score is higher, 

    Ex : [ 5,6,7,8,9,4 ] ⇒ [ 1,2,3,4,5,1 ]  { we dont disturb the 12345 hill here in the 2nd pass}

## Code :

```cpp
def minRewards(scores):
    
	# Distribute 1 reward for all, since its the minimum
	result = [1 for _ in range(len(scores))]
    
	# Checking the element on the LEFT in this iteration
	for i in range(1,len(scores)):
		
		if scores[i] > scores[i-1]:
			result[i]  = result[i-1] + 1
			
	# Checking the element on the RIGHT in this iteration
	# MAX needed to maintain peak/bottom ratio according to condition
	for i in range(len(scores)-1,0,-1):
		
		if scores[i-1] > scores[i]:
			result[i-1] = max(result[i-1],result[i]+1)
			
	return sum(result)
```

A more well-written elegant solution with same logic

```python
def minRewards(scores):
    
	# 1 reward for everyone
	rewards = [1 for _ in range(len(scores))]
	
	# for every student on your left
	for i in range(1,len(scores)):
		currentStudent = i
		previousStudent = i-1
		currentStudentScore = scores[currentStudent]
		previousStudentScore = scores[previousStudent]
		
		if  currentStudentScore > previousStudentScore :
			rewards[currentStudent] = rewards[previousStudent] + 1
			
	
	# for every student on your right
	for i in reversed(range(len(scores)-1)):
		currentStudent = i
		previousStudent = i+1
		currentStudentScore = scores[currentStudent]
		previousStudentScore = scores[previousStudent]
		
		if  currentStudentScore > previousStudentScore :
			currentReward = rewards[previousStudent] + 1
			rewards[currentStudent] = max( rewards[currentStudent] , currentReward )
	
	return sum(rewards)
```

## Optimal Time Space Complexity :

O(2n) Time and O(n) Space

# *Solution 2 :*

## Explanation :

ALGORITHM NAIVE APPROACH

- IF CURRENT STUDENT SCORE > LEFT STUDENT:
    - CURRENT STUDENT = LEFT STUDENT SCORE + 1
- IF LEFT STUDENT SCORE > CURRENT STUDENT SCORE
    - BACKTRACK AND INCREMENT ALL OTHER STUDENT REWARDS WHERE LEFT > CURRENT
    - LEFT STUDENT = MAX ( CURRENT VALUE , RIGHT STUDENT + 1 )

## Code :

```cpp
class Solution(object):
    def candy(self, scores):
        
        result = [1 for _ in range(len(scores))]
        
        for currStudent in range(1,len(scores)):
            
            leftStudent = currStudent-1
            
            if scores[currStudent] > scores[leftStudent]:
                
                result[currStudent] = result[leftStudent] + 1
                
            else:
                
                # backtrack and fix the slope
                while leftStudent>=0 and scores[leftStudent] > scores[leftStudent+1]:
                    
                    result[leftStudent] = max(result[leftStudent],result[leftStudent+1] + 1)
                    
                    leftStudent-=1
                    
                    
        return sum(result)
```

## Optimal Time Space Complexity :

O ( N^2 ) TIME | O ( N ) SPACE

# *Solution 3 :*

## Explanation :

Idea is to traverse the array and find the local minimums. Then EXPAND ( in both directions ) from the local mins and keep increasing values (using the max trick as to not disturb higher values) until you either the hit the end of the array OR you come out of an increasing trend ( i.e  current element is not greater than previous ). If the increasing trend is over, it means you are in the territory of another local minimum so stop.

## Code :

```cpp
Code available in algoexpert solutions. too lazy to right the code.
```

## Optimal Time Space Complexity :

O(n) Time and Space

# *Solution 4:*

SINGLE PASS APPROACH 

## Explanation :

Idea is to determine length of left and right side of mountain. The peak element becomes the max of both + 1. Now the left side sum is calculated using the series formula of n(n-1)/2 and right side also the same way. In the end all three of these are added. This is repeated for all mountains.

## Code :

```cpp
public int candy(int[] ratings) {
    if(ratings==null || ratings.length==0) return 0;
    int start=0,sum=0,len=ratings.length;

    while(start<len) {

			// if element is equal just give 1
    	if(start+1<len && ratings[start]==ratings[start+1]) {
    		sum+=1;
    		start++;
    		continue;
    	}
			
			// Starting new mountain
    	int left=0,right=0;

      //left means the left part of the mountain,right means the right part of the mountain
			// GOING UP UP UP
    	while(start+1<len && ratings[start]<ratings[start+1]) {
    		start++;
    		left++;
    	}
			// GOING DOWN DOWN DOWN
    	while(start+1<len && ratings[start]>ratings[start+1]) {
    		start++;
    		right++;
    	}
    	if(left==0 && right==0) {
    		sum+=1;
    		break;
    	}
    	int max=Math.max(left, right)+1;
    	int leftSum=(1+left)*left/2;
    	int rightSum=(1+right)*right/2-1;

			//ADD ALL THREE
    	sum+=max+leftSum+rightSum;
    }
    return sum;
}
```

## Optimal Time Space Complexity :

O(n) Time and  O(1) Space

# *Solution 5 :*

## Explanation :

MY NAIVE 121 LINE CODE , FIRST ATTEMPT STRUGGLING CODE WHERE I ACTUALLY SOLVED IT FOR DISTINCT ELEMENTS.

Written here just to remind myself how stupid i was.

Anyway idea was to find Bottoms/Crests and expand till the peaks.

## Code :

```cpp
def minRewards(scores):
    
	# index : isPeak
	results = {}
	visited  = [0 for _ in range(len(scores))]
	
	increasing  = 0
	decreasing = 0
	
	for i in range(1,len(scores)-1):
		
		if  scores[i-1] < scores[i] > scores[i+1]:
			
			results[i] = True
			continue
			
		elif scores[i-1] > scores[i] < scores[i+1]:
			
			results[i] = False
			continue
	increasing = all(i < j for i, j in zip(scores, scores[1:]))
	decreasing = all(i > j for i, j in zip(scores, scores[1:]))

	
	resultList = [0 for _ in range(len(scores))]
	
	# not peak or crest
	if increasing or decreasing or len(scores)==1:
		print("list is either strictly increasing or decreasing")
		for i in range(0,len(scores)):
			resultList[i] = (len(scores) - i) if decreasing else i+1
			print(resultList[i])
		return sum(resultList)
			
	peaksAndCrests = list(sorted(results.keys()))
	
	for i in range(len(peaksAndCrests)-1):
		
		currentValue = peaksAndCrests[i]
		currentState =  results[peaksAndCrests[i]]
		nextValue = None if len(peaksAndCrests)<i+1 else peaksAndCrests[i+1] 
		nextState = not results[currentValue]
		print(currentState)
		print(currentValue)
		if not currentState:
			resultList[currentValue] = 1
	if not results[peaksAndCrests[-1]]:
		resultList[peaksAndCrests[-1]] = 1
		
		
		
	print(peaksAndCrests)
	
	print(results)
	
	# ok so we're expanding from crests for now
	for index,isPeak in results.items():
		if not isPeak:
			curr = index-1
			count = 2
			# expandleft
			while(curr>=0):
				isPeak = results.get(curr,None)
				condition = visited[curr]
				if condition == 0 or isPeak:
					visited[curr] = 1
					prev = resultList[curr] 
					resultList[curr]+=count
					count += 1
					
					if isPeak is not None:
						resultList[curr] = max(prev,count-1)
						break
					curr -=1

				else:
					break
			# expandRight
			curr = index+1
			count = 2
			while(curr<len(scores)):
				condition = visited[curr]
				if condition == 0:
					visited[curr] = 1
					resultList[curr]+=count
					count+=1
					
					isPeak = results.get(curr,None)
					if isPeak is not None:
						break
					curr+=1
				else:
					break
				
	# fill in the blanks from sides
	last = max(peaksAndCrests)
	isLastPeak = results[last]
	lastPeak = resultList[last]
	first = min(peaksAndCrests)
	isFirstPeak = results[first]
	firstPeak = resultList[first]
	
	last+=1
	first-=1
	
	while(last < len(scores)):
		if isLastPeak and visited[last]==0:
			resultList[last] = len(scores) - last
			last+=1
		else:
			break
	countv = 1
	while(first >= 0):
		if isFirstPeak and visited[first]==0:
			resultList[first] = countv
			countv+=1
			first-=1
		else:
			break
			
	return sum(resultList)
```

## Optimal Time Space Complexity :

Dont even bother

[Candy - LeetCode](https://leetcode.com/problems/candy/solution/)