# Dijkstra's Algorithm

## Overview 

We have observed that a breadth first search traversal of a tree allows us to find the shortest path between any two nodes in an unweighted graph. In an unweighted graph, the length of a path is equal to the number of the edges in the path.

With a weighted graph, finding the shortest path between two nodes looks slightly different. We consider the weight of each edge to be the 'length' or 'distance' of the edge. We calculate the total length of a path by summing the weights of all the edges that make up at the path.

Below are two versions of the same graph: the version on the left is unweighted and the version on the right is unweighted.

Say we want to find the shortest path from Node B to Node D. In the unweighted graph, the shortest path would be along the direct edge from B to D for a path of length 1. 

However, in the weighted graph, we the shortest path from Node B to Node D travels from Node B to Node A, from Node A to Node C, and finally from Node D. The combined length of the path is the sum of the corresponding edges: 2 + 1 + 1 = 4. Because the edge directly between Node B to Node D has a weight or length of 10, it is considered a longer path even though it is a more direct route. 

![Weighted v Unweighted Graph Comparison](./images/weighted-v-unweighted.png)

Because of the change in how we calculate shortest paths when weighted edges exist, we are not able to use breadth first search to find the shortest path in weighted graphs. We need a new algorithm: Dijkstra's. 

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: testable-project
* id: 539dfc0a-a8d7-4e80-ba02-a8babb841cc1
* title: Dijsktra's Algorithm
* upstream: https://github.com/Ada-C16/dijkstra
* validate_fork: true
* points: 0
* topics: graphs

##### !question

Complete the [Dijstra's Algorithm](https://github.com/Ada-C16/dijkstra) project.

##### !end-question

##### !placeholder

Your repo link goes here.

##### !end-placeholder

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: 39c50f28-ca7b-4709-a88c-725e89bdbfa1
* title: Dijsktra's Algorithm
* points: 2
* topics: graphs

##### !question

Place your PR into the box below.

##### !end-question

##### !placeholder

PR Link goes here

##### !end-placeholder

##### !answer

/^https:\/\/github.com\/.*\/pull.*\d$/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

