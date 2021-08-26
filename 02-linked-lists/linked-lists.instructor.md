# Instructor: Linked Lists

## Simon's Final Implementation

Simon's implementations for the stubbed `LinkedList` class in the lesson.

```python
# Defines a node in the singly linked list
class Node:
    def __init__(self, value):
        self.data = value
        self.next = None
```

```python
# Defines the singly linked list
class LinkedList:
    def __init__(self):
        self.head = None

    # Method. Adds a new node with the specific data value to the beginning of the linked list.
    def add_first(self, value):
        new_node = Node(value)
        new_node.next = self.head
        self.head = new_node

    # Method. Returns the value in the first node in the linked list.
    # Returns None if the list is empty.
    def get_first(self):
        return self.head.data if self.head else None

    # Method. Returns the value of the last node in the linked list. Returns None if the list is empty.
    def get_last(self):
        # Return None if the list is empty
        # Otherwise, traverse the list to the end
        # Then return the last node's value
        current_node = self.head
        while current_node:
            if not current_node.next:
                return current_node
            current_node = current_node.next
    
    def add_last(self, value):
        new_node = Node(value)
        last_node = self.get_last()
        if not last_node:
            self.head = new_node
        else:
            last_node.next = new_node

    # Method. Returns the value at a given index in the linked list.
    # Index count starts at 0.
    # Returns None if there are fewer nodes in the linked list than the index value.
    def get_at_index(self, index):
        # Traverse the list
        # <index> times
        # or until the end is reached
        # Then return the current node's value
        current_node = self.head
        for i in range(index + 1):
            if i == index:
                return current_node.data
            if current_node.next is None:
                return None
            current_node = current_node.next
```
