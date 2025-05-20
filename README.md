# Huffman-Coding
## Aim
To implement Huffman coding to compress the data using Python.

## Software Required
1. Anaconda - Python 3.7

## Algorithm:
### Step1:
Get the input string.

### Step2:
Create tree nodes.

### Step3:
Main function to implement huffman coding.

### Step4:
calculate frequency of occurence.

### Step5:
print the characters and its huffmancode.
## Program:

```python
class NodeTree(object):
    def __init__(self, value=None, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

    def children(self):
        return (self.left, self.right)

    def __str__(self):
        return '%s %s' % (self.left, self.right)

def huffman_code_tree(node, binString=''):
    if node is None:
        return {}
    if type(node.value) is str:
        return {node.value: binString}

    (l, r) = node.children()
    d = dict()
    d.update(huffman_code_tree(l, binString + '0'))
    d.update(huffman_code_tree(r, binString + '1'))
    return d

def generate_huffman_code(string):
    freq = {}
    for c in string:
        if c in freq:
            freq[c] += 1
        else:
            freq[c] = 1
    freq = sorted(freq.items(), key=lambda x: x[1])
    nodes = [NodeTree(value=key) for key, _ in freq]
    nodes = [(NodeTree(value=key), freq) for key, freq in freq]

    while len(nodes) > 1:
        nodes = sorted(nodes, key=lambda x: x[1])
        (left_node, c1) = nodes[0]
        (right_node, c2) = nodes[1]

        nodes = nodes[2:]

        merged_node = NodeTree(left=left_node, right=right_node)
        nodes.append((merged_node, c1 + c2))

    huffmanCode = huffman_code_tree(nodes[0][0])

    print(' Char | Huffman code ')
    print('----------------------')
    for char, _ in freq:
        print(f'{char!r:<4}| {huffmanCode[char]:<12}')

string1 = "HIMAVATH"
string2 = "accelerate"

print("\nHuffman Codes for the first string:")
generate_huffman_code(string1)

print("\nHuffman Codes for the second string:")
generate_huffman_code(string2)

```
## Output:

### Print the characters and its huffmancode
![image](https://github.com/user-attachments/assets/49c8afbd-a74b-4e37-abee-c33752f2d068)



## Result
Thus the huffman coding was implemented to compress the data using python programming.
