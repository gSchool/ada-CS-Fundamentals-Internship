# Dijkstra's Algorithm

## Overview 

We have observed that a breadth first search traversal of a tree allows us to find the shortest path between any two nodes in an unweighted graph. In an unweighted graph, the length of a path is equal to the number of the edges in the path.

With a weighted graph, finding the shortest path between two nodes looks slightly different. We consider the weight of each edge to be the 'length' or 'distance' of the edge. We calculate the total length of a path by summing the weights of all the edges that make up at the path.

Below are two versions of the same graph: the version on the left is unweighted and the version on the right is unweighted.

Say we want to find the shortest path from Node B to Node D. In the unweighted graph, the shortest path would be along the direct edge from B to D for a path of length 1. 

However, in the weighted graph, we the shortest path from Node B to Node D travels from Node B to Node A, from Node A to Node C, and finally from Node D. The combined length of the path is the sum of the corresponding edges: 2 + 1 + 1 = 4. Because the edge directly between Node B to Node D has a weight or length of 10, it is considered a longer path even though it is a more direct route. 

![Weighted v Unweighted Graph Comparison](./images/weighted-v-unweighted.png)

Because of the change in how we calculate shortest paths when weighted edges exist, we are not able to use breadth first search to find the shortest path in weighted graphs. We need a new algorithm: Dijkstra's. 

## Dijkstra's Algorithm
<!-- Video -->

Dijkstra's algorithm takes a weighted graph and determines the least costly path from a specified start node to every other _reachable_ node in the graph.


Dijkstra's algorithm works by initially overestimating the cost to travel from the start node to every other node in the graph. It then operates similarly to breadth first search. Beginning at the given start node, Dijkstra's algorithm visits each direct neighbor of the current node. As it visits new nodes, the algorithm uses the weights of the corresponding edges to adjust the original estimated cost to each neighbor. 

We can see how it works in more detail with an example. The video walkthrough of this example is included at the top of this section.

![Dijkstra's Walkthrough Part 0](./images/dijkstras-0.png)
Step 0. We start with a weighted graph. 

![Dijkstra's Walkthrough Part 1](./images/dijkstras-1.png)
Step 1. We identify our start node, in this example Node A, and set the cost to travel from the start node to all nodes except itself to infinity, an obvious overestimation. The distance of the start node to itself is set to 0.

In the diagram above, the costs are denoted in magenta. 

```
current: A

costs/distances:
    - A: 0
    - B: ∞
    - C: ∞
    - D: ∞
    - E: ∞
    - F: ∞
```
![Dijkstra's Walkthrough Part 2](./images/dijkstras-2.png)
Step 2. We look at each of the edges of the start node, Node A. For each of Node A's edges, we check if the cost to travel along that edge to its neighbor is less than the current estimate of the cost to reach that neighbor. If so, we reset the distance of that neighbor to be equal to the weight of the edge. Since at this point in our traversal, all of the nodes have an estimated cost of infinity, the cost of travelling to each of Node A's neighbors will decrease.

For example, in the diagram above the edge from Node A to Node B has a weight of 10. 10 is clearly less than our current estimate of the cost from Node A to B, infinity, so we reset the cost of travelling from Node A to Node B to 10. 

We add our start node to a list of visited nodes, and the neighbors of our start node to the queue of nodes that still need to be visited. 

In the diagram above, visited nodes and edges are identified in teal. 

```
current: A

visited nodes: A 

queue: B, D, E

costs/distances:
    - A: 0
    - B: 10
    - C: ∞
    - D: 3
    - E: 6
    - F: ∞
```
![Dijkstra's Walkthrough Part 3](./images/dijkstras-3.png)
Step 3. We visit the next node in the queue, B. Exactly the same as step 2, we look at Node B's _untravelled_ edges.

Node B's only unvisited edge is to Node C. Notice that Node C is not a direct neighbor of our start node, Node A. Because we are interested in calculating the minimum cost to get from Node A to Node C, when considering whether we should revise our current estimation of the cost, we need to sum the cost of the edge from Node B to Node C and whatever the cost to get from Node A to node B is. 

From the work we did in Step 2, we know the cost to get to node B is 10. The weight of the dedge from Node B to C is 2. 10 + 2 = 12 which is less than the current estimate of infinity so we revise our estimate of the minimum cost to travel from Node A to Node C to be 12. 


We add Node B to the list of visited nodes and update the queue with all Node B's unvisited neighbors.

```
current: B

visited nodes: A, B 

queue: D, E, C

costs/distances:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: ∞
```
![Dijkstra's Walkthrough Part 4](./images/dijkstras-4.png)
Step 4. Now we look at the next node in the queue, Node D. 

Node D has two unvisited neighbors, Nodes C and F. Following the same logic as in Step 3, we sum the cost of to travel from the start node to Node D, 3, with the sum of the edge from Node D to each of its neighbors. In this case, each of those sums is less than the current estimates so we revise our list of estimated costs accordingly.

As before, we update the queue and list of visited nodes as needed.

```
current: D

visited nodes: A, B, D 

queue: E, C, C, F

costs/distances:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: 15
```

![Dijkstra's Walkthrough Part 5](./images/dijkstras-5.png)
Step 5. We move on to the next node in the queue, Node E. 

Node E's only unvisited neighbor is Node F. The minimum cost to travel from Node A to Node F is currently estimated to be 15 via the path from Node A -> Node D -> Node F. 

The sum of the cost to travel from Node A to Node E plus the cost to travel along Node E to Node F is 8. The cost of this new path 8 is less than that of the previously found path 15, so we revise our costs/distances list to reflect our new minimum cost.

We add Node E to the list of visited nodes, and its unvisited neighbor, Node F, to the queue.

```
current: E

visited nodes: A, B, D, E 

queue: C, C, F, F

costs/distances:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: 15
```

![Dijkstra's Walkthrough Part 6](./images/dijkstras-6.png)
Step 6. We move on to the next node in the queue, Node C. 

Node C's neighbors Node B and Node D have already been visited, so we do not need to perform any other further calculations.

We add Node C to the list of visited nodes. Node C has no unvisited neighbors so we do not need to add anything to the queue.

In fact, we can move on to the next node in the queue. Notice that the next node in the queue is also Node C. Because Node C has now also been visit it, we are free to skip over it and move on to the next node in the queue, Node F.

```
current: C

visited nodes: A, B, D, E, C 

queue: C, F, F

costs/distances:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: 15
```

![Dijkstra's Walkthrough Part 7](./images/dijkstras-7.png)
Step 7. Now we are visiting our final unvisited node, F. Like Node C, Node F has no unvisited neighbors. 

We are free to pop it off the queue and move on. 
```
current: F

visited nodes: A, B, D, E, C, F

queue: F

costs/distances:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: 15
```

Like Node C, Node F was in the queue twice. By looking at the list of visited nodes above, we can observe that we have visited all nodes in the given graph. We pop this second instance of Node F and have our final list of costs/distances. Dijkstra's algorithm is complete!

```
Minimum costs/distances from Node A to each node in the graph:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: 15
```

### !callout-info

## Priority Queues
You may recall that when we first introduced [queues](../02-linked-lists/03-linked-lists-stacks-queues.md), we said queues remove elements in first-in-first-out (FIFO) order. 

<break>

However, in our walkthrough above, we prioritized removing elements from the queue based on minimum cost. This is a special type of queue called a **minimum priority queue**. There are also maximum priority queues where elements are removed in order of maximum cost/priority. 
<break> 
We will use the [`heapq`](https://docs.python.org/3/library/heapq.html) module in Python as our priority queue when we implement Dijkstra's. The internals of implementing a priority queue, also called a heap, are beyond the scope of this course, but we encourage you to follow your curiosity!
### !end-callout

### Pseudocode
The process outlined above can be generalized as pseudocode.

Before jumping into the pseudocode, observe that to find the cost of a path from Node A to a non-neighboring node D, we needed to know the cost of travelling from Node A to Node D's direct neighbor along that path.

In the example below, say we want to find the cost of the path from Node A to Node D. Node D's neighbor along that path is Node C. We could also say that Node C is the _previous_ node along that path. 

Observe that the cost to get from Node A to Node D is the cost to get from Node A to Node C plus the cost to get from Node D to Node C. 

![Previous Node in a Graph Example](./images/dijkstra-subpath.png)

This observation illustrates that when calculating the costs of a path between two non-neighboring nodes as we may need to do in Djikstra's requires us to know the previous node of the end node in the path that we are looking at. As a result, when implementing Djikstra's algorithm it can be useful for us to keep track of each node's previous node along its minimum cost path.


The following pseudocode implementation of Djikstra's assumes that we are provided with a graph g and a starting node.
```
- Create three lists, each equal in length to the number of nodes in the graph
    - distances: minimum distances from the start node to each node in the graph
    - visited: tracks which nodes in the graph have been visited
    - previous: tracks the previous node for each node's shortest/minimum cost path]
- Initialize each value in the distances list to infinity.
- Set distances[start_node] to zero.
- Initialize each value in the visited list to False (since none have been visited yet)]
- Initialize each value in the previous list to None (since we have not yet traversed any paths)
- Initialize a queue. Add the start node to the queue.
- While the queue is not empty:
    - loop through all the current node's neighbors
        - if the neighbor has not yet been visited:
            - set that node to visited
            - temp_distance = distance[previous[neighbor]] + graph[current node][neighbor]
            - if temp_distance < distance[neighbor]
                - distance[neighbor] = temp_distance
                - parent[neighbor] = current_node
            - queue.append(neighbor)
    - visited[current_node] = True
- Return the distances list

```
### Challenge
<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: code-snippet
* language: python3.6
* id: ea30a148-cce4-458e-a2f0-9f39de10e354
* title: Dijkstra's
* points: 1
<!-- * topics: [python, pandas] (Checkpoints only, optional the topics for analyzing points) -->

##### !question

Given a graph `g` and a start node `s` implement Dijkstra's Algorithm. 

The graph `g` is given as an adjacency matrix where `adj_matrix[i][j]` has a value equal to the weight of the edg between nodes `i` and `j`. A value of zero indicates that there is no edge between node `i` and `j`. The start node `s` is the index of the node. 

Return a dictionary that has two keys:
  - `previous` whose value is a list of the previous nodes in the shortest path from node `s` to the `i`th node
  - `distances` whose value is the distance/cost of the shortest path from node `s` to e in the the graph `g`.

##### !end-question

##### !placeholder
```py
def dijkstra(g, s):
    pass
```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestPython1(unittest.TestCase):

    def test_with_sample_matrix(self):
        adjacency_matrix = [
            [ 0, 4, 0, 0, 0, 0, 0, 8, 0 ], 
            [ 4, 0, 8, 0, 0, 0, 0, 11, 0 ], 
            [ 0, 0, 7, 0, 9, 14, 0, 0, 0 ], 
            [ 0, 8, 0, 7, 0, 4, 0, 0, 2 ], 
            [ 0, 0, 0, 9, 0, 10, 0, 0, 0 ], 
            [ 0, 0, 4, 14, 10, 0, 2, 0, 0 ], 
            [ 0, 0, 0, 0, 0, 2, 0, 1, 6 ], 
            [ 8, 11, 0, 0, 0, 0, 1, 0, 7 ], 
            [ 0, 0, 2, 0, 0, 0, 6, 7, 0 ] 
        ]
        expected = {
            'previous': [None, 0, 1, 2, 5, 6, 7, 0, 2],
            'distances': [0, 4, 12, 19, 21, 11, 9, 8, 14]
        }

        answer = dijkstra(adjacency_matrix, 0)

        self.assertEqual(answer, expected)

    def test_dijkstra_with_small_graph():
        #Arrange
        adjacency_matrix =[ 
            [0, 4, 0, 0],
            [4, 0, 12, 6],
            [0, 12, 0, 0],
            [0,  6, 0, 0]
        ]

        expected = {
            'previous': [None, 0, 1, 1],
            'distances': [0, 4, 16, 10]
        }

        # Act
        answer = dijkstra(adjacency_matrix, 0)

        #Assert
        self.assertEqual(answer, expected)
    
    def test_dijkstra_with_unconnected_graph(self):
        #Arrange
        adjacency_matrix =[ 
            [0, 4, 0, 0],
            [4, 0, 12, 0],
            [0, 12, 0, 0],
            [0,  0, 0, 0]
        ]

        expected = {
            'previous': [None, 0, 1, None],
            'distances': [0,4,15,float('inf')]
        }

        # Act
        answer = dijkstra(adjacency_matrix, 0)
        
        #Assert
        self.assertEqual(answer, expected)

    def test_dijkstra_with_starting_node_other_than_zero(self):
        adjacency_matrix = [
            [0, 4, 0, 0],
            [4, 0, 12, 0],
            [0, 12, 0, 0],
            [0,  0, 0, 0]
        ]

        expected = {
            'previous': [1, 2, None, None],
            'distances': [16, 12, 0, float('inf')]
        }

        #Act
        answer = dijkstra(adjacency_matrix, 2)

        #Assert
        self.assertEqual(answer, expected)
    
    def test_dijkstra_will_report_no_connections_for_starting_at_unconnected_node(self):
        # Arrange
        adjacency_matrix =[ 
            [0, 4, 0, 0],
            [4, 0, 12, 0],
            [0, 12, 0, 0],
            [0,  0, 0, 0]
        ]

        expected = {
            'previous': [None, None, None, None],
            'distances': [float('inf'), float('inf'), float('inf'), 0]
        }

        # Act
        answer = dijkstra(adjacency_matrix, 3)

        #Assert
        self.assertEqual(answer, expected)

    def test_dijkstra_will_return_empty_for_empty_graph(self):
        adjacency_matrix = []

        expected = {
            'previous': [],
            'distances': []
        }

        #Act
        answer = dijkstra(adjacency_matrix, 0)

        #Assert
        self.assertEqual(answer, expected)

    def test_dijkstra_with_unweighted_graph(self):
        adjacency_matrix = [
            [0, 1, 1],
            [1, 0, 1],
            [1, 1, 0]
        ]
        expected = {
            'previous': [None, None, None],
            'distances': [1, 0, 1]
        }

        #Act
        answer = dijkstra(adjacency_matrix, 1)

        #Assert
        self.assertEqual(answer, expected)

    def test_dijkstra_with_weighted_graph(self):
        adjacency_matrix = [
            [0, 10, 1],
            [10, 0, 1],
            [1, 1, 0]
        ]

        expected = {
            'previous': [2, None, None],
            'distances': [2, 0, 1]
        }

        #Act
        answer = dijkstra(adjacency_matrix, 1)

        #Assert
        self.assertEqual(answer, expected)


```

##### !end-tests

<!-- other optional sections -->
##### !hint 

Still feeling stuck? Watch the video solution walkthrough below. 
<!-- Add video walkthrough -->
##### !end-hint
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation 
##### !end-explanation

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Dijkstra's with a priority queue

We can improve the performance of Dijkstra's by using a priority queue instead of a regular first-in-first-out queue. 




## Limitations of Dijkstra's

Dijkstra's _does not work_ for graphs with negative weights. To find the shortest path in a graph with negative weights we can use the [Bellman Ford algorithm](https://www.programiz.com/dsa/bellman-ford-algorithm). This algorithm is outside the scope of our curriculum and appears only very occasionally in interviews for SDE1 positions, but we encourage you to follow your curiosity.
