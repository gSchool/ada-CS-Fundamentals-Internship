# Heaps

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?pid=608a709b-d0c2-4273-815d-ada2004e4e8d&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&captions=true&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>

## Learning Goals

By the end of this lesson you should be able to:

- Describe a heap data structure
- Explain how a heap data structure is maintained as elements are added and removed
- Explain several use-cases for a heap

## Video Lesson & Slides

- [Video Lesson](https://adaacademy.hosted.panopto.com/Panopto/Pages/Viewer.aspx?pid=608a709b-d0c2-4273-815d-ada2004e4e8d)
- [Slide Deck](https://docs.google.com/presentation/d/1UojimxYNCm7r4lxs5owPuST-e26uwN_h5jLjTBdQzgs/edit#slide=id.p7)
- [Heap Exercise](https://github.com/ada-C16/heaps)

## Introduction

In this lesson we will introduce a new data structure, a heap!  Heaps are a great way to store information in a semi-order.  Essentially if you have a collection of data that you can sort or compare, you can add it to a heap.  A heap maintains a [complete binary tree](https://web.cecs.pdx.edu/~sheard/course/Cs163/Doc/FullvsComplete.html).  In a complete binary tree each level is full except the last, and the last level is filled from left-to-right.  Further, in a heap each parent has a specific order-relationship with it's children.  In a Min-Heap every parent node is less than its child nodes.  In a Max-Heap, every parent node is greater than its child nodes.

Below is a drawing of a Max-Heap.

![Heap Diagram](images/heap.png)

<!-- Image source:  https://drive.google.com/file/d/17cH7vfyZg-PFlULi-bO2K4H61oc4pCDT/view?usp=sharing -->

On the other hand this is **not** a Max-Heap.  Notice that 47 on the bottom level is greater than 25, its parent.

![Invalid Max-Heap](images/invalid-max-heap.png)

This is also **not** a Max-Heap.  The last level is not full from left-to-right.  The 20 should be the left-child of 35.

![Another Invalid Max-Heap](images/invalid-max-heap2.png)

## Uses for Heaps

There are times when you remove items from a data structure in a specific order. For example consider an employee has been given a list of tasks to complete. However they should be handled by priority. The most important jobs should be handled first. 

We could use arrays or linked lists to store tasks, but that would entail `O(n)` time complexity for inserting and removing tasks.

We could use a binary search tree to store the tasks. However, as we discovered, maintaining the balance of the tree is a very expensive and difficult operation. However, properly handled adding or removing tasks would be `O(log n)` time complexity. Unfortunately however writing the tree to a disk or external storage using a traversal would entail `O(n)` time complexity to convert the data structure to a list.

Heaps provide a method of maintaining a balanced binary tree (but not a binary *search* tree) with O(log n) time complexity for adding and removing items, and maintain all elements in an internal array to allow faster transfer to external devices, like external storage.

### Priority Queues

What we have described is a _Priority Queue_.  A priority queue is an abstract data type, like a stack or a regular queue.  However, with a queue items are added and removed in a first-in-first-out (FIFO) order.  Priority queues remove items with the highest priority first.  By using a heap to implement a priority queue you can build a data structure to serve data by priority.  

### Heapsort

Since heaps allow you to extract elements in order, you can use them to sort an array.

With an array of `n` elements, to perform Heapsort you can add the elements to the heap, an O(nlog n) operation.  Then you can remove the elements from the heap one-by-one placing them in the proper place in an array, also an O(nlog n) operation.

It is possible to do this with O(1) space complexity using the original array to store the heap elements and a single temporary variable.

So how does this compare?  Well, adding the elements to a heap and then placing them back in the array in order is O(nlog n + nlog n) = O(nlog n).  That's a pretty good sort.  On average it is not as fast as [QuickSort](https://www.geeksforgeeks.org/quick-sort/), but it has a **much** better worst-case time complexity, as QuickSort has a worst-case of O(n<sup>2</sup>).  It is also slower than [MergeSort](https://www.geeksforgeeks.org/merge-sort/), but has a better space complexity - O(1) compared to O(n).  

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-secondary

## Dijkstra’s Algorithm

We will later look at [Dijkstra’s algorithm](https://brilliant.org/wiki/dijkstras-short-path-finder/) to find the shortest path in a weighted graph from a starting node to all other points in a graph.

### !end-callout

## Implementation

While you **can** implement a heap with linked TreeNode objects, it can be **much** easier to implement a heap with an array.

Consider if the root is at index 0, the left child could be at index 1, and right index 2.  The child of index 1 would be at index 3 and 4 while the children of index 2 are at 5 and 6... we could write a formula to find the children of a node at index _i_.

```python
left_child = i * 2 + 1
right_child = i * 2 + 2
```

So this heap:

![Heap Diagram](images/heap.png)

In Array format:

![Heap as an Array](images/heap-as-array.png)

### Adding An Element

To add an element to a heap, you place it into the end of the array (or the next logical leaf).  Then you do a "heap-up" operation comparing the new node to its parent and swapping them if they are out of order.  Then, if a swap occurred, repeat the operation using the new node's updated location.

Below is an example of adding a node to a heap.

![heap-up diagram](images/heap-up.png)

When finished the heap could look like this.

![Heap-up finished diagram](images/add-element-finished.png)

Pictured with an array it would look like this:

![heap-up with an array](images/heap-up-array.png)

The add method would look like this:

```python
# This heap is sorted by key-value pairs
def add(self, key, value)
    self.store.append(HeapNode.new(key, value))

    # Compare the new node with it's parent
    # If they are out of order swap and heap-up
    # using the parent's index number.
    # Implementation not shown purposefully.
    self.heap_up(self.store.length - 1)
```

**Exercise:** Write pseudocode for the heap-up method using an array implementation for a heap.  Then compare your steps with your neighbor.

#### Add Node Time Complexity

Adding a value to the end of the array is an O(1) operation (assuming the array is large enough).  Performing the heap-up operation will at worst-case perform 1 swap per level of the heap.  Since there are `Log n` levels to the heap, then adding a node is a O(log n) operation.

### Removing An Element

Removing an element in some ways works in the opposite manner of adding an element.  To remove an element you can swap the last leaf with the root.  Then compare the new root with its children and swap to maintain the heap order in an operation called heap-down.  The heap down operation is repeated until a leaf node is reached or no swaps are made.

1. First, swap the last leaf & the root node

![Initial swap for remove](images/heap-remove-1.png)

2. Delete the last leaf (last item in the array)

![Heap delete node](images/heap-delete.png)

3. Then heap-down the new root, to reestablish the heap property

![Initial swap for remove](images/heap-remove-2.png)

4. Then you should have a new, slightly smaller heap

![Initial swap for remove](images/heap-remove-3.png)

So removing a node could be done with:

```python
def remove(self):
    if self.store.empty?
      return nil

    self.swap(0, self.store.last - 1)
    result = self.store.pop()

  # heap_down is specifically not
  # implemented here
  # start heap_down with the root (index 0)
  self.heap_down(0) unless self.store.empty?
  return result


def swap(self, index_1, index_2)
    temp = self.store[index_1]
    self.store[index_1] = self.store[index_2]
    self.store[index_2] = temp
```

Looking at it as an array:

![heap up with an array 1](images/heap-down-array-1.png)

![heap up with an array 2](images/heap-down-array-2.png)

With the result:

![heap up with an array 3](images/heap-down-array-3.png)


**Exercise:** Write pseudocode to implement the heap_down operation.  Note that you will need to verify that you may swap all the way down to a leaf node.

<!-- available callout types: info, success, warning, danger, secondary, star  -->
### !callout-info

## Sidenote: The System Heap

When you allocate memory dynamically with `.new` or `malloc` in C, the operating system allocates the memory from something called [Heap Memory](https://www.geeksforgeeks.org/stack-vs-heap-memory-allocation/).  This is **not** the same as the heap data structure.  Instead it's considered a "heap" of memory, like clothes in the laundry basket is a heap of clothes.  

### !end-callout

## Summary

Heaps are a data structure to maintain elements in order.  They can be diagramed as a complete tree, but are often implemented as an array.  Each array element can represent one node in a binary tree.  

Adding a node involves placing a node in the next available leaf node and then conducting a series of swaps with its parent until heap order is achieved.  Removing an element involves swapping the last leaf with the root of the heap, removing the last leaf, and then swapping the updated root with its children until a valid heap realtionship is established.  

## Resources

- [Basecs on Heaps](https://medium.com/basecs/learning-to-love-heaps-cef2b273a238)
- [Basecs on Heapsort](https://medium.com/basecs/heapify-all-the-things-with-heap-sort-55ee1c93af82)
- [Geeks for Geeks on Heaps](https://www.geeksforgeeks.org/heap-data-structure/)