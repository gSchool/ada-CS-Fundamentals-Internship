## Graph Algorithms

There are a huge [class of algorithms](https://en.wikipedia.org/wiki/Category:Graph_algorithms) involving graphs.  We will look at two of the most common graph algorithms as a sample.  

### Breadth-First-Search

Like in a binary search tree a breadth-first-search in a graph is performed with a queue.  However, unlike trees, graphs often have cycles so we will need to keep track of the nodes we have visited.

### !callout-info

## Cycles in Graphs
In graph theory, a path that starts from a given node and ends at that same node is called a *cycle*. In the graph below, there is a cycle starting from node A -> node B -> node C -> node A.

![graph with cycle](images/directed-graph.png)

### !end-callout

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

Write a function returning a list of elements representing a breadth first search of the items in `self.adjacency_dict`.

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
    def test_bfs(self):
        adjacency_dict = {
            "Seattle": ["Portland", "Chicago"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Hawaii"],
            "Hawaii": ["Portland"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Chicago", "Hawaii"]
        self.assertEqual(answer, g.bfs())

    def test_bfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.bfs())

    def test_bfs_one_item(self):
        adjacency_dict = {
            "Seattle": []
        }
        g = Graph(adjacency_dict)
        self.assertEqual(["Seattle"], g.dfs())
```

##### !end-tests

##### !hint

**Pseudocode**

1. Start by grabbing the first item in the adjacency dictionary `start_node`
1. Create an empty list called `visited`
1. Create an empty queue `q`
1. Add `start_node` to `q` and `visited`
1. While `q` is not empty:
    1. Remove an element from `q` and store it in `current`
    1. Loop through each of `current`'s neighbors:
        1. If the neighbor is not in `visited`:
            1. Add the neighbor to `visited`
            1. Add the neighbor to `q`
1. Return `visited`
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
* O(N^2)
* O(E)
* O(NE)
* O(N + E)
* O(1)

##### !end-options

##### !answer

* O(N + E)

##### !end-answer

##### !explanation

Since we will visit each node once, and loop through each of the edges in each node the Big-O of this algorithm is O(N + E) where `N` is the number of nodes in the graph and `E` is the number of edges since each node and each edge will be explored.

O(N + E) is different from O(NE) because O(NE) implies that we visit each node `E` times. On the contrary, we visit each node at most one time O(N). We examine the edges adjacent to a node only when we visit the node, so each edge is examined at most two times, once for each of the nodes to which it is connected. This gives us a Big-O of O(2E) = O(E). Put together O(N) + O(E) and we get O(N + E).

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

[HackerEarth](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/visualize/) has an excellent description and visualization of the algorithm.

Depth-First-Search has a number of applications in graph problems including:

- Detecting a cycle in a graph
- Finding a path in a maze where there is only one correct path
- Scheduling jobs based on dependencies on other jobs

**Questions**

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: ce448643-59d9-44a8-b2c6-ba4a8a2227e5
* title: Iterative Depth First Search
* points: 1

##### !question

Write a function returning a list of elements representing a depth first search of the items in `self.adjacency_dict`. Please write the function iteratively, i.e. without using recursion.

##### !end-question

##### !placeholder

```py
class Graph:
    
    # The graph is stored in an adjacency dictionary where each key 
    # represents an item in the graph and each value in the dictionary
    # corresponds to a list of edges from the key
    def __init__(self, adjacency_dict = {}):
        self.adjacency_dict = adjacency_dict

    def dfs(self):
        pass
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_dfs(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle"],
            "Portland": ["Seattle", "Hawaii"],
            "Hawaii": ["Portland", "Juneau"],
            "Juneau": ["Hawaii"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Portland", "Hawaii", "Juneau", "Chicago"]
        self.assertEqual(answer, g.dfs())

    def test_dfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.dfs())

    def test_dfs_one_item(self):
        adjacency_dict = {
            "Seattle": []
        }
        g = Graph(adjacency_dict)
        self.assertEqual(["Seattle"], g.dfs())
```

##### !end-tests

### !hint
**Pseudocode**

1. Start by grabbing the first item in the adjacency dictionary `start_node`
1. Create a Stack called `stack`
1. Create an empty list called `visited`
1. Push `start_node` onto `stack`
1. while `stack` is not empty
    1. Pop the stack and store it in `current`
    1. Add `current` to `visited`
    1. Loop through all the neighbors of `current`
        1. If they are not in `visited`
            1. Push the neighbor onto `stack`
1. Return `visited`
<br>
Still feeling stuck? Check this video walkthrough of the solution.

<!-- Insert link to video explanation here -->

### !end-hint 

### !explanation
An example of a working implementation:

```python
def dfs(self):
    graph = self.adjacency_dict
    
    if len(graph) == 0:
        return []
        
    first_item = list(graph.keys())[0]
    stack = [first_item]
    visited = []

    while stack:
        current = stack.pop()
        visited.append(current)

        for neighbor in graph[current]:
            if neighbor not in visited:
                stack.append(neighbor)

    return visited
```
### !end-explanation

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->

### !challenge

* type: code-snippet
* language: python3.6
* id: 243eaf9a-e87e-48f6-bfa0-9df10c5b15d2
* title: Recursive Depth First Search
* points: 1

##### !question

Write a function returning a list of elements representing a depth first search of the items in `self.adjacency_dict`. Please write the function recursively.

##### !end-question

##### !placeholder

```py
class Graph:
    
    # The graph is stored in an adjacency dictionary where each key 
    # represents an item in the graph and each value in the dictionary
    # corresponds to a list of edges from the key
    def __init__(self, adjacency_dict = {}):
        self.adjacency_dict = adjacency_dict

    def dfs(self):
        pass
```

##### !end-placeholder

##### !tests
```py
import unittest
from main import *

class TestPython1(unittest.TestCase):
    def test_dfs(self):
        adjacency_dict = {
            "Seattle": ["Chicago", "Portland"],
            "Chicago": ["Seattle", "New York"],
            "Portland": ["Seattle", "Honolulu"],
            "New York": ["Chicago"],
            "Juneau": ["Honolulu"],
            "Honolulu": ["Portland", "Juneau"]
        }

        g = Graph(adjacency_dict)

        answer = ["Seattle", "Chicago", "New York", "Portland", "Honolulu", "Juneau"]
        self.assertEqual(answer, g.dfs())

    def test_dfs_empty_graph(self):
        g = Graph()
        self.assertEqual([], g.dfs())

    def test_dfs_one_item(self):
        adjacency_dict = {
            "Seattle": []
        }
        g = Graph(adjacency_dict)
        self.assertEqual(["Seattle"], g.dfs())
```

##### !end-tests

##### !hint
**Pseudocode**
1. For base function:
    1. Create empty list called `visited`
    1. Grab the first item in the adjacency graph `first_item`
    1. Call helper function with `visited`, `self.adjacency_dict`, and `first_item`
    1. Return `visited`

1. For helper function (takes in `visited`, `graph`, and `node`):
    1. If `node` is not in `visited`:
        1. Append `node` to `visited`
        1. For each `neighbor` of the `node`:
            1. Call helper with `visited`, `graph`, and the `neighbor`
<br>
What we're essentially doing here is replacing the explicit creation of a stack and taking advantage of the recursive call stack.

##### !end-hint 

##### !explanation
An example of a working implementation:

```python
def dfs_helper(self, visited, graph, node):
    if node not in visited:
        visited.append(node)
        for neighbor in graph[node]:
            self.dfs_helper(visited, graph, neighbor)

def dfs_recursive(self):
    graph = self.adjacency_dict
    if len(graph) == 0:
        return []
        
    visited = []
    first_item = list(graph.keys())[0]

    self.dfs_helper(visited, graph, first_item)
    return visited
```

##### !end-explanation 

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

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


## Summary

In this lesson we have looked at the Graph data structure. A graph is a collection of `nodes` and the connections between nodes are called `edges`. Binary search trees and linked lists are both subsets of graphs.  

Here are some other facts about graphs:
- A graph can have both unweighted and weighted edges.  In a weighted graph, each connection is assigned a cost or weight. 
- A graph can be directed or undirected.  In a directed graph an edge is *not* bidirectional.  

There are a few main ways to represent a graph:
1. Using an adjacency dictionary, which represents the nodes as keys and the edges are represented in a list as the value of the key. This method has an O(1) time complexity to look up the neighbors of the node. We used this representation in the challenges above.
1. Using an adjacency matrix which is a 2-dimensional array where each entry represents an edge between the nodes indicated by it's row and column indices.  An adjacency matrix is very quick to lookup a connection between two nodes.  On the other hand retrieving a list of all the edges a node has has a time complexity of O(N) where `N` is the number of nodes.  It also require O(N<sup>2</sup>) space complexity.  
1. Another method of representing a graph involves an adjacency list, which is an array of lists of neighbors.  This method has an O(1) time complexity to look up all the neighbors of a node, but O(d) to lookup a particular connection where `d` is the degree of the node, or the number of neighbors it has.  It also requires less space complexity.

There are a number of algorithms involving graphs in computer science.  To traverse a graph you can either make a breadth-first-search or a depth-first-search.  In a breadth-first-search each node is investigated by it's proximity to the starting node.  In a depth-first-search a path is explored as far as it will go, and then the algorithm backs up until another subpath can be explored, like a mouse exploring a maze.

In weighted graphs, finding the shortest paths is a common problem.  One classic solution is Dijkstra's algorithm which is a good example of a greedy algorithm. We'll learn more about Dijkstra's algorithm in our next Graph lesson.
