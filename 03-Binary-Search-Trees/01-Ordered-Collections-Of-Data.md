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

Arrays and linked lists are two data structures that can be used to store ordered collections of data. Each has its respective advantages and disadvantages. Binary Search Trees are another data structure that we can consider.

### !callout-info

## What about dictionaries?

Dictionaries are unordered and thus cannot be used to store ordered data.

### !end-callout


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