# List Implementations

**Native Arrays and Array Lists**

  1. Let's talk about native arrays vs. Ruby arrays (`ArrayList` in Java)
  2. Let's write `lib/array_list.rb` where we will simulate what happens "under the hood" with Ruby's Array object.
      - together: `initialize`, `add`, `delete`, `to_s`, `include?`, `size`
      - on your own: `max`

**Array Lists vs Linked Lists**

  3. Let's talk about linked lists
  4. Let's take look at `lib/linked_list.rb` and see how the _implementation_ is different (but the _interface_ is the same) and uses nodes instead of a native array to store data.
      - provided: `Node` class, `LinkedList` class: `initialize`, `add`, `delete`, `to_s`
      - together: `include?`, `size`
      - on your own: `max`

**Interfaces vs Implementations**

  5. Let's look at `lotto.rb` and talk about interfaces vs implementations
  6. Let's make it so that lotto ticket numbers are always displayed in numerical order. Do this by modifying the `add(value)` method in `ArrayList`
  7. Do the same for `add(value)` method in `LinkedList`

<!-- >>>>>>>>>>>>>>>>>>>>>> BEGIN CHALLENGE >>>>>>>>>>>>>>>>>>>>>> -->
<!-- Replace everything in square brackets [] and remove brackets  -->

### !challenge

* type: testable-project
* id: 99d480d9-6d1d-4df8-8a1d-0e270104a61f
* title: List Implementations
* upstream: https://github.com/ada-c13/list-implementations
* validate_fork: false
* points: 3
* topics: linked-lists

##### !question

Fork the linked repo and submit your completed exercise.  **Then** on the next question submit your PR, so I can make PR comments.

##### !end-question

##### !placeholder

Link to your repo

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
* id: 91ea123a-3d04-4273-b088-31ff25be58ab
* title: Link to your PR
<!-- * points: [1] (optional, the number of points for scoring as a checkpoint) -->
* topics: linked-lists

##### !question

Submit a link of your PR for the project.

##### !end-question

##### !placeholder

Your PR link goes here.

##### !end-placeholder

##### !answer

/*/

##### !end-answer

<!-- other optional sections -->
<!-- !hint - !end-hint (markdown, users can see after a failed attempt) -->
<!-- !rubric - !end-rubric (markdown, instructors can see while scoring a checkpoint) -->
<!-- !explanation - !end-explanation (markdown, students can see after answering correctly) -->

### !end-challenge

<!-- ======================= END CHALLENGE ======================= -->