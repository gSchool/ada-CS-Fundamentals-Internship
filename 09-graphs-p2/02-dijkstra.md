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
Step 3. We visit the next node in the queue, B. Exactly the same as step 2, we look at Node B's edges.

Node B's only edge is to Node C. Notice that Node C is not a direct neighbor of our start node, Node A. Because we are interested in calculating the minimum cost to get from Node A to Node C, when considering whether we should revise our current estimation of the cost, we need to sum the cost of the edge from Node B to Node C and whatever the cost to get from Node A to node B is. 

From the work we did in Step 2, we know the cost to get to node B is 10. The weight of the dedge from Node B to C is 2. 10 + 2 = 12 which is less than the current estimate of infinity so we revise our estimate of the minimum cost to travel from Node A to Node C to be 12. 


We update the queue, list of visited nodes, and list of distances as needed.

```
current: B

visited nodes: A, B 

queue: D, E, C

distances:
    - A: 0
    - B: 10
    - C: 12
    - D: 3
    - E: 6
    - F: ∞
```
![Dijkstra's Walkthrough Part 4](./images/dijkstras-4.png)
Step 4. 
![Dijkstra's Walkthrough Part 5](./images/dijkstras-5.png)
Step 5.
![Dijkstra's Walkthrough Part 6](./images/dijkstras-6.png)
Step 6.
![Dijkstra's Walkthrough Part 7](./images/dijkstras-7.png)
Step 7.


### Backtracking

### Pseudocode
```
pseudocode
```


### Challenge

### Dijkstra's with a priority queue

We can improve the performance of Dijkstra's by using a priority queue instead of a regular first-in-first-out queue. 




## Limitations of Dijkstra's

Dijkstra's _does not work_ for graphs with negative weights. To find the shortest path in a graph with negative weights we can use the [Bellman Ford algorithm](https://www.programiz.com/dsa/bellman-ford-algorithm). This algorithm is outside the scope of our curriculum and appears only very occasionally in interviews for SDE1 positions, but we encourage you to follow your curiosity.
