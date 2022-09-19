## Graph Algorithms

There are a huge [class of algorithms](https://en.wikipedia.org/wiki/Category:Graph_algorithms) involving graphs.  We will look at two of the most common graph algorithms as a sample.  

### Breadth-First-Search

Like in a Binary Search Tree a breadth-first-search in a graph is performed with a queue.  However because a graph can, and likely will have a cycle, unlike a tree we need to keep track of the nodes we have visited.  

In breadth-first-search we start with a particular node and visit each node connected to the starting point in the graph starting with the closest node to the starting point and expanding outward.

We do so by adding each of the neighbors of the starting node to a Queue and then loop through the Queue removing an element and repeating the process with the neighbors of the current node.

You can see breadth-first-search animated on [HackerEarth](https://www.hackerearth.com/practice/algorithms/graphs/breadth-first-search/visualize/)

Breadth first search is a solution in a variety of problems including:

- Finding the shortest path in a graph/maze
- Solving puzzle games like a [Rubik's Cube](https://www.quora.com/How-can-solving-a-Rubiks-Cube-be-framed-as-a-graph-problem)
- Checking to see if a graph is connected

**Questions**

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 3398d942-7078-4567-9b81-67bb6c38d104
* title: Iterative Breadth First Search
* points: 1

##### !question

Write a function returning a list of elements which represent a breadth first search of the items in the `adjacency_dict`.

##### !end-question

##### !placeholder

```py
class Graph:
    
    # The graph is stored in an adjacency dictionary where each key 
    # represents an item in the graph and each value in the dictionary
    # corresponds to a list of edges from the key
    def __init__(self, adjacency_dict = {}):
        self.adjacency_dict = adjacency_dict

    def bfs(self):
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_bfs_one(self):
        adjacency_dict = {
            "Seattle": ["Portland", "Chicago"],
            "Portland": ["Seattle", "Hawaii"],
            "Chicago": ["Seattle"],
            "Hawaii": ["Portland"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Chicago", "Hawaii"]
        self.assertEqual(answer, g.bfs())

    def test_bfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.bfs())
```

##### !end-tests

##### !hint

**Pseudocode**

1. Start by grabbing the first item in the adjacency dictionary `start_node`
1. Create a list of nodes called `visited`
1. Create an empty queue `q`
1. Add `start_node` to `q` and `visited`
1. While `q` is not empty:
    1. Remove an element from `q` and store it in `current`
    1. Loop through each of `current`'s neighbors:
        1. If the neighbor is not in `visited`:
            1. Add the neighbor to `visited`
            1. Add the neighbor to `q`
<br>
Still feeling stuck? Check this video walkthrough of the solution.

<!-- Insert link to video explanation here -->

### !end-hint

### !explanation 
An example of a working implementation:

```python
def bfs(self):
    graph = self.adjacency_dict
    
    if len(graph) == 0:
        return []
        
    first_item = list(graph.keys())[0]
    queue = [first_item]
    visited = [first_item]
        
    while queue:
        current = queue.pop(0)
        
        for neighbor in graph[current]:
            if neighbor not in visited:
                visited.append(neighbor)
                queue.append(neighbor)
                
    return visited
```
### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 7b46c76f-c47e-4ed1-8606-732c610a1eaa
* title: Time complexity of BFS
* points: 1
* topics: graphs

##### !question

What is the time complexity of Breadth-First-Search with N nodes and E edges.

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)

##### !end-options

##### !answer

* O(N + E)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Since you will visit each node once, and loop through each of the edges in each node the Big-O of this algorithm is O(N + E) where `N` is the number of nodes in the graph and `E` is the number of edges since each node and each edge will be explored.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 4376fdea-ebec-4fdc-897d-21fc7ca5ff91
* title: Space Complexity of BFS
* points: 1
* topics: graphs

##### !question

What is the space complexity of Breadth-First-Search with N nodes and E edges?

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)


##### !end-options

##### !answer

* O(N)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

In the worst-case you will need to add each node to the Queue, so the space complexity is O(N) where `N` is the number of nodes in the graph.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->


### Depth-First-Search

Where breadth-first-search spreads out from a starting node in order of distance from the starting node, depth first search follows each path as far as possible before backing up and following the next closest path.

**Pseudocode**

1. Starting with a graph's adjacency list and a starting node `s`
1. Create a Stack called `stack`
1. Create a list of nodes called `visited` and mark each element `false`
1. Push `s` into `stack`
1. mark `s` as `true` in `visited`
1. while `stack` is not empty
    1. Remove an element from `stack` and store it in `current_node`
    1. Loop through all the neighbors of `current_node`
        1. If they are not marked as `true` in `visited`
            1. Push the neighbor into `stack`
            1. Mark the neighbor as `true` in `visited`


**Questions**

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 72fd7b4f-2d0b-4f60-9f99-57ede4dc769b
* title: Time complexity of DFS
* points: 1
* topics: graphs

##### !question

What is the time complexity of Depth-First-Search with N nodes and E edges?

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)


##### !end-options

##### !answer

* O(N + E)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

Since you will visit each node once, and loop through each of the edges in each node the Big-O of this algorithm is O(N + E) where `N` is the number of nodes in the graph and `E` is the number of edges since each node and each edge will be explored.  Note, this is the same as breadth-first-search.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: ac56a302-147e-44bd-9438-3779d9fe226a
* title: Space complexity of DFS
* points: 1
* topics: graphs

##### !question

What is the space complexity of Depth-First-Search?

##### !end-question

##### !options

* O(N)
* O(E)
* O(NE)
* O(N + E)
* O(1)

##### !end-options

##### !answer

* O(N)

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

In the worst-case you will need to add each node to the Stack, so the space complexity is O(N) where `N` is the number of nodes in the graph.

##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

[HackerEarth](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/visualize/) has an excellent description and visualization of the algorithm.

Depth-First-Search has a number of applications in graph problems including:

- Detecting a cycle in a graph
- Finding a path in a maze where there is only one correct path
- Scheduling jobs based on dependencies on other jobs


## Summary

In this lesson we have looked at the Graph data structure.  A graph is a collection of nodes and connections between nodes called edges.  Binary search trees and linked lists are both subsets of graphs.  A graph can have both unweighted and weighted edges.  In a weighted graph, each connection is assigned a cost or weight.  Further a graph can be directed or undirected.  In a directed graph an edge is not bidirectional.  

There are two main ways to represent a graph.  The first is using an adjacency matrix which is a 2-dimensional array where each entry represents an edge between the nodes indicated by it's row and column indices.  An adjacency matrix is very quick to lookup a connection between two nodes.  On the other hand retrieving a list of all the edges a node has a time complexity of O(N) where `N` is the number of nodes.  It also require O(N<sup>2</sup>) space complexity.  The other method of representing a graph involves an adjacency list, which is an array of lists of neighbors.  This method has an O(1) time complexity to look up all the neighbors of a node, but O(d) to lookup a particular connection where `d` is the degree of the node, or the number of neighbors it has.  It also requires less space complexity.

There are a number of algorithms involving graphs in computer science.  To traverse a graph you can either make a breadth-first-search or a depth-first-search.  In a breadth-first-search each node is investigated by it's proximity to the starting node.  In a depth-first-search a path is explored as far as it will go, and then the algorithm backs up until another subpath can be explored, like a mouse exploring a maze.

In weighted graphs, finding the shortest paths is a common problem.  One classic solution is Dijkstra's algorithm which is a good example of a greedy algorithm.
