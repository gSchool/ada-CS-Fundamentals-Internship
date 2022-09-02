# Binary Search Trees

## Overview

The data structures we've reviewed thus far are all examples of a _linear structure_. Linked lists are a linear structure, with each node directly linking to exactly one other node in the structure (the next node).

![Linked List Diagram](images/linked-list-vocab.png)

*Fig. 1. Linked List Diagram*

Recall that our Node class from the [Linked List Topic](../02-linked-lists/01-linked-lists.md), which we will refer to here as `ListNode`, looked like this:

```python
class ListNode:
    def __init__(self, value, next=None):
        self.data = value
        self.next = next
```

The `ListNode` class was used in a larger `LinkedList` class which maintained a chain of `ListNode` objects starting with a node pointed to by an instance variable called `head`.

### Consider A Nonlinear Structure

Binary search trees have a _non-linear structure_. In a binary search tree each node has pointers to two other nodes in the data structure. We refer to these pointers collectively as the _child_ nodes of the original _parent_ node. We label each of the parent node's two children as the `left` and `right` children or pointers. 

A binary search tree's `left` and `right` child nodes must maintain special properties. The `left` child must have a `key` that is less than or equal to the `key` of its parent node. The `right` child must have a `key`  that is greater than or equal to that of its parent node.

### !callout-info

## Keys vs Values

Nodes can store a `value` or piece of data that is not a number. For example a node can have a string as a `value`. When our nodes store non-numerical data we still need a way to determine whether a node is less than or greater than another node. This can be done by assigning each node a separate numerical `key`. 

### !end-callout


Each node in a binary search tree can refer to other nodes. Like a real person, a node can be both a parent _and_ a child. The topmost node in a tree is known as the _root_. The root has no parent node. Nodes with no children are called _leaves_.

When we draw a binary search tree, parent nodes are always drawn above children nodes with the root node at the very top. 
 

![Binary Search Tree Vocabulary](images/TreeVocabulary.png)

In summary, in a Binary Search Tree:

- Nodes with keys/values less than any node are stored to the **left** of that node.
- Nodes with keys/values greater than any node are stored to the **right** of that node.

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-info

## Tree Data Structure

A binary search tree is a subtype of a more general data type: a _tree_. Trees are always both non-linear and hierarchical, meaning that they are always a collection of nodes where each node points to a series of other _child_ nodes. 

Different types of trees will maintain different properties including but not limited to the number of children nodes each parent has and the values children nodes can have in relation to their parent node.

### !end-callout

### Binary Search Tree Node

Instead of a node with one `next` pointer, we can create nodes with 2 pointers, `left` and `right`.  Since each node can have 2 successors or _children_, it forms a _non-linear_ binary structure as opposed to the linear structure of a linked list.

This node stores both a key and value for each node.  The `Tree` class will compare keys to maintain node order.

```python
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None
```

### The Tree Class

Just like the `LinkedList` class discussed above, we can create a `Tree` class to represent the full data structure, using the `TreeNode` class to create nodes and build the tree.

```python
class Tree:
    def __init__(self):
        self.root = None # The root is the starting
                  # node in the Tree
    # Tree methods go here...
```
How do the same operations we looked at with arrays and linked lists work with a binary search tree?

### Insertion

The root is where the tree begins; the topmost node. New nodes as they are added are placed to the left of a given node if they are less than or equal to the current node, and to the right if they are greater than the current node. This is a natually recursive process. We can outline a recursive insertion implementation as follows:

```
Method add:
    Base Case:
        If the root is None set the root to be a new node with the given value and return the node.

    Recursive Case:
        Otherwise:
            If the value is less than the current node's value, make the current node's left be the result of calling add on the node's left.
            Otherwise make node's right be the result of calling add on node's right.
```

![Tree Insert operation visualization](./images/Binary-search-trees__insert-into-tree.gif)

_Fig.  Visualization of inserting a value into a BST_

You can experiment with this in the [Binary Tree Visualizer](https://visualgo.net/en/bst)


Implemented fully, the recursive implementation of `add` might look like this.

```python
    # helper function handles the recursive case
    def add_helper(self, current_node, new_node):

        # if new node should be in left subtree (less than current node)
        if new_node.key < current_node.key: 
            # if current node is a leaf
            if not current_node.left:
                # make new node left child of current node
                current_node.left = new_node
                return
            # Otherwise, recurse through left subtree of current node
            self.add_helper(current_node.left, new_node)
        # if new node should be in right subtree 
        # (greater than or equal to current node)
        else:
            # if current node is a leaf
            if not current_node.right:
                # make new node right child of current node
                current_node.right = new_node
                return
            # Otherwise, recurse through right subtree of current node
            self.add_helper(current_node.right, new_node)

    def add(self, key, value = None):
        # base case
        if not self.root:
            self.root = TreeNode(key, value)
        # recursive case
        else:
            new_node = TreeNode(key, value)
            self.add_helper(self.root, new_node)
```

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 39be2c02-aef0-481f-91e6-7778420bc737
* title: Binary Search Tree Iterative Insertion
* points: 1
<!-- * topics: [python, pandas] (Checkpoints only, optional the topics for analyzing points) -->

##### !question

Now that you have seen the recursive solution, see if you can implement the same `add` method iteratively. An node with a value equal to that of its parent should be added to the parent's right subtree.

##### !end-question

##### !placeholder

```py
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None

class Tree:
    def __init__(self):
        self.root = None # The root is the starting
                  # node in the Tree
    
    def add(self, key, value = None):
        pass
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
#   def setUp(self) -> None:
#     self.empty_tree = Tree()
#     # self.tree_with_nodes = tree_with_nodes(self.empty_tree)

#     # def tree_with_nodes(empty_tree) -> Tree():
#     #     empty_tree.add(5, "Peter")
#     #     empty_tree.add(3, "Paul")
#     #     empty_tree.add(1, "Mary")
#     #     empty_tree.add(10, "Karla")
#     #     empty_tree.add(15, "Ada")
#     #     empty_tree.add(25, "Kari")
#     #     return emtpy_tree

    def test_add_node_to_empty_tree(self):
        #Arrange
        t = Tree()

        #Act
        t.add(5, "Peter")

        #Assert
        self.assertEqual(5, t.root.key)
        self.assertEqual("Peter", t.root.value)
        self.assertEqual(None, t.root.left)
        self.assertEqual(None, t.root.right)

    def test_add_node_left_child(self):

        #Arrange
        t = Tree()

        #Act
        t.add(5, "Peter")
        t.add(3, "Paul")

        #Assert
        self.assertEqual(5, t.root.key)
        self.assertEqual("Peter", t.root.value)
        self.assertEqual(3, t.root.left.key)
        self.assertEqual("Paul", t.root.left.value)
        self.assertEqual(None, t.root.right)

    def test_add_node_right_child(self):
        #Arrange
        t = Tree()

        #Act
        t.add(5, "Peter")
        t.add(10, "Kara")

        #Assert
        self.assertEqual(5, t.root.key)
        self.assertEqual("Peter", t.root.value)
        self.assertEqual(None, t.root.left)
        self.assertEqual(10, t.root.right.key)
        self.assertEqual("Kara", t.root.right.value)

    def test_duplicate_key_added_to_right(self):
        #Arrange
        t = Tree()

        #Act
        t.add(5, "Peter")
        t.add(5, "Peter's twin")

        #Assert
        self.assertEqual(5, t.root.key)
        self.assertEqual("Peter", t.root.value)
        self.assertEqual(None, t.root.left)
        self.assertEqual(5, t.root.right.key)
        self.assertEqual("Peter's twin", t.root.right.value)

    def test_add_large_tree(self):
        #Arrange
        t = Tree()

        #Act
        t.add(5, "Peter")
        t.add(3, "Paul")
        t.add(1, "Mary")
        t.add(10,"Karla")
        t.add(9, "Char")
        t.add(15, "Ada")
        t.add(25, "Kari")

        #Assert
        self.assertEqual(5, t.root.key)
        self.assertEqual("Peter", t.root.value)
        self.assertEqual(3, t.root.left.key)
        self.assertEqual("Paul", t.root.left.value)
        self.assertEqual(1, t.root.left.left.key)
        self.assertEqual("Mary", t.root.left.left.value)

        self.assertEqual(10, t.root.right.key)
        self.assertEqual("Karla", t.root.right.value)
        self.assertEqual(9, t.root.right.left.key)
        self.assertEqual("Char", t.root.right.left.value)
        self.assertEqual(15, t.root.right.right.key)
        self.assertEqual("Ada", t.root.right.right.value)
        self.assertEqual(25, t.root.right.right.right.key)
        self.assertEqual("Kari", t.root.right.right.right.value)
```

##### !end-tests

##### !hint 

Look back at the [Linked Lists Problem Set](../02-linked-lists/02-linked-lists-implementation.md) to see how you iteravely stepped through a linked list. 

Look at the recursive solution and try to translate each step into your iterative solution.

Still feeling stuck? Check this video walkthrough of the solution.

<!-- ADD VIDEO WALKTHROUGH -->
##### !end-hint 

##### !explanation

An example of a working implementation:

```python
    def add(self, key, value = None):
        new_node = TreeNode(key, value)
        if not self.root:
            self.root = new_node
            return
        current = self.root
        while current:
            if key < current.key:
                if not current.left:
                    current.left = new_node
                    return
                current = current.left
            else:
                if not current.right:
                    current.right = new_node
                    return
                current = current.right
```

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


### Deletion

To delete a node from a binary search tree we must first find the node to delete. To find the node, we can use the same recursive technique to traverse the root node's subtrees. Once we find the node we can delete it by changing the parent and child nodes' references.

```
Method delete:
    Base Case:
        If the root is None, return None
  
    Recursive Case:
        Otherwise, recur down the tree:
            If the key is less than the current node's key, call the delete function on current node's left subtree.

            If the key is greater than the current node's key, call the delete function on current node's right subtree.

            If the current node is the node to be deleted:
                If current node's left child is None:
                    return the right child
                If current node's right child is None:
                    return the left child
                Otherwise:
                    Find the minimum node in the right subtree
                    Set the current node equal to the minimum node
        Return the current node
```
<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: e6e5ea66-d55f-4fc0-bc6f-eeda3f8106bd
* title: Binary Search Tree Recursive Removal
* points: 1

##### !question

Implement `delete` recursively for a binary search tree. The current_root 

##### !end-question

##### !placeholder

```py
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None

class Tree:
    def __init__(self):
        self.root = None # The root is the starting
                  # node in the Tree
    
    def delete(self, current_root, key):
        pass
```

##### !end-placeholder

##### !tests

[the unit tests below will run against the student submission]
```py
import unittest
import main as p
import numpy as np

class TestPython1(unittest.TestCase):
  def test_one(self):
    self.assertEqual(1,p.doSomething())
```

##### !end-tests

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->



### Searching - O(log n)

You can try to search to find a value in a Binary Search Tree Like this:

```
Start the current node at the root
If the current node is nil return nil
If the current node equals the value 
    being searched for return the current
    node's data

If the value is less than the current node 
    return search on current node's left side
If the value is greater than the root 
    return search on current node's right side
```

### Finding A Node With Python

![Finding a 29 in a tree visualization](./images/Binary-Search-Trees__find-value.gif)

_Fig.  A visualization of finding a value in a BST._

You can implement the `find` method in Python as follows:

```python
class Tree:
    def __init__(self):
        self.root = None
    
    def find(self, key):
        current = self.root

        while current != None:
            if current.key == key:
                return current.value
            elif key < current.key:
                current = current.left
            else:
                current = current.right

        return None
```

### Recursive Find Method

Because every node in a Binary Search Tree is the root of a subtree, you can take advantage of the recursive structure to write a recursive solution.

```python
class Tree:
    def __init__(self):
        self.root = None
    
    def find_helper(self, current, value):
        if current == None:
            return None
        elif current.data == value:
            return current.value
        elif value < current.data:
            return self.find_helper(current.left, value)

        return self.find_helper(current.right, value)

    def find(self, value):
        return self.find_helper(self.root, value)
```

### Exercise

Try this out on the [Binary Tree Visualizer](https://visualgo.net/en/bst).

**Question**:  If you have a tree of height 5, what's the worst-case for finding a value in the tree?  What affects the number of comparisons you need to make?

<details style="max-width: 700px; margin: auto;">
  <summary>
    Open this to see our answer.
  </summary>

  Worst-case, you need to make comparisons to 5 nodes before inserting.  This occurs when you need to insert a new node into a leaf.

  Worst-case:  O(h) comparisons where _h_ is the height of the tree
</details>

## Balanced Trees & Unbalanced Trees

A tree is considered **balanced** if the levels of any two leaves differ by at most 1.  In this way the nodes in the tree must be spread fairly evenly.

This is an example of a balanced tree.

![balanced bst](images/balanced-bst.png)

On the other hand this is an unbalanced tree.

![unbalanced bst](images/unbalanced-bst.png)

### !callout-warning

## Tree Balance & Time Complexity

Assume that we are using the Binary Search tree methods as we have described them here.  If all the nodes were inserted in order, the worst case time complexity would be O(n) because each node except the root would be the left child of the previous nodes if the nodes were inserted in descending order, or the right child of the previous node if they were inserted in ascending order.  The tree would be **unbalanced**.  There are more advanced algorithms that can be used to create self-balancing trees.

* If a tree is unbalanced it's time complexities for Insertion, Deletion, and searching approach O(n).
* If a tree is balanced it's time complexities for Insertion, Deletion, and searching are O(log n).

Therefore it is very important that a tree **remain balanced**.

### !end-callout

### !challenge

* type: number
* id: 476cab10-a81f-4877-aad3-682602a3c30d
* title: How many nodes do you need to examine to find 5, in the 1st example?
* decimal: 0
* points: 1
* topics: bst

##### !question

How many nodes do you need to examine to find 5, in the 1st example?

##### !end-question

##### !placeholder

put a number in here

##### !end-placeholder

##### !answer

3

##### !end-answer


### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: number
* id: 5a4ce281-7f17-47e5-961e-a582171eb3be
* title: How many nodes to check in the 2nd example?
* decimal: 0
* points: 1
* topics: bst

##### !question

How many in the 2nd?

##### !end-question

##### !placeholder

Number goes here

##### !end-placeholder

##### !answer

5

##### !end-answer


### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: number
* id: b7d69d24-04e0-4891-beaa-ccbb81f73fed
* title: 5 level tree
* decimal: 0
* points: 1
* topics: bst

##### !question

With the [Binary Tree Visualizer](https://visualgo.net/en/bst), build a **balanced** tree with a height of 5 levels.  How many comparisons do you need to make to find a particular leaf node?

##### !end-question

##### !placeholder

Number goes here

##### !end-placeholder

##### !answer

5

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: number
* id: 0dd499dc-7260-4d51-aabd-b9f4560e1047
* title: 6 level tree
* decimal: 0
* points: 1
* topics: bst

##### !question

Add 5 more nodes to the balanced tree, maintaining the balance.  How many comparisons do you need to make now to find a particular leaf node?

##### !end-question

##### !placeholder

Number goes here

##### !end-placeholder

##### !answer

6

##### !end-answer

<!-- other optional sections -->
##### !hint 

How many levels does adding 5 nodes add, if you maintain balance?

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: number
* id: f32167e5-2264-49bc-8850-f81afd0f697b
* title: Unbalanced 5 level tree
* decimal: 0
* points: 1
* topics: bst

##### !question

Build a **completely unbalanced** tree with 5 levels.  How many comparisons to find a leaf node?

##### !end-question

##### !placeholder

Number here

##### !end-placeholder

##### !answer

5

##### !end-answer

<!-- other optional sections -->
##### !hint

What's the worst case?

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Worst-case you have to travel to the last node in the chain and since there are 5 levels, it takes 5 comparisons

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: number
* id: a97fce91-ee27-4f04-be01-7484247a236e
* title: Adding 4 more unbalanced nodes
* decimal: 0
* points: 1
* topics: bst

##### !question

What if you added 4 nodes and kept the tree unbalanced. How many more comparisons would you need to make?

##### !end-question

##### !placeholder

Number goes here 

##### !end-placeholder

##### !answer

9

##### !end-answer

<!-- other optional sections -->
##### !hint

If you have 5 levels and add 4 more nodes, how many levels do you gain if the tree is totally unbalanced?

##### !end-hint

##### !explanation

Worst case you added 4 more levels 5 + 4 = 9, so 9 comparisons to find the value.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: short-answer
* id: 78ea3ad2-2a41-496b-af4a-535720e0e4f4
* title: Growth as `n` changes
* points: 1
* topics: bst

##### !question

Create a tree with one node.  Then double the number of nodes, **keeping the tree balanced.**  Then double the number of nodes again, maintaining balance.  Notice how the height changes.

What standard Big-O time complexity does this match?
  

##### !end-question

##### !placeholder

O(?)

##### !end-placeholder

##### !answer

/O\(log n\)/

##### !end-answer

<!-- other optional sections -->
##### !hint 

Answer in the form of O(n), O(nlog n) or O(log n) etc

##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 

O(log n) when you double the number of nodes, the height increases by 1.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

Notice if a tree is balanced, when you move left or right, you eliminate half of the possible nodes.  This means you are essentially doing **binary search.**  If the tree is unbalanced, you are performing a linear search.

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-star

## Balance is important in a tree's efficiency

If a tree is _balanced_ then adding, finding, removing operations on a that tree perform in O(log n) time.  However if a tree becomes unbalanced the efficiency can approach O(n) time complexity.  

For this reason, computer scientists spend a lot of time focusing on ways to maintain the balance of a Binary Search Tree.

### !end-callout

**Self-Balancing Trees** There are a lot of algorithms for [keeping a tree balanced](https://en.wikipedia.org/wiki/Self-balancing_binary_search_tree).  The act of keeping a tree balanced is also O(log n), and so rebalancing a tree after an insertion or deletion doesn't significantly impact the runtime of a binary search tree.  These structures are wonderful things to learn, but beyond the scope of this class.  You **can** however rest assured that any library tree classes that you use will keep the tree balanced in such a manner.

## Summary

In this lesson we looked at the advantages a Binary Search Tree provides over a sorted array or LinkedList.  Binary Search trees provide an O(log n) time to add, remove and find elements because searching a tree performs a binary search.  This performance however depends on the tree being **balanced**.  A balanced tree has subtrees of height within 1 of each other.

In short we want to use a Binary Search Tree When:

- Maintaining order is important
- We want to maintain efficient search, insertion and deletion time complexities

## Big-O Comparison

We can see below a balanced Binary Search Tree provides good performance while maintaining elements in order.  

**#**|**Data Structure**|**Access By Key**|**Search**|**Insertion (Middle)**|**Deletion (Middle)**|**Add First**|**Add Last**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
1|Unsorted Array|O(1)|O(n)|O(n)|O(n)|O(n)|O(1)
2|Sorted Array|O(1)|O(log n)|O(n)|O(n)|O(n)|O(1)
3|Linked List|O(n)|O(n)|O(n)|O(n)|O(1)|O(1)
4|Binary Tree (balanced)|O(log n)|O(log n)|O(log n)|O(log n)|NA|NA
5|Hash Table|O(1)|O(1)|O(1)|O(1)|NA|NA