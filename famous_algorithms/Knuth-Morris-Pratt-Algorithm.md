# Problem Statement:

Knuth—Morris—Pratt Algorithm 

Write a function that takes in two strings and checks if the first string contains the second one using the Knuth—Morris—Pratt algorithm. The function should return a boolean. 

If you're unfamiliar with the Knuth—Morris—Pratt Algorithm, we recommend watching the Conceptual Overview section of this question's video explanation before starting to code.

## Sample Input

```cpp
string = "aefoaefcdaefcdaed"
substring = "aefcdaed"
```

## Sample Output

```cpp
True
```

# *Solution 1 :*

- [x]  Done on my own

## Explanation :

STUPID NAIVE SOLUTION [ not the algorithm ]

## Code :

```cpp
def knuthMorrisPrattAlgorithm(string, substring):
    count = 0
	found = False
	
	for i in range(len(string)):
		
		for j in range(len(substring)):
			# first pointer on string
			first = i
			# second pointer on substring
			second = 0
			
			# while both are equal increment count
			while string[first] == substring[second]:
				
				count+=1
				if count == len(substring):
					found = True
					break
					
				second+=1
				first+=1
				
				if second >= len(substring) or first>=len(string):
					break
					
			# reset if not found		
			count=0
			
		
	return found
```

## Time Space Complexity :

 O ( M * N ) Time | O ( 1 ) Space

M —> Length of Substring

N —>  Length of String

# *Solution 2 :*

- [ ]  Done on my own

## Explanation :

The Real Algorithm [ CLEMENT INDEX 0 BASED ] 

## Code :

```cpp
def knuthMorrisPrattAlgorithm(string, substring):
    pattern = buildPattern(substring)
	return doesMatch(string,substring,pattern)

def doesMatch(string,substring,pattern):
	
	i = 0
	j = 0
	
	while i < len(string) and j<len(substring):
		
		if string[i] == substring[j]:
			if j==len(substring)-1:
				return True
			i+=1
			j+=1
			
		elif j > 0:
			j = pattern[j-1] + 1
			
		else:
			i+=1
	
	return (j==(len(substring)-1))

def buildPattern(substring):
	pattern = [-1 for _ in range(len(substring))]
	
	j=0
	i=1
	
	while i < len(substring):
		
		if substring[j] == substring[i]:
			pattern[i] = j
			i+=1
			j+=1
		
		elif j > 0:
			j = pattern[j - 1] + 1
			
		else:
			i+=1
	
	return pattern
```

## Time Space Complexity :

O ( M + N ) Time | O ( N ) Space

# *Solution 3 :*

- [ ]  Done on my own

## Explanation :

ABDUL BARI [ INDEX 1 BASED ]

Both solutions have some logic, just way of application is different.

This solution is easier to understand.

[9.1 Knuth-Morris-Pratt KMP String Matching Algorithm](https://www.youtube.com/watch?v=V5-7GzOfADQ)

## Code :

```cpp
# follows Abdul Bari method ( index 1 based ) [clement uses index 0 based ]
def knuthMorrisPrattAlgorithm(string, substring):
	# takes O ( M ) Time where M is len(substring)
    pattern , substring = buildPattern(substring)
	# takes O ( N ) Time where N is len(string)
		return doesItContain(substring,string,pattern)
	# total O ( M + N )

def doesItContain(substring,string,pattern):
	
	i = 0
	j = 0
	
	while i < len(string):
		
		if string[i] == substring[j+1]:
			i+=1
			j+=1
			# since j + 1 will not go out of the substring
			# and we have reached the end, return True
			if j == len(substring) - 1:
				return True
			
		elif j > 0:
				j = pattern[j]
			
		else:
			i+=1
		
	return False	
	
def buildPattern(substring):
	
	# these 2 steps are necessary to make all of it INDEX 1 BASED
	# which means if it points to zero, no prev pattern 
	# and index zero is empty deliberately
	substring = " " + substring
	pattern = [0 for _ in range(len(substring))]
	
	# j will start from 1 , since 0th position is nothing
	# idea behind 0th position is similar to starting from index 1
	# when you need to compare all left elements, but here you have
	# to compare all the right elements of the substring with current
	# letter in big string
	j = 1
	i = 2
	
	while i < len(substring):
		
		if substring[j] == substring[i]:
			pattern[i] = j
			i+=1
			j+=1
		
		elif j > 1:
			j = pattern[j - 1] + 1
			
		else:
			i+=1
			
	return [pattern , substring]
```

## Time Space Complexity :

O ( M + N ) Time | O ( N ) Space