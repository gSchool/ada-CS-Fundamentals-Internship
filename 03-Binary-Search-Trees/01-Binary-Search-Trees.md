# Binary Search Trees

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=ceac4982-192f-44a7-88a8-ad91016c972b&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

Students should be able to:

- Compare a Binary Tree to a Linked List
- Explain how a Binary Search Tree differs from a generic Binary Tree
- Write methods to perform the following on a Binary Search tree:
  - Search
  - Insert value
  - Delete value
  - Find height
  - Perform traversals including: 
    - Depth first traversals: pre-order, in-order, post-order
    - Breadth first traversal

## Video Lesson & Exercises

- [Video Lesson](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?id=d9746397-8a10-43be-b1cc-aaaf00720b31)
- [Slide Deck](https://docs.google.com/presentation/d/1Fj0deIUswGZ3ooJMpgVUqPEaWHKTkQ1w2Ci-yf8v66M/edit#slide=id.p)
- [BST Exercise](https://github.com/Ada-C16/tree-practice)

## Vocabulary and Synonyms

| Vocab          | Definition                                                    | Synonyms  | How to Use in a Sentence                                                      |
| -------------- | ------------------------------------------------------------- | --------- | ----------------------------------------------------------------------------- |
| Linked List | A linear collection of data elements whose order is not given by their physical placement in memory.  Each element of the list contains a reference to the next element.     |       | "Because I wanted to add and remove elements to the front and rear, I used a linked list to store the data." |
| Tree      | A widely used abstract data type that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes. |  | "I used a tree to store ordered data." |
| Binary Tree      | A tree structure in which each node has at most two children, which are referred to as the _left child_ and _right child_. |  | "A Mathematical expression can be written as a binary tree where the leaves are values and the parent nodes are operators like +, -, *, and /." |
| Binary Search Tree      | A specific type of Binary Tree which is a rooted binary tree data structure whose internal nodes each store a key greater than all the keys in the node’s left subtree and less than those in its right subtree. | Ordered Binary Tree | "Because 23 is less than the root, it can only be found in the left subtree of this binary search tree." |
| Leaf      | A node in a tree with no descendants. |  | "Because the left and right subtrees of the current node were `None`, this node is a leaf." |
| Parent      | A node with descendants. |  | "Because the left and right subtrees of the current node not `None`, this node is a parent and not a leaf." |
| Unbalanced Tree 	|  A BST where each node has 0 or 1 children (it looks like a linked list) 	| | The tree was unbalanced so inserting new values took linear time. |
| Balanced Tree 	| A tree where the the level of any two leaves differs by at most 1 node.	| | "Because my tree is balanced, it's quick to find values inside it."  |
| Subtree | The tree which is a child of a node. Note: The name emphasizes that everything which is a descendant of a tree node is a tree, too, and is a subset of the larger tree.| | "The value I'm looking for is less than the current node, so I will continue searching in the left subtree." |
| Traversal 	|  A method of visiting each node in a BST	| | "My method performs a traversal visiting each node in the tree, level-by-level." |
| Depth-First Traversal 	|  An algorithm for traversing or searching a tree. The algorithm starts at the root node and explores as far as possible along each branch before backtracking.	| | A depth-first traversal looks like a mouse exploring a maze in that it goes as far down one path before backtracking when encountering dead ends. |
| Breadth-first traversal 	|  An algorithm for searching a tree data structure for a node that satisfies a given property. It starts at the tree root and explores all nodes at the present depth prior to moving on to the nodes at the next depth level. 	| | I printed out the tree level-by-level so I had to perform a breadth-first traversal. |

## Overview

We commonly encounter problems which require us to maintain ordered collections of data. This could be a list of students by name, jobs to process by priority or a collection of accounts by username.

When dealing with an ordered collection of data, we need to consider the time and space complexity of the following operations:

* **Insertion** - Adding elements to the collection
* **Deletion** - Removing elements from the collection
* **Searching** - Finding an element in the collection
* **Serialization** - Converting the collection to an array or string to write to a file, network, or database

Dictionaries are unordered and thus cannot be used to store ordered data, however we *could* use arrays or linked lists to store ordered data.

### Using An Array for Ordered Data

If we maintain an ordered array of data we can examine these 4 operations.

**Insertion** - O(n)

Adding an element to a sorted list requires us to first find the index in which to insert the new value and then each subsequent item must be shifted before a new item can be inserted.

Finding an item is an O(log n) operation because we can use binary search to find the index to insert into.  Then shifting each element over to the right is an O(n) operation.  Because the larger term dominates insertion is an O(n) operation.

![Adding an element to a sorted array](images/adding-sorted-array-element.png)

<!-- Image source:  https://www.draw.io/#G1j_vbvEN5UgNSszrKSPgwA7agvgQdhs1r -->

**Deletion** - O(n)

Similarly to remove an element from an ordered array, we must first find the index of the element to delete and then shift each subsequent element over to the left.

![Deleting an element from an array](images/deleting-array-element.png)

<!-- Image at:  https://drive.google.com/file/d/1PeYa3z7mgVxy6jOPqS7brL09u2Vq_nFW/view?usp=sharing -->

**Searching** - O(log n)

To find an element in an ordered array, we can use [binary search](https://www.geeksforgeeks.org/python-program-for-binary-search/) to find the index of the given element.  Because binary search is an O(log n) operation, finding an element in an ordered array is an O(log n) operation.

**Serialization** - O(n)

Serialization is a process of converting the data into a format that can be stored in a file, network, or database. In languages like Python this is often done by converting the data into a string.  You can do so using the `JSON.dumps()` function.  This function iterates through the list and converts each element into a string.  This is an O(n) operation.

### What About a Linked List

Likewise we could use a Linked List. We can also examine how well Linked Lists perform these operations.

**Insertion**  - O(n)

Maintaining a list in order requires Ada's application to:

1. **find** the location in the list to do the insertion - O(n)
1. Adjusting links to insert the new node - O(1)

While adjusting the links to insert a new node in a Linked List is O(1), finding the place to do the insertion would be O(n). So while the process of inserting a new node between two existing nodes in a linked list very fast, finding the location to insert into is not resulting in an overall O(n) operation.

**Deletion** - O(n)

Again to delete a specific node from a linked list requires us to first **find** it. To find the node we must traverse the list until we find the node prior to the node we want to delete.  This is an O(n) operation.

**Searching** - O(n)

Because we cannot perform a binary search on a linked list, we must instead perform a linear search which runs in O(n) time.

**Serialization** - O(n)

To convert a linked list into a string or other data type suitable to write to another device we need to iterate through the list and access the value of each node. To visit each node requires O(n) operations and thus linear runtime.

## The Need

We want to maintain an ordered collection of data and outperform both arrays and linked lists in terms of insertion, deletion, searching and serialization, if possible.

The key requirements are:

1. Maintain a list of items in order.
1. Add and delete elements in better than O(n) time
1. Find elements with an O(log n) time
1. Serialize the list into a string or another data type that can be written to a file, network, or database in O(n) time or better.

If need 1 & 2 are maintained an array will struggle to add and delete items, and a Linked List will require O(n) for all operations because you have to traverse the sorted list to do anything. So another data structure is needed.

## Enter Binary Trees

Our Linked Lists are a linear structure with each node linking to the next node in the structure.

![Linked List Diagram](images/linked-list-vocab.png)

*Fig. 1. Linked List Diagram*

Our Node class from the LinkedList topic, which will be referred to as `ListNode`, looked like this:

```python
class ListNode:
    def __init__(self, value, next=None):
        self.data = value
        self.next = next
```

The `ListNode` class was used in a larger `LinkedList` class which maintained a chain of `ListNode` objects starting with a node pointed to by an instance variable called `head`.

### Consider A Nonlinear Structure

In a _Binary Search Tree_ each node's left pointer points to all elements smaller than or equal to the node's key.  The right pointer points to all nodes greater than the given node's key.   Each node can refer to other nodes.  A Tree is hierarchical with certain nodes acting as parents to others.  A node above another is the node's _parent_.  The node(s) below a node are it's _children_.  The topmost node in a tree is known as the _root_.  The nodes with no children are called _leaves_.

In a Binary Search Tree:

- Nodes with values less than any node are stored to the **left** of that node.
- Nodes with values greater than any node are stored to the **right** of that node. 

![Binary Search Tree Vocabular](images/TreeVocabulary.png)

### Binary Search Tree Node

Instead of a node with one link to a next node, we can create nodes with 2 pointers, left and right.  Since each node can have 2 successors or "children", it forms a binary structure as opposed to the linear structure of a Linked List.

This node stores both a key and value for each node.  The `Tree` class will compare keys to maintain node order.

```python
class TreeNode:
    def __init__(self, key, val = None):
        if val == None:
            val = key

        self.key = key
        self.value = val
        self.left = None
        self.right = None```
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

### Insertion - O(log n)

The _root_ is where the tree begins, the topmost node.  New nodes as they are added are placed to the left or a given node, if they are less than or equal to the current node, and to the right if they are greater than the current node.  This is a natually recursive process.

```
Method add:
  if the root is nil set the root to be a new node with the given value and return the node.

  Otherwise:
    if the value is less than or equal to the current node's value, make the current node's left be the result of calling add on root's left.
    otherwise make node's right be the result of calling add on node's right.
```

![Tree Insert operation visualization](./images/Binary-search-trees__insert-into-tree.gif)

_Fig.  Visualization of inserting a value into a BST_

You can experiment with this in the [Binary Tree Visualizer](https://visualgo.net/en/bst)

### Deletion - O(log n)

To delete a node from a binary search tree we must first find the node to delete.  This is an O(log n) operation.  Once we find the node we can delete it by changing the references.

```
Method delete(current_root, key):
    if the root is nil return nil
  
    Otherwise, recur down the tree
        if the key is less than the root's key delete the node in the left subtree.
            current_root.left = delete(current_root.left, key);
        otherwise if the key is greater than root's key delete the node in the right subtree.
            current_root.right = delete(current_root.right, key);


        Otherwise if the current root is the node to be deleted
        
            if the left child is none
                return current_root.right
            otherwise if current_root.right == none
                return current_root.left;

            Otherwise find the minimum node in the right subtree
            smallest_node_on_right = min_node(root.right);
            current_root.key = smallest_node_on_right.key;
            current_root.value = smallest_node_on_right.value;

            // Delete the inorder successor
            root.right = delete(root.right, root.key);

    return current_root;
```

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

## Serialization - O(n)

To serialize a tree, we need to traverse the tree.  This means we need to visit each node and add it to a string or array. There are several ways to do this.

A _traversal_ is an action visiting each node in a graph such as a tree.  There are several kinds of traversals, Breadth First Traversals which visit each node level, by level and Depth First Traversals which visit a node's children before it's siblings.

### Depth First Traversals

Unlike linear data structures like arrays or linked list which have only one logical way to traverse them, trees can be traversed in different ways.  In a _Depth-first traversal_ you explore the children and grandchildren of a node before moving to it's sibling.

There are three standard types of depth-first traversals:

- **Pre-Order**:  Current, Left, Right
- **In-Order**: Left, Current, Right
- **Post-Order**: Left, Right, Current

In a **Pre-Order** traversal you execute the algorithm in this manner:

```
visit the current node
traverse the left subtree
traverse the right subtree
```

In a **In-Order** traversal you execute the algorithm in this manner:

```
traverse the left subtree
visit the current node
traverse the right subtree
```

In a **Post-Order** traversal you execute the algorithm in this manner:

```
traverse the left subtree
traverse the right subtree
visit the current node
```

Notice that all of the algorithms are recursive in structure because each node can be treated as it's own subtree.

![Binary Search Tree 2](images/bst2.png)

For the above Binary Search Tree
- **Pre-Order**:  [50, 25, 10, 30, 75, 60, 100]
- **In-Order**: [10, 25, 30, 50, 60, 75, 100]
- **Post-Order**: [10, 30, 25, 60, 100, 75, 50]

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: number
* id: 83e29c11-66b7-4b74-a85b-4fe936c92fa2
* title: Height of a tree
* decimal: 0
* points: 1
* topics: bst

##### !question

![bst3](images/bst3.png)

What is the height of the above BST?

##### !end-question

##### !placeholder

Number goes here

##### !end-placeholder

##### !answer

3
##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: a1703f9c-c97c-4b7a-86cf-cadb8780c77f
* title: Balanced
* points: 1
* topics: bst

##### !question

![bst3](images/bst3.png)

Is the tree balanced?

##### !end-question

##### !options

* Yes
* No
* Huh?

##### !end-options

##### !answer

* Yes

##### !end-answer

##### !hint

In a balanced tree no sibling subtrees differ in height more than 1.  So no left-right subtrees differ in height by 1.

##### !end-hint

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: e755df96-56ec-4d50-a336-3834838abb96
* title: Inorder
* points: 1
* topics: bst, traversal

##### !question

![bst3](images/bst3.png)

In what order would you hit the nodes doing an inorder traversal

##### !end-question

##### !options

* [17, 14, 20, 19, 52]
* [14, 17, 19, 20, 52]
* [14, 19, 52, 20, 17]

##### !end-options

##### !answer

* [14, 17, 19, 20, 52]

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: 08e94a48-fc15-4d95-8a47-d8ed9e199b34
* title: Preorder
* points: 1
* topics: bst, traversal

##### !question

![bst3](images/bst3.png)

In what order would you hit the nodes doing an preorder traversal

##### !end-question

##### !options

* [17, 14, 20, 19, 52]
* [14, 17, 19, 20, 52]
* [14, 19, 52, 20, 17]

##### !end-options

##### !answer

* [17, 14, 20, 19, 52]

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: multiple-choice
* id: c6009e6c-5717-459a-ae66-4570918271b9
* title: Postorder
* points: 1
* topics: bst, traversal

##### !question

![bst3](images/bst3.png)

In what order would you hit the nodes doing an postorder traversal

##### !end-question

##### !options

* [17, 14, 20, 19, 52]
* [14, 17, 19, 20, 52]
* [14, 19, 52, 20, 17]

##### !end-options

##### !answer

* [14, 19, 52, 20, 17]

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Why Do Traversals

Traversals can be very useful to serialize our data structure into a format that can be easily read by humans or stored on another device.

- **Pre-order** If we need to save a tree data structure to disk, or send it across the network and maintain the structure, pre-order traversals can be useful.
- **In-Order**: If we need to print or otherwise visit all the nodes of a tree in order.
- **Post-Order**: If we need to delete all the nodes in a BST.

### !callout-info

## Why are they all left-to-right?

So why are all the traversals left-to-right instead of right-to-left?

Computer Science was initially pioneered in western cultures where people read left-to-right and so their cultural bias lead to designing traversals in that manner.  There's nothing inherit in Binary Search Trees to require this.  You could create a right-to-left traversal, but for historical reasons, these are the standard Binary Search Tree traversals.

### !end-callout

## Finding the Height of a Binary Search Tree

To find the height of a binary search tree you can do the following:

```
If the current node is nil return 0

Otherwise return 1 plus the maximum of the heights of the right and left subtrees
```

This is a recursive solution because it treats the left and right sides of a node as trees.


## Summary

In this lesson we looked at the advantages a Binary Search Tree provides over a sorted array or LinkedList.  Binary Search trees provide an O(log n) time to add, remove and find elements because searching a tree performs a binary search.  This performance however depends on the tree being **balanced**.  A balanced tree has subtrees of height within 1 of each other.

We also examined different methods to traverse a Tree.  Unlike a LinkedList where there is only one method to traverse a tree has multiple ways to traverse.

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

## Additional Resources

* [MIT Open Courseware on Binary Search Trees](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-006-introduction-to-algorithms-fall-2011/lecture-videos/lecture-5-binary-search-trees-bst-sort/)
* [FreeCodeCamp Binary Search Tree Algorithms for JavaScript Beginners](https://www.freecodecamp.org/news/binary-tree-algorithms-for-javascript-beginners/)
* [Geeks for Geeks on Self-Balancing-Binary-Search-Trees](https://www.geeksforgeeks.org/self-balancing-binary-search-trees-comparisons/)
