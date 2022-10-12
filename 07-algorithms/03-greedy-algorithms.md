# The Greedy Approach

<!-- Definition -->
<!-- The algorithm makes the optional s-->
<!-- Greedy algorithms -->

## Introduction
The divide and conquer approach won't help us solve all problems so it is useful to be familiar with additional techniques we can use to develop algorithms. **Greedy Algorithms** or the greedy approach is another handy strategy and is often used to solve optimization problems.

We can think of a greedy algorithm as a mouse moving through a maze filled with cheese. At each decision point in the maze, the mouse will choose the path that provides the tastiest cheese. The mouse can't see the entire problem, it chooses its path using only the information available at the moment (which fork in the road offers the tastier cheese?)
without regard for future consequences. Greedy algorithms _hope_ that by making a locally optimal choice at each step, they arrive at an optimum solution for the larger problem, but it does not always work out.

In the diagram below, we can see that the mouse successfully makes it out of the maze by using the greedy approach. 

[Greedy Algorithm - Mouse Analogy Visualization](images/greedy-mouse-maze.png)

However, if a maze route that ended in a dead-end offered tastier cheese, the mouse could just as easily end up lost in the maze!

[Unsuccessful Greedy Algorithm - Mouse Analogy Visualization](images/greedy-mouse-maze.png)

## Applications of Greedy Algorithms



#### Greedy Example 1 - Sorting

One example of a greedy sorting algorithm is this `greedy_sort` method.  In this method any time it finds an element smaller than the current element, it will swap.  

```python
def greedy_sort(numbers):
    for i in range(len(numbers)):
        for j in range(i+1, len(numbers)):
            if(numbers[i] > numbers[j]):
                swap(numbers, i, j)
    return numbers
```

**Question** Compare the `greedy_sort` with `selection_sort` below.  Which will end up making fewer swaps?

```python
def selection_sort(numbers):
    for i in range(len(numbers) - 1):
        min = i
        for j in range(i, len(numbers)):
            if numbers[min] > numbers[j]:
                min = j
        swap(numbers, min, i)
    return numbers
```

#### Greedy Example 2 - Merging Sorted Lists

In this problem you are given `k` sorted arrays of varying lengths and asked to merge them.  The greedy approach is to merge the smallest two arrays, then the next two smallest, including the merged result.

For example, suppose you had arrays a, b, and c which have 30, 20 and 15 elements each.  The greedy approach would be to merge arrays b & c, which would take 35 iterations, then merge the result with array a, which would take 65 iterations, for a total of 100.  If you had merged arrays a and b first, that would take 50 iterations, and then merging array c would take 65, for a total of 115 iterations.  

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: short-answer
* id: a6405591-60d6-4ae7-9cf8-fdbe87965b37
* title: Can you think of another way to solve this problem?
* points: 1
* topics: algorithms, greedy

##### !question

Can you think of another way to solve this problem?

##### !end-question

##### !placeholder

Another approach

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

##### !hint

Could a heap be used?

##### !end-hint

##### !explanation

You could also use a heap to solve this by adding the 1st element of each list to a min-heap, then removing the root value from the min-heap and adding the next element in the list from which it came into the heap, and repeating until the heap is empty.  This can be done in O(n log k) time where n is the total number of elements in all of the arrays and k is the number of arrays.

##### !end-explanation

### !end-challenge
