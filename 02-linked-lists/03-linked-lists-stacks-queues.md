# Applications of Linked Lists

## Overview

Linked lists have a variety of practical applications. Imagine a playlist in your favorite music application. Each song in the playlist represents a node in a doubly linked list. We can add new songs onto the end of our playlist in O(1) time. As we listen to our playlist, it is very easy to replay or skip a song using our previous and next pointers. 

We might also imagine the undo and redo functions of a word processor or other software. Each change to our word document is stored in a node in a doubly linked list. We can undo and redo our changes by traversing our list backwards and forwards.

Linked lists are also prove useful when implementing many other data types that fall into a category called _abstract data types_.

## Abstract Data Types

An _Abstract Data Type_ (ADT), is a type of object which is described by the methods it has and how they perform. Implementation details are not included.  You could for example create a `List` class. You can provide methods to add elements and retrieve elements at a given index. The user of your class never needs to know if you used an array or linked list to store the information internally. The class is called _abstract_ because the data structure's description is independent from it's implementation.  

Linked lists are not considered abstract data types, because a key feature of a linked list is that is implemented by linking nodes together in a chain. However, as mentioned previously, linked lists are often used to implement abstract data types.

Two abstract data types often implemented with linked lists are stacks and queues. Stacks and queues are, like linked lists, ordered linear collections of data. Unlike linked lists, they are described by what they do, rather than how they are implemented. This means that while we might choose to implement stacks and queues with a linked list, we could also choose to implement them with an array.


## Stacks

## Queues


## Abstract Data Types



