# The Greedy Approach

<!-- Definition -->
<!-- The algorithm makes the optional s-->
<!-- Greedy algorithms -->

## Introduction
The divide and conquer approach won't work for all problems so it is useful to be familiar with additional techniques we can use to develop algorithms. **Greedy Algorithms** or the greedy approach is another handy strategy and is often used to solve optimization problems.

We can think of a greedy algorithm as a mouse moving through a maze filled with cheese. At each decision point in the maze, the mouse will choose the path that provides the tastiest cheese. The mouse can't see the entire problem; it chooses its path using only the information available at the moment (which fork in the road offers the tastier cheese?)
without regard for future consequences. Greedy algorithms _hope_ that by making a locally optimal choice at each step, they arrive at an optimum solution for the larger problem, but it does not always work out.

In the diagram below, we can see that the mouse successfully makes it out of the maze by using the greedy approach. 

![Greedy Algorithm - Mouse Analogy Visualization](images/greedy-mouse-maze.png)

However, if a maze route that ended in a dead-end offered tastier cheese, the mouse could just as easily end up lost in the maze!

![Unsuccessful Greedy Algorithm - Mouse Analogy Visualization](images/greedy-mouse-maze-unsuccessful.png)

## Applications of Greedy Algorithms

Although greedy algorithms don't always provide the most optimal or even correct solution there are many cases where they do!

We have actually already seen a successful greedy algorithm in practice. [Dijkstra's Algorithm](./../09-graphs-p2/02-dijkstra.md) uses a greedy approach and is proven to always return the shortest path between two connected nodes in any graph with non-negative weights.

### Dijkstra's as a Greedy Algorithm

Why is Dijkstra's a greedy algorithm? 

Let's first recall how Dijkstra's works. At a high level, Dijkstra's works by initially overestimating the distance from the start node to every other node in the graph. Then, as the algorithm traverses the graph and finds new paths to each destination node, it uses the weights of the edges of these new paths to revise its estimates for the shortest distance to each destination node.

In the example below, the shortest distance to nodes B, D, and E were all estimated as infinity. But as the algorithm traverses the edges from the start node A to each of these B, D, and E, it sees that there is a shorter path available and updates the estimates accordingly. 

![Edge relaxation in Dijkstra's](./images/dijkstras-2.png)

What makes Dijkstra's a greedy algorithm is the order in which it conducts its traversal of the graph. At each step, Dijkstra's chooses which node to visit next by picking the node that is _currently least expensive to visit_. Since we are trying to find the minimum cost path, this is the optimal choice at that point. At each step in the traversal, Dijkstra's doesn't necessarily have all information about the weights of every edge in the graph and all possible paths to each node, making its choices locally optimal decisions. It doesn't consider how paths beyond what it has looked at so far will impact the solution.

In the example below, Dijkstra's chooses to visit Node D next because it is currently estimated to be the closest of all the unvisited nodes.

![Choosing the next closest node in Dijkstra's](./images/dijkstras-3.png)

For a more detailed review of Dijkstra's, take a look at the pseudocode below.

<details>
   <summary>Dijkstra's Pseudocode</summary>

```
- Create a distances list equal in length to the number of nodes in the graph
    - Tracks the minimum cost/distance from start node to each node in graph
    - Initialize each value to infinity
    - Initialize distances[start_node] to zero
- Create a previous list equal in length to the number of nodes in the graph
    - Tracks the previous node in each node's shortest/minimum cost path
    - Initialize each value to None since we have not yet traversed any paths
- Create a visited list to track which nodes have already been visited
- Create a priority queue and add the start node to it
- While the queue is not empty:
    - Set current as node in the queue with minimum cost
    - Add current to the list of visited nodes
    - loop through all the current node's neighbors
        - if the neighbor has not yet been visited:
            - calculate distance from start node to neighbor via current node
            - If calculated distance < distance[neighbor]
                - distance[neighbor] = calculated distance
                - previous[neighbor] = current_node
            - queue.append(neighbor)
- Return the previous and distances list
```

</details>

### Generalizing Greedy Algorithms

We mentioned previously that the greedy approach works well for some problems but not all problems. How do we know when greedy algorithms will be successful? Most problems which can be solved with a greedy algorithm will have the following two characteristics.

#### Greedy Choice Property

Greedy algorithms follow the **greedy choice property** which says that the globally optimal solution to a problem can be found by making the best choice available to it in the moment for the current subproblem. Choices can be made based on information that has been gathered thus far but may not depend on future choices or consider solutions that have not yet been explored. After making the locally optimal choice, the algorithm never looks back and reconsiders that choice. It only moves forward with making new choices.

We have already noted that Dijkstra's makes the greedy choice at each step by choosing the node it believes is least far from it in the moment. In making this choice, it considers the edges and nodes it has traversed thus far to evaluate which unvisited node is the next nearest. However, it does not try and peek at paths beyond those it has already traversed or whether the estimated distance for any of the unvisited nodes will change in the future. 

Notice in the example below, it will choose Node D next because after traversing the edges of the current node, Node A, it finds Node D is the nearest node to the start node, also Node A. However, it doesn't consider whether the distance to other nodes will ultimately be updated. Note that it currently thinks the distance to Node B is 10, when the actual shortest distance from Node A to Node B is 8. 

![Dijkstra's makes locally optimal choice](./images/greedy-choice-property-dijkstra.png)

Once Dijkstra's visits a node, the path to that node is set. Per the greedy choice property, Dijkstra's never goes back and revisits that node. While there are other paths to Node D, they won't be considered because Dijkstra's only ever considers revising the minimum path when looking at the current node's _unvisited_ neighbors. 

In the visualization of Dijkstra's below, observe that the distance to a node does not change once it has been visited. 

![Paths to visited nodes are set](./images/dijkstras-example.gif)

### Optimal Substructures
Most algorithms where the optimal solution is greedy will be **optimal substructure** problems. A problem with an optimal substructures is one in which the optimal solution to the overall problem is made up of the optimal solution to each of its subproblems.

For Dijkstra's, observe that the optimal path between two nodes is made up of optimal paths between any intermediary nodes. 

In the example below, the shortest path from Node A to Node E contains intermediary nodes B & D. It is made up of the following subpaths:
- Node A to Node B
- Node B to Node D
- Node D to Node E

![optimal substructure in Dijkstra's](./images/optimal-path.png)

Notice that the path from Node A to Node E is made up of the optimal solution for each subpath. In particular, observe that the optimal solution for the minimum cost path from Node B to Node D is the direct edge between the two nodes rather than the path from Node B -> Node C -> Node D. Likewise, the overall solution uses the direct edge from Node B to Node D and ignores Node C. 



#### Developing Greedy Algorithms - The Coin Change Problem

## Benefits of Greedy Algorithms


## Drawbacks to Greedy Algorithms

There are many problems that greedy algorithms will not solve. 

You may have noticed that we mentioned above several examples had been proven. But how was it proven ? The 

## Summary
