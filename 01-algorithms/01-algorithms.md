# Introduction to Algorithms

<iframe src="https://adaacademy.hosted.panopto.com/Panopto/Pages/Embed.aspx?id=2619c3c1-e6d5-48a1-a199-aad7014dcc4e&autoplay=false&offerviewer=true&showtitle=true&showbrand=false&start=0&interactivity=all" height="405" width="720" style="border: 1px solid #464646;" allowfullscreen allow="autoplay"></iframe>
<!--update video-->


**Note** This video lesson covers algorithms content as it was written for cohorts C16 and prior. Significant changes have been made, and the above videos do not fully align with the updated lesson content. However, they do provide a good general overview of divide and conquer, greedy, and dynamic programming for those who prefer video lessons.


## Learning Goals

By the end of this lesson you should be able to:

- Explain the term algorithm
- Further explain time and space complexity
- Further explain recursion
- Explain two categories of algorithms: _divide and conquer_ and _dynamic programming_

## Video Lesson


- [Slide Deck used for C16](https://docs.google.com/presentation/d/1V4ycrfl3dbL0IbRHqK3ytU45VyMJQNHhyxpc3Ti2e28/edit?usp=sharing)

## What is an an Algorithm?

Before we can discuss different algorithmic strategies, we need to understanding what an algorithm _is_.  An **algorithm** is a finite set of instructions that, if followed, accomplishes a particular task.  We can think of it as a series of steps to accomplish a task.  For example, Google maps has an algorithm to calculate the best route to drive between any two points on map.  

All algorithms must have:

- Input
  - An algorithm may accept zero or more inputs
- Output
  - An algorithm should produce some result
- Clarity
  - Each step in an algorithm should be a clear and unambiguous
- Finiteness
  - An algorithm should end after a finite number of steps. 
  - An algorithm cannot repeat forever (otherwise it doesn't solve a problem)
- Effectiveness
  - It should be possible for a person or computer to fulfill each step in an algorithm and the algorithm should accomplish the given task.

### Algorithms areas of study

The study of computer science is the study of algorithms. At its core, computer science is really the art of devising, analyzing, proving the correctness of, and testing algorithms:

- **Devising** algorithms
  - This is the art of using data structures and design strategies to develop new and useful algorithms
  - It also encompasses optimizing and generalizing existing algorithms
- **Validating** algorithms
  - This is the art of proving the correctness of an algorithm for all possible inputs
  - This is very similar to a mathematical proof
- **Analyzing** algorithms
  - This is identifying the efficency of an algorithm using time and space complexity
- **Testing** algorithms
  - This is really debugging the algorithm  
  - When the algorithm is tested, it is run on sample data. If the tests produce unexpected output, the error causing the unexpected output needs to be debugged
  - Algorithms are also _profiled_ or assessed on their performance measurements by running the algorithm on sample data and measuring performance changes and memory usage.
    - For example [leetcode](https://leetcode.com/) takes your solution to a common programming problem and compares its performance to solutions from other developers

This course will focus on devising, analyzing, and, testing algorithms. We are choosing to focus on these three aspects because they are the skills most often evaluated during technical interviews for junior software developer roles. Validating algorithms is beyond the scope of this course, but feel free to follow your curiosity!

## Devising and Testing Algorithms
Devising algorithms is really just problem solving. So how do we approach solving a new, knotty problem? What steps can we take when we sit down in front of a programming and... have no idea what to do? This lesson describes a systematic approach to problem solving. Notice the similarity to Problem Solving Exercises in the classroom portion of Ada and their equivalent, Interview Practice Questions, in the Thursdays at Ada portion. In follow-up lessons, we will practice using Big-O notation to compare multiple approaches to the same problem.  



