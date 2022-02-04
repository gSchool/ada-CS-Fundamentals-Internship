# Problem Solving & Big O Exercise

### !challenge

* type: short-answer
* id: 8f9ce926-298f-42e5-bf3a-8354d752063e
* title: Why is Big O important?
* points: 1
* topics: Big O

##### !question

Why is Big O important?

##### !end-question

##### !placeholder

Why use Big O

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

##### !hint

Why don't we just time our application, or count the number of operations a function does?

##### !end-hint

##### !explanation

Big O provides a standard and precise way to measure and compare how fast and memory intensive our code is.

##### !end-explanation

### !end-challenge

### !challenge

* type: multiple-choice
* id: 4dd37fb7-79b2-499b-867b-187df51bbdda
* title: Sum Digits
* points: 1
* topics: python, big-o, sum-digits, time-complexity

##### !question

What is the time complexity of the following function where `n` is the number passed in as a parameter?

```py
def sum_digits(n):
    total = 0
    while n > 0:
        total += n % 10 # get last digit
        n //= 10        # remove last digit
    
    return total
```
##### !end-question

##### !options

* O(1)
* O(log n)
* O(n)
* O(n log n)
* O(n^2)

##### !end-options

##### !answer

* O(log n)

##### !end-answer

##### !hint

Remember `n` is the number passed in, not the number of digits.

##### !end-hint

##### !explanation

Because we *divide* n by 10 with each iteration of the loop the time complexity is logarithmic.  This is a case where the base of the logarithm is 10, instead of 2 (because we're dividing by 10 with each loop iteration).  If `n` is 57, the loop will execute 2 times.  If we make it a 4 digit number ~100 times bigger, 1057, the loop will execute 4 times.

##### !end-explanation

### !end-challenge

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: multiple-choice
* id: 2d6fbcb2-931a-4c2b-a5ea-f186515651fe
* title: Picking Between Solutions
* points: 1
* topics: python, big-o, time-complexity

##### !question

Consider the following solutions to a problem.  Which one is the best?

```py
def isAnagram(self, s: str, t: str) -> bool:
    s_list = []
    t_list = []
    s_list[:0] = s
    t_list[:0] = t
    
    for s_letter in s_list:
        if s_letter in t_list:
            t_list.remove(s_letter)
        else:
            return False
    
    return len(t_list) == 0
```
*Code Sample: Solution 1*

```py
def isAnagram(self, s: str, t: str) -> bool:
    s_freq_map = {}
    t_freq_map = {}
    if len(s) != len(t):
        return False
    
    for letter in s:
        if not s_freq_map.get(letter):
            s_freq_map[letter] = 0
        
        s_freq_map[letter] += 1
    
    for letter in t:
        if not t_freq_map.get(letter):
            t_freq_map[letter] = 0
        
        t_freq_map[letter] += 1
    
    for letter, count in s_freq_map.items():
        if t_freq_map.get(letter) != count:
            return False
    
    return True
```
*Code Sample: Solution 1*

##### !end-question

##### !options

* Solution 1
* Solution 2
* Both are the same

##### !end-options

##### !answer

* Solution 2

##### !end-answer

<!-- other optional sections -->
##### !hint

What are the time complexities of the two solutions?  Are there any hidden nested loops?

##### !end-hint

### !end-challenge


<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: short-answer
* id: d8b19e21-8bc1-411a-9824-ab9c681566e6
* title: Why
* points: 1
* topics: python, big-o, time-complexity

##### !question

Why did you pick that answer?

##### !end-question

##### !placeholder

Why?

##### !end-placeholder

##### !answer

/.+/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, hidden, students click to view) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
##### !explanation

* The 1st solution has an O(n^2) time complexity because it uses a hidden nested loop.  
* The 2nd solution has an O(n) time complexity

`if letter in t_list:` loops through `t_list` and it is nested inside a loop.  Furthermore, deleting a letter from `t_list` also require O(n) time because removing an element from a list requires a loop.

##### !end-explanation

### !end-challenge
