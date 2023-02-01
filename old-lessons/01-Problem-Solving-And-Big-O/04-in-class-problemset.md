# Activity:  Problem Solving

## Goal

Our goal is to practice taking a problem, analyzing it, and then refactoring it to improve the solution. 

## Activity Instructions

- [Activity Replit](https://replit.com/@adadev/two-sum-II#README.md)

### Getting Started

In small groups of 3-4, **one student** will *fork* the given replit and then share a collaboration link with the rest of the team. 

### Read The Markdown Document

Read the replit markdown document to understand the problem. The problem **has already been solved.**  However the solution is a brute-force apprach. You can improve it.

### Read Through the Solution

Read through the solution and analyze the time/space complexity.  Fill in the time complexity below.

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- prettier-ignore -->
### !challenge
* type: multiple-choice
* id: 7785c9bb-d328-4325-a6d9-70a42e540bec
* title: What is the time complexity of the initial solution?
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
<!-- * topics: [python, pandas] (optional the topics for analyzing points) -->

##### !question

Look at the `two_sum/two_sum.py` file.  What is the time complexity of the initial solution presented here?

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n^2)
* O(n^3)


##### !end-options

##### !answer

* O(n^2)

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- prettier-ignore -->
### !challenge
* type: multiple-choice
* id: d55b51b1-29dc-47b9-83d7-5a7004bec8db
* title: What is the *space* complexity of the initial solution?
* topics: python, big-o, space-complexity

##### !question

Look at the `two_sum/two_sum.py` file.  What is the space complexity of the initial solution presented here?

##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n^2)
* O(n^3)

##### !end-options

##### !answer

* O(1)

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

### Look For Additional Test/Input Cases

Look at the test file and try to identify at least 1 additional edge-case. Write that as a test-case and verify the solution works.

### Refactor the Solution

Then as a team refactor the solution to improve the time complexity. 

*Notice that the input list is already sorted...*

### !callout-danger

## Maintain O(1) Space Complexity

Note, you should maintain O(1) space complexity.

### !end-callout

### Analyze Your Solution

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: 3929f4c7-d049-47f6-968f-9fb0c2098a51
* title: What is the time complexity of your solution?
* points: 1
* topics: python, big-o, searching

##### !question

What is your solution's time complexity?

##### !end-question

##### !placeholder

O( ... )

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: paragraph
* id: b7befc76-ea5d-44ac-bf4c-7e5205567cf0
* title: Summary
* topics: python, big-o, searching

##### !question

Summarize your solution

##### !end-question

##### !placeholder

How does your solution work?

##### !end-placeholder

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->