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
* If a tree is balanced its time complexities for insertion, deletion, and searching are O(log n).

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

What if you added 4 nodes and kept the tree unbalanced. How many comparisons would you need to make?

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

If a tree is _balanced_ then the adding, finding, and removing operations on that tree perform in O(log n) time.  However if a tree becomes unbalanced the efficiency can approach O(n) time complexity.  

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