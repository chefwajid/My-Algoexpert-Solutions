# *Problem Statement :*

Write a function that takes in a big string and an array of small strings, all of which are smaller in length than the big string. 

The function should retum an array of booleans, where each boolean represents whether the small string at that index in the array of small strings is contained in the big string. 

Note that you can't use language-built-in string-matching methods.

## Sample Input

```cpp
bigString = "this is a big string"
smallStrings = ["this", "yo", "is", "a", "bigger", "string", "kappa"]
```

## Sample Output

```cpp
[true, false, true, true, false, true, false]
```

# *Solution 1 :*

## Explanation :

## Code :

```python
def multiStringSearch(bigString, smallStrings):
    trie = Trie()
	result = []
	words = bigString.split(" ")
	# for every word
	for i in words:
		# add every prefix
		for j in range(1,len(i)+1):
			trie.insert(trie.root,i[:j])
		# add every suffix
		for j in range(len(i)):
			trie.insert(trie.root,i[j:])
			
	for i in smallStrings:
		# search for every string given and store result
		result.append(trie.search(trie.root,i))
		
	return result

class Node:
    def __init__(self, value):
        self.value = value
        self.doesWordEndHere = False
        self.children = [None for _ in range(100)]

class Trie:
    def __init__(self):
        self.root = Node("/")

    def getIndex(self, character):
        if character.isnumeric():
            return ord(character) - ord("0") + 52
        elif character.isupper():
            return ord(character) - ord("A") + 26
        elif character.islower():
            return ord(character) - ord("a")
        else:
            print(character)
            return ord(character) % 38 + 62

    def insert(self, node, word):
        index = self.getIndex(word[0])
        child = node.children[index]
        if child is None:
            child = Node(word[0])
            node.children[index] = child

        if len(word) == 1:
            if not child.doesWordEndHere:
                child.doesWordEndHere = True
                node.children[index] = child
                return True
            else:
                return False

        return self.insert(child, word[1:])

    def search(self, node, word):
        index = self.getIndex(word[0])
        child = node.children[index]
        if child is None:
            return False

        if len(word) == 1:
            if child.doesWordEndHere:
                return True
            else:
                return False

        return self.search(child, word[1:])

    def delete(self, node, word):
        index = self.getIndex(word[0])
        child = node.children[index]
        if child is None:
            return False

        if len(word) == 1:
            if child.doesWordEndHere:
                child.doesWordEndHere = False
                return True
            else:
                return False

        return self.delete(child, word[1:])
       

```

## Optimal Time Space Complexity :

# *Solution  :*

## Explanation :

Clement Solution

## Code :

```cpp
#   Solution 02
#   O(b^2 + ns) time | O(b^2 + n) space
def multiStringSearch(bigString, smallStrings):
    modifiedSuffixTrie = ModifiedSuffixTrie(bigString)
    return [modifiedSuffixTrie.conntains(string) for string in smallStrings]

class ModifiedSuffixTrie:
    def __init__(self, string):
        self.root = {}
        self.populateModifiedSuffixTrieFrom(string)

    def populateModifiedSuffixTrieFrom(self, string):
        for i in range(len(string)):
            self.insertSubstringStartinngAt(i, string)

    def insertSubstringStartinngAt(self, idx, string):
        node = self.root
        for j in range(idx, len(string)):
            letter = string[j]
            if letter not in node:
                node[letter] = {}
            node = node[letter]

    def conntains(self, string):
        node = self.root
        for letter in string:
            if letter not in node:
                return False
            node = node[letter]
        return True

#   Solution 03
#   O(bs + ns) time | O(ns) space
def multiStringSearch(bigString, smallStrings):
    trie = Trie()
    for string in smallStrings:
        trie.insert(string)
    containedString = {}
    for i in range(len(bigString)):
        findSmallStringsIn(bigString, i, trie, containedString)
    return [string in containedString for string in smallStrings]

def findSmallStringsIn(string, startIdx, trie, containedStringns):
    currentNode = trie.root
    for i in range(startIdx, len(string)):
        currentChar = string[i]
        if currentChar not in currentNode:
            break
        currentNode = currentNode[currentChar]
        if trie.endSymbol in currentNode:
            containedStringns[currentNode[trie.endSymbol]] = True

class Trie:
    def __init__(self):
        self.root = {}
        self.endSymbol = '*'

    def insert(self, string):
        current = self.root
        for i in range(len(string)):
            if string[i] not in current:
                current[string[i]] = {}
            current = current[string[i]]
        current[self.endSymbol] = string
```

## Time Space Complexity :

O(ns + bs) time | O(ns) space - where n is the number of small strings, s is the length of longest small string, and b is the length of the big string