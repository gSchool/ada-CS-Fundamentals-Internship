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

### Areas of Study

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


## Vocabulary and Synonyms

Vocab | Definition | Synonyms | How to Use in a Sentence
:-----:|:-----:|:-----:|:-----:
Nominal Case | A "normal" or typical input to an application. | normal case, typical case| I used `x=5` as the nominal case.
Edge Case | An input that is outside the normal range of inputs. |extreme case, corner case | I used `x=0` as an edge case.


### Steps in Problem Solving

When we look at programming problems - either interview problems or challenges encountered on the job - we can approach the task systematically. Let's examine one particular strategy which involves first ensuring we understand the problem followed by breaking down the larger problem into smaller, more approachable steps and solving each step in turn. Then, we will examine our solution, evaluate how effective it is and attempt to improve upon it.

Our steps are:

* Understand the problem
* Explore Examples
* Break Down the Problem
* Solve or Reduce the Problem
* Simplify/Refactor

These steps are adapted from [George Pólya](https://en.wikipedia.org/wiki/George_P%C3%B3lya) a 20th century mathematician who wrote a book called [How to solve it](https://www.adasbooks.com/book/9780691164076) about how to go about solving math problems.

### Sample Problem

We will walk through the steps of solving a problem using the following sample problem:

*Write a function called `zero_sum_subarray` that takes in a list of integers.*  

*The function should return a 2D list where the outer list contains all contiguous subsequences within the given list that add up to zero.*

### Understand the Problem

When we look at a given problem we need to understand what our code is expected to do.  Without solid understanding of our requirements, we might write code which does not fully address the problem or even write a solution to a different problem entirely!

#### Interview Problems

In an interview problem like `zero_sum_subarray`, we need to carefully examine the question and ask the interviewer follow-up questions to make sure we understand what is expected.

In this interview problem we can examine the problem statement and figure out that we need to:

* Write a function named `zero_sum_subarray`
* The function should take in a list of integers
* The function should find all contiguous subsequences in the given list which add up to zero

The first two points are relatively clear, but the third is a little more tricky.  We need to understand some of the terminology used in the problem.  Using Google or your own knowledge answer the following.

### !challenge

* type: paragraph
* id: f0a7b426-d097-4ae6-a25a-2a0567ef46d9
* title: What do contiguous, subsequence, and 2D list mean?

##### !question

Explain the meaning of the following terms:

* contiguous
* subsequence
* 2D list

Feel free to look up the terms in [Google](https://www.google.com/) or use other resources.

##### !end-question

##### !placeholder


##### !end-placeholder

##### !explanation

* contiguous: Elements of an array/list are contiguous if they are *adjacent to each other in the list and maintain the exact same order*.
* subsequence: A sequence is a subset of a larger sequence in which all the elements of the subsequence are contained in the larger sequence in the *same relative order*. For example, if our larger sequence is the list `[1,2,3,4]`, a subsequence would be `[1,4]` because both `1` and `4` are in each of the two sequences and `1` comes before `4` in each list. `[4,1]` would not count as a subsequence because `1` precedes `4` in the larger list but `1` comes after `4` in the subsequence. Our sequence could also be a string, integer, or another linear series of data. 
* 2D list: A 2D list/2D array is a *list whose elements are all lists*. The containing list is often called the outer list and its elements are referred to as inner lists. Inner lists are often the same length but can also have different lengths.

##### !end-explanation

### !end-challenge

### !callout-info

## Contiguous Subsequence vs Subarray

A contiguous subsequence is also known as a [**subarray**](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)/sublist. Many interviewing problems use the terminology contiguous, subsequence, and/or subarray in the problem statement. 

### !end-callout

### !callout-star

## What if I'm not allowed to use Google?

Ask your interviewer! While it may feel nervewracking to admit you are unfamiliar with a term (or multiple terms!), asking for clarification on unfamiliar terms can also signal that you are a clear communicator, detail-oriented, and collaborative. 

### !end-callout

####  Summarizing Our Understanding

So in this problem we need to write a function `zero_sum_subarray` which takes in a list of integers as parameters and will return all the sublists whose elements add up to zero in an outer list.

### Explore Example Input/Output

Next to ensure we understand the problem we need to develop example inputs and determine what the output *should* be for those given inputs.  In industry this might involve drawing up mock-ups of the program and running through scenarios, or asking a customer or a team member to do so.  It could also involve generating sample input data and determining what the output should be.

In general it's most helpful to develop a few examples which will test the bounaries of what is possible for input.  These are called **edge cases**.

We should consider:

* **Nominal Edge Cases**
  * In this example we could give a list and number which does contain a contiguous sublist which adds up to the given number.
  * For example:  [1, 2, 3, 4] and 7 would return 2 because [1, 2] adds up to 7.
* **Negative Edge Case**
  * In this example we can give a list and a number in which the list does **not** contain a contiguous sublist which adds up to the given number.
    * For example: [1, 2, 3, 4] and 8 would need to return *something* to indicate that there is no contiguous sublist which adds up to the given number.
  * Another Negative Edge Case input would be an array and given number for which there is no valid sublist which adds up to the given value.
    * For example: [6, 7] and 1 would return *something* to indicate there is no contiguous sublist which adds up to the given number.
* **Positive Edge Case**
  * This would be an input on the edge of what is possible which returns a valid length of a contiguous sublist.
  * For example: [1] and 1 would return 1 because [1] is a contiguous sublist which adds up to 1.

### Hey We Found a Problem!

By looking at concrete sample input and output examples, we can see that our problem is not as simple as it seems.  We need to consider cases when the list does not contain a contiguous sublist which adds up to the given number.  We also need to consider cases when the list is empty or contains only one element.

These make **excellent** test cases to use when developing and verifying our code.

For our purposes we will expect the function to return `None` if there is no contiguous sublist which adds up to the given number.  

## Break Down the Problem

Big massive problems are *hard*.  As developers we often find it easier to break down the problem into smaller, easier to understand steps.  This also helps us make an application more modular, testable and maintainable.  Clearly not all problems need to be broken up, but most substantial problems in interviews and in the workplace do.

In industry teams will often break the user stories into features and then break down those features into more modular components. This is called *modularizing* the application.

How could you break up our sample problem?  Answer and then check the explanation below.

### !challenge

* type: paragraph
* id: 819220a4-080c-4818-a984-29766400d819
* title: What subproblems do you see?

##### !question

How would you break down the problem into two subproblems?

##### !end-question

##### !placeholder

Subproblems

##### !end-placeholder

##### !explanation

Two subproblems could be:

1.  Determining the sum of a contiguous sublist
1.  Traversing the list to find the shortest contiguous sublist which sums to the given number

##### !end-explanation

### !end-challenge

### Solve or Reduce the Problem

Once a problem is understood and broken into more manageable pieces we can then solve the problem.

Write your solution and then look below to see a sample solution.

### !challenge

* type: code-snippet
* language: python3.6
* id: 4dc81336-1c2d-421e-8fe8-27326736b2e3
* title: Smallest Contiguous Sublist Problem
* points: 1
* topics: python, lists, sliding-window

##### !question

Write a function called `minimum_sub_list_length` that takes in a list of positive numbers, `numbers` and a positive integer, `target`.

It should return the minimal length of a contiguous sublist of the given input list which adds up to the given integer.

##### !end-question

##### !placeholder

```py
def minimum_sub_list_length(numbers, target):
    '''
    INPUT: list of positive numbers, and target a positive integer
    OUTPUT: the minimal length of a contiguous sublist of the given input list which adds up to the given integer.
    Return the length of the smallest contiguous sublist which adds up to the given integer or 
    return None if there is no such sublist.
    '''

```

##### !end-placeholder

##### !tests

```py
import unittest
from main import *

class TestChallenge(unittest.TestCase):
    def test_with_empty_list_and_42(self):
        self.assertEqual(None,minimum_sub_list_length([], 42))

    def test_with_one_element_list_and_number_equal_to_the_element(self):
        self.assertEqual(1,minimum_sub_list_length([12], 12))

    def test_with_one_element_list_and_number__not_equal_to_the_element(self):
        self.assertEqual(None,minimum_sub_list_length([12], 42))

    def test_with_1_2_3_4_and_target_7(self):
        self.assertEqual(2,minimum_sub_list_length([1, 2, 3, 4], 7))

    def test_with_4_3_2_1_and_target_7(self):
        self.assertEqual(2,minimum_sub_list_length([4, 3, 2, 1], 7))

    def test_with_1_2_3_4_and_target_10(self):
        self.assertEqual(4,minimum_sub_list_length([1, 2, 3, 4], 10))

    def test_with_1_3_4_and_target_5(self):
        self.assertEqual(2,minimum_sub_list_length([1, 3, 4], 7))

    def test_with_1_2_3_4_5_and_target_5(self):
        self.assertEqual(1,minimum_sub_list_length([1, 2, 3, 4, 5], 5))
```

##### !end-tests

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

A sample solution could be:

```py
def minimum_sub_list_length(numbers, target):
    '''
    INPUT: list of positive numbers, and target a positive integer
    OUTPUT: the minimal length of a contiguous sublist of the given input list which adds up to the given integer.
    Return the length of the smallest contiguous sublist which adds up to the given integer or 
    return None if there is no such sublist.
    '''
    if target == 0:
        return 0
    
    min_length = len(numbers) + 1
  
    for index in range(0, len(numbers)):
        current_sum = numbers[index]
        current_index = index + 1
        while current_index < len(numbers) and \
                current_sum + numbers[current_index] <= target:
            current_sum += numbers[current_index]
            current_index += 1
        
        if current_sum == target and current_index - index < min_length:
            min_length = current_index - index
    
    if min_length == len(numbers) + 1:
        return None
    
    return min_length
```


##### !end-explanation

### !end-challenge

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see a sample solution</summary>

  The solution below works, but as we will see later below, it is not optimal.  We can do better.

  ```py
  def minimum_sub_list_length(numbers, target):
    '''
    INPUT: list of positive numbers, and target a positive integer
    OUTPUT: the minimal length of a contiguous sublist of the given input list which adds up to the given integer.
    Return the length of the smallest contiguous sublist which adds up to the given integer or 
    return None if there is no such sublist.
    '''
    if target == 0:
        return 0
    
    min_length = len(numbers) + 1
  
    for index in range(0, len(numbers)):
        current_sum = numbers[index]
        current_index = index + 1
        while current_index < len(numbers) and \
                current_sum + numbers[current_index] <= target:
            current_sum += numbers[current_index]
            current_index += 1
        
        if current_sum == target and current_index - index < min_length:
            min_length = current_index - index
    
    if min_length == len(numbers) + 1:
        return None
    
    return min_length
  ```
</details>

This solution works and is a relatively direct straight forward approach. This is often called a "brute force" solution.

## Simplify/Refactor

The first big challenge in software development is to **produce working code**. After code is working however the time comes to simplify or refactor (improve) the solution.

In the sample solution above we are using a nested loop and the loop repeatably traverses the list. Our code is not time efficient because we examine the same elements of the list repeatedly.

We are only interested in contiguous sublists, elements have to be next to one another. This means we can apply a technique called a [sliding window](https://www.geeksforgeeks.org/window-sliding-technique/).  A sliding window is a technique that creates a contiguous sublist of a the larger list and then iterates through adjusting the start and end indicies of the sublist.  So each iteration either the start index moves forward or the end index moves forward allowing us to have a "sliding" sublist that progresses through the original list.

In this technique we slide a "window" across the list and track the sum of the elements within the window.  If the sum of the elements in the window is equal to the target, we have found a contiguous sublist.  

The image below illustrates the sliding window technique.

![Sliding Window Example](images/problem-solving__sliding-window.gif)

*Fig. Sliding Window*

### Implementing Our Refactor

In our refactor we can start by creating a window of size 1 from index 0 to index 1.  So our window's `start_index` is `0` and `end_index` is `1`. Our current sum then is the value of the 1st element of the list.

We track the following values:

* `start_index` - Where our window starts
* `end_index` - Where our window ends
* `current_sum` - The sum of the elements in the current window
* `min_length` - The length of the smallest contiguous sublist found thus far.

Then we can repeat this algorithm:

1.  If the current sum is equal to the target, we have found a contiguous sublist which adds up to target, and if it is the smallest contiguous sublist we have found so far, we update the minimum length.
      * We can also advance the window by incrementing the `start_index` by one.
1.  If the current sum is greater than or equal to the target we can decrease the window size by adding one to the start index of the window.
1.  If the current sum is less than the target we can increase the window size by adding one to the end index of the window.
1.  We will repeat this algorithm until the end index has passed the end of the list.

**Practice**:  Go back to the exercise above and try to implement the refactor.  Spend no more than 15 minutes on it.

<details style="max-width: 700px; margin: auto;">
  <summary>Click here to see a sample solution</summary>

  ```py
  def minimum_sub_list_length(numbers, target):
    '''
    INPUT: list of positive numbers, and target a positive integer
    OUTPUT: the minimal length of a contiguous sublist of the given input list which adds up to the given integer.
    Return the length of the smallest contiguous sublist which adds up to the given integer or 
    return None if there is no such sublist.
    '''
    if len(numbers) == 0:
        return None
          
    start_index = 0
    end_index = 1
    current_sum = numbers[0]
    min_length_sublist = len(numbers) + 1
  
    while end_index < len(numbers) + 1:

        if current_sum == target:
            min_length_sublist = min(min_length_sublist, end_index - start_index)

            current_sum -= numbers[start_index]
            start_index += 1

        elif current_sum < target:
            if end_index < len(numbers):
                current_sum += numbers[end_index]
            end_index += 1
            
        elif current_sum > target:
            current_sum -= numbers[start_index]
            start_index += 1

    if min_length_sublist == len(numbers) + 1:
        return None
    return min_length_sublist
  ```
</details>

This solution now makes only one pass through the list, meaning as the input array grows, the solution will perform better compared to our original solution.

## Summary

In this lesson we have walked through a general approach to problem solving.  By breaking the approach into a set of steps we can systematically approach problems in computer science.

The steps we created are:

* Understand the problem
* Explore Examples
* Break Down the Problem
* Solve or Reduce the Problem
* Simplify/Refactor

By making problem solving a process we can reduce stress and improve our ability to work toward solutions.


