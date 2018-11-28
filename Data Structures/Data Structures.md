
# Basic Data Structures in Python 3

- Todo: Add time complexities for all the structures
- Todo: Implement graphs + some graph algos (Djikstras etc.)
- Todo: Implement Queues


## 1. Linked Lists

- Store data
- Successive elements are connected by pointers
- Last element points to NULL
- Can grow or shrink in size (hehe)
- Cool cause they can dynamically resize + efficient to insert/delete. BUT, shitty as far as search goes.
- Not stored in contiguous memory like arrays :( 


Time complexities:

- Insert: O(1)
- Deletion: O(1)
- Indexing O(n)
- Searching: O(n)

### 1.1 Singly Linked List


```python
class Node(object):
    def __init__(self, data, next_node=None):
        self.data = data;
        self.next_node = next_node;
    
    def set_data(self, data):
        self.data = data
        
    def set_next(self, next_node):
        self.next_node = next_node
        
    def get_next(self):
        return self.next_node

class LinkedList(object):
    def __init__(self):
        self.head = None
        
    def insert_at_start(self, data):
        new_node = Node(data)
        if self.head is not None:
            new_node.next_node = self.head
        self.head = new_node
        
    def delete(self, data):
        temp = self.head
        if temp.next_node is not None:
            if temp.data == data:
                self.head = temp.next_node
                temp = None
                return
            else:
                while temp.next_node is not None:
                    if temp.data == data:
                        break
                    prev = temp
                    temp = temp.next_node
                if temp == None:
                    return
                
                prev.next_node = temp.next_node
                return
            
    def search(self, node, data):
        if node == None:
            return False
        if node.data == true:
            return True
        self.search(node.get_next(), data)
        
    def print_list(self):
        temp = self.head
        while(temp):
            print(temp.data, end=' ')
            temp = temp.next_node
```


```python
my_list = LinkedList()
my_list.head = Node(1)
node_2 = Node(2)

my_list.head.set_next(node_2)

node_3 = Node(3)
node_2.set_next(node_3)

my_list.insert_at_start(5)

my_list.print_list()
```

    5 1 2 3 

### 1.2. Doubly Linked List


```python
class Node(object):
    def __init__(self, data, next_node=None, previous_node=None):
        self.data = data;
        self.next_node = next_node;
        self.previous_node = previous_node
    
    def set_data(self, data):
        self.data = data
        
    def set_next(self, next_node):
        self.next_node = next_node
        
    def get_next(self):
        return self.next_node
    
    def set_previous(self, previous_node):
        self.previous_node = previous_node

    def get_previous(self):
        return self.previous_node

class DoublyLinkedList(object):
    def __init__(self):
        self.head = None
        
    def insert_at_start(self, data):
        new_node = Node(data)
        if self.head == None:
            self.head = new_node
        else:
            self.head.previous_node = new_node
            new_node.next_node = self.head
            self.head = new_node
    
    def insert_at_end(self, data):
        new_node = Node(data)
        temp = self.head
        while temp.next_node != None:
            temp = temp.next_node
        temp.next_node = new_node
        new_node.previous_node = temp
        
    def delete(self, data):
        temp = self.head
        if temp.next_node is not None:
            if temp.data == data:
                temp.next.previous = None
                self.head = temp.next_node
                temp.next = None
                return
            else:
                while temp.next_node is not None:
                    if temp.data == data:
                        break
                    temp = temp.next_node
                if temp.next:
                    temp.previous_node.next_node = temp.next_node
                    temp.next_node.previous_node = temp.previous_node
                    temp.next_node = None
                    temp.previous_node = None
                else:
                    temp.previous_node.next_node = None
                    temp.previous_node = None
                
                return
            
            if temp == None:
                return
            
    def search(self, node, data):
        if node == None:
            return False
        if node.data == true:
            return True
        self.search(node.get_next(), data)
        
    def print_list(self):
        temp = self.head
        while(temp):
            print(temp.data, end=' ')
            temp = temp.next_node
```


```python
my_list = DoublyLinkedList()
my_list.insert_at_start(1)
my_list.insert_at_start(2)
my_list.insert_at_end(6)
my_list.insert_at_end(2)
my_list.print_list()
```

    2 1 6 2 

## 2. Trees

Similar to a linked list, but any node can point to a number of nodes.  Non-linear data structure. Hierarchical in nature. Many variations with loads of applications (PQ trees, AVL trees, Red Black Trees etc.).

- Easy to search
- Easy to manipulate sorted lists of data
- Root node is the one with no parents.
- Edge is the link between parent and child.
- Node with no children is called a leaf.
- Children of same parent are called children.

### 2.1. Basic Tree


```python
class Node(object):
    def __init__(self, data = None):
        self.left = None
        self.right = None
        self.data = data
    
    def set_left(self, node):
        self.left = node
        
    def set_right(self, node):
        self.right = node
        
    def get_left(self):
        return self.left

    def get_right(self):
        return self.right
    
    def set_data(self, data):
        self.data = data
    
    def get_data(self):
        return self.data
    
# Traverse to leftmost and then print and then to rightmost
def in_order_traversal(tree):
    if tree:
        in_order_traversal(tree.get_left())
        print(tree.get_data(), end=' ')
        in_order_traversal(tree.get_right())
    return
        
    
# We print the root node and then to the leftmost and then to the rightmost
def pre_order_traversal(tree):
    if tree:
        print(tree.get_data(), end=' ')
        pre_order_traversal(tree.get_left())
        pre_order_traversal(tree.get_right())
    return
        
    
# We traverse to the leftmost node and then to the rightmost node and then print
def post_order_traversal(tree):
    if tree:
        post_order_traversal(tree.get_left())
        post_order_traversal(tree.get_right())
        print(tree.get_data(), end=' ')
    return
        
```


```python
root = Node(1)
root.set_left(Node(2))
root.set_right(Node(5))
root.left.set_left(Node(3))
root.left.set_right(Node(8))

'''
    1
   / \
  2   5
 / \
3   8
'''

print('In Order Traversal:')
in_order_traversal(root)
print('\nPre Order Traversal:')
pre_order_traversal(root)
print('\nPost Order Traversal:')
post_order_traversal(root)
```

    In Order Traversal:
    3 2 8 1 5 
    Pre Order Traversal:
    1 2 3 8 5 
    Post Order Traversal:
    3 8 2 5 1 

### 2.2. Binary Search Tree

- Full if every node has 0 or 2 children.
- Complete if all levels are completely filled except last level.
- Perfect if all internal nodes have two children and all leaves are at same level
- Balanced if height of tree is O(logn) where n is number of nodes.
- Degenerate if every internal node has one child. Same performance-wise as Linked List.


```python
class Node(object):
    def __init__(self, data):
        self.data = data
        self.left_child = None
        self.right_child = None
        
    def get_left(self):
        return self.left_child
    
    def get_right(self):
        return self.right_child
    
    def get_data(self):
        return self.data
        
    def insert(self, data):
        if self.data == data:
            return False
        elif data < self.data:
            if self.left_child:
                return self.left_child.insert(data)
            else:
                self.left_child = Node(data)
                return True
        else:
            if self.right_child:
                return self.right_child.insert(data)
            else:
                self.right_child = Node(data)
                return True
    
    def min_value_node(self, node):
        current = node
        while current.left_child is not None:
            current = current.left_child
            
        return current
    
    def max_value_node(self, node):
        current = node
        while current.right_child is not None:
            current = current.right_child
        
        return current
    
    def delete(self, data):
        if self is None:
            return None
        
        if data < self.data:
            self.left_child = self.left_child.delete(data)
        elif data > self.data:
            self.right_child = self.right_child.delete(data)
        else:
            if self.left_child is None:
                temp = self.right_child
                self = None
                return temp
            elif self.right_child is None:
                temp = self.left_child
                self = None
                return temp
            else:
                temp = self.min_value_node(self.right_child)
                self.data = temp.data
                self.right_child = self.right_child.delete(temp.data)
                
        return self
    
        
    # Traverse to leftmost and then print and then to rightmost
    def in_order_traversal(self):
        if self:
            if self.left_child:
                self.left_child.in_order_traversal()
            print(self.get_data(), end=' ')
            if self.right_child:
                self.right_child.in_order_traversal()
        return


    # We print the root node and then to the leftmost and then to the rightmost
    def pre_order_traversal(self):
        if self:
            print(self.get_data(), end=' ')
            if self.left_child:
                self.left_child.pre_order_traversal()
            if self.right_child:
                self.right_child.pre_order_traversal()
        return


    # We traverse to the leftmost node and then to the rightmost node and then print
    def post_order_traversal(self):
        if self:
            if self.left_child:
                self.left_child.post_order_traversal()
            if self.right_child:
                self.right_child.post_order_traversal()
            print(self.get_data(), end=' ')
        return
    
    
class Tree(object):
    def __init__(self):
        self.root = None
        
    def insert(self, data):
        if self.root:
            return self.root.insert(data)
        else:
            self.root = Node(data)
            return
        
    def pre_order(self):
        if self.root is not None:
            print('\nPre order:')
            self.root.pre_order_traversal()
    
    def in_order(self):
        if self.root is not None:
            print('\nIn order:')
            self.root.in_order_traversal()
            
    def post_order(self):
        if self.root is not None:
            print('\nPost order:')
            self.root.post_order_traversal()
```


```python
tree = Tree()
tree.insert(10)
tree.insert(12)
tree.insert(5)
tree.insert(4)
tree.insert(20)
tree.insert(8)
tree.insert(7)
tree.insert(15)
tree.insert(13)

'''
       10
      /  \
     5   12
    / \    \
   4   8    20
      /    /
     7    15
         /
        13
'''

tree.pre_order()
tree.in_order()
tree.post_order()

```

    
    Pre order:
    10 5 4 8 7 12 20 15 13 
    In order:
    4 5 7 8 10 12 13 15 20 
    Post order:
    4 7 8 5 13 15 20 12 10 

#### Breadth First Traversal of Tree


```python
def breadth_first_traversal(root):
    if root == None:
        return 0
    else:
        h = height(root)
        for i in range(1, h+1):
            print_bft(root, i)

def height(node):
    if node is None:
        return 0
    else:
        left_height = height(node.left_child)
        right_height = height(node.right_child)
        
        if left_height > right_height:
            return left_height + 1
        else:
            return right_height + 1
            
def print_bft(root, level):
    if root is None:
        return
    else:
        if level == 1:
            print(root.data, end = ' ')
        elif level > 1:
            print_bft(root.left_child, level - 1)
            print_bft(root.right_child, level - 1)


'''
       10
      /  \
     5   12
    / \    \
   4   8    20
      /    /
     7    15
         /
        13
'''


breadth_first_traversal(tree.root)
```

    10 5 12 4 8 20 7 15 13 

## 3. Heaps

Good for queueing shit.  Good locality of reference + cache friendly. 


```python
class BinaryHeap(object):
    def __init__(self):
        self.heap = [0]
        self.current_size = 0
        
    def shift_up(self, index):
        while (index // 2) > 0:
            if self.heap[index] < self.heap[index // 2]:
                temp = self.heap[index // 2]
                self.heap[index] = temp
            index = index // 2
            
    def insert(self, key):
        self.heap.append(key)
        self.current_size += 1
        self.shift_up(self.current_size)
        
    def shift_down(self, index):
        while (index * 2) <= self.current_size:
            min_child = self.min_child(index)
            if self.heap[index] > self.heap[min_child]:
                temp = self.heap[index]
                self.heap[index] = self.heap[min_child]
                self.heap[min_child] = temp
            index = min_child
            
    def min_child(self, i):
        if (i * 2 + 1) > self.current_size:
            return i * 2
        else:
            if self.heap[i * 2] < self.heap[i * 2 + 1]:
                return i * 2
            else:
                return i * 2 + 1
    
    def delete(self):
        deleted_node = self.heap[1]
        self.heap[1] = self.heap[self.current_size]
        self.current_size -= 1
        self.heap.pop()
        self.shift_down(1)
        return deleted_node
    
            
    def build_heap(self, alist):
        i = len(alist) // 2
        self.current_size = len(alist)
        self.heap = [0] + alist[:]
        while (i > 0):
            self.shift_down(i)
            i = i - 1
            
```


```python
heap = BinaryHeap()
heap.build_heap([9,5,6,2,3,25])
print(heap.delete())
print(heap.delete())
print(heap.delete())
print(heap.delete())
print(heap.delete())
print(heap.delete())
print(heap.delete())
```

    2
    3
    5
    6
    9
    25



    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-116-e0d70120c69c> in <module>()
          7 print(heap.delete())
          8 print(heap.delete())
    ----> 9 print(heap.delete())
    

    <ipython-input-115-7054796aeaee> in delete(self)
         35 
         36     def delete(self):
    ---> 37         deleted_node = self.heap[1]
         38         self.heap[1] = self.heap[self.current_size]
         39         self.current_size -= 1


    IndexError: list index out of range



```python

```


```python

```
