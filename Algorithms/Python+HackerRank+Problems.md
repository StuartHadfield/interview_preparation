
# Check if a tree is a valid BST


```python
def checkBST(root):
    return traverse(root, -sys.maxsize-1, sys.maxsize)
    
def traverse(node, mini, maxi):
    if node is None:
        return True
    else:
        return (mini < node.data) and (maxi > node.data) and traverse(node.left, mini, node.data) and traverse(node.right, node.data, maxi)
```

# Decode a huffman tree


```python
def decodeHuff(root, s):
    temp=root
    string=[]

    for i in s:
        c = int(i)
        if c == 1:
            temp = temp.right
        elif c == 0:
            temp = temp.left
        if temp.right == None and temp.left == None:
            string.append(temp.data)
            temp = root
    b = ''.join(string)
    print(b)
```
