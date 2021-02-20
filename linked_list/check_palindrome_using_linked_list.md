## Question:

Given a singly linked list of characters, write a function that returns true if the given list is a palindrome, else false.

[Function to check if a singly linked list is palindrome - GeeksforGeeks](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)

```python
class Node:
    def __init__(self, data=None):
        self.data = data
        self.next = None
    
class LinkedList():
    def __init__(self):
        super().__init__
        self.first = None    

    def insert(self, data):
        temp = Node()
        temp.data = data
        temp.next = None

        if self.first == None:
            self.first = temp    
        else:
            curr = self.first
            while curr.next != None:
                curr = curr.next

            curr.next = temp
            curr = temp

    def display(self):
        if self.first != None:
            curr = self.first
            while curr != None:
                print(curr.data, end=" ");
                curr = curr.next
        else:
            raise Exception("Empty linked list") 

    def length(self):
        l_length = 0

        curr = self.first
        while curr != None:
            l_length += 1
            curr = curr.next

        return l_length
## first approach is to reverse the linked list and check the reverse one with original 
def reverse_ll(ll: LinkedList):
    prev = None
    curr = ll.first

    while curr != None:
        next_ = curr.next
        curr.next = prev
        prev = curr
        curr = next_

    return prev   

def palindrome(ll_1: Node, ll_2: Node):
    if ll_1 != None and ll_2 != None:
        while ll_1 != None and ll_2 != None:
            if ll_1.data != ll_2.data:
                return False
            ll_1 = ll_1.next
            ll_2 = ll_2.next    

        return True  

    raise Exception("Both the linked should be non-empty")
## the second apprach is good were with the help of stack we are checking if the linked list is palindrome or not
def stackPalindrome(ll: LinkedList):
    stack = []
    curr = ll.first

    ispalin = False

    while curr != None:
        stack.append(curr.data)
        curr = curr.next

    curr = ll.first

    while curr != None:
        i = stack.pop()
        if curr.data == i:
            is_palin = True
        else:
            is_palin = False
            break

        curr = curr.next

    return is_palin              

ll = LinkedList()
ll.insert(1)            
ll.insert(1)            
ll.insert(2)            
ll.insert(1)            
#ll_2 = reverse_ll(ll)

#print(palindrome(ll.first, ll_2))
print(stackPalindrome(ll))
```

Time complexity of the algorithm is O(n) and space complexity is O(n)