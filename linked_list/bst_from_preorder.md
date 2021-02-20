## Question:

Given preorder traversal of a binary search tree, construct the BST.

[Construct BST from given preorder traversal | Set 1 - GeeksforGeeks](https://www.geeksforgeeks.org/construct-bst-from-given-preorder-traversa/)

```python
class Node():
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

class BST():
    def __init__(self):
        self.root = None
        self.first = None
    
    def insert(self, data):
        temp = Node(data)
        if self.root == None:
            self.root = temp
        
        else:
            curr = self.root
            while True:
                if data < curr.data:
                    if curr.left == None:
                        curr.left = temp
                        break
                    else:
                        curr = curr.left
                
                elif data > curr.data:
                    if curr.right == None:
                        curr.right = temp
                        break
                    else:
                        curr = curr.right
                else:
                    pass
    
    def inorder(self, curr):
        if curr:
            self.inorder(curr.left)
            print(curr.data)
            self.inorder(curr.right)
            
    def preorder(self, curr, preOrder_nums):
        if curr:
            preOrder_nums.append(curr.data)
            self.preorder(curr.left, preOrder_nums)
            self.preorder(curr.right, preOrder_nums)
        return preOrder_nums    
     

    def bst_from_preorder(self, data):
        self.first = self.create_bst_from_preOrder(self.first, data)
    
    def create_bst_from_preOrder(self, root, data):
        if root == None:
            root = Node(data)
        
        else:
            if root.data < data:
                root.right = self.create_bst_from_preOrder(root.right, data)
            elif root.data > data:
                root.left = self.create_bst_from_preOrder(root.left, data)
            else:
                pass
        return root    
                
        

bst = BST()
#10, 5, 1, 7, 40, 50
bst.insert(10)
bst.insert(5)
bst.insert(1)
bst.insert(7)
bst.insert(40)
bst.insert(50)

preOrder_nums = list()
preOrder_nums = bst.preorder(bst.root, preOrder_nums)
print(preOrder_nums)

bst_2 = BST()

for i in range(len(preOrder_nums)):
    bst_2.bst_from_preorder(preOrder_nums[i])

bst_2.inorder(bst_2.first)
```

Time complexity of the algorithm is O(n) and space complexity is O(n)