Here's the explanation of a **stack using an array** in Markdown format, suitable for your notes:

---

## Stack Using Array

A **stack** is a linear data structure that follows the **LIFO (Last In First Out)** principle. The last element added is the first one to be removed. Stacks can be implemented using arrays or linked lists. Below is the implementation using an array in Python.

### Operations on Stack
1. **Push**: Add an element to the top of the stack.
2. **Pop**: Remove the top element from the stack.
3. **Peek/Top**: View the top element without removing it.
4. **isEmpty**: Check if the stack is empty.
5. **isFull**: Check if the stack is full (optional in dynamic arrays like Python).

### Code Implementation

```python
class Stack:
    def __init__(self, max_size):
        # Initialize the stack with a fixed-size array
        self.stack = [None] * max_size
        self.top = -1  # Index of the top element
        self.max_size = max_size  # Maximum capacity of the stack

    def isEmpty(self):
        # Check if the stack is empty
        return self.top == -1

    def isFull(self):
        # Check if the stack is full
        return self.top == self.max_size - 1

    def push(self, element):
        # Add an element to the stack
        if self.isFull():
            print("Stack Overflow!")
        else:
            self.top += 1
            self.stack[self.top] = element
            print(f"Pushed {element}")

    def pop(self):
        # Remove and return the top element
        if self.isEmpty():
            print("Stack Underflow!")
            return None
        else:
            popped_element = self.stack[self.top]
            self.stack[self.top] = None  # Optional: Clear the value
            self.top -= 1
            return popped_element

    def peek(self):
        # Return the top element without removing it
        if self.isEmpty():
            return None
        else:
            return self.stack[self.top]

    def display(self):
        # Display the stack contents
        if self.isEmpty():
            print("Stack is empty")
        else:
            print("Stack elements:", self.stack[:self.top + 1])


# Example usage
stack = Stack(5)
stack.push(10)
stack.push(20)
stack.push(30)
stack.display()
stack.pop()
stack.peek()
stack.display()
```

### Explanation

1. **Constructor (`__init__`)**: Initializes the stack with an array of `max_size` and sets `top` to `-1`, indicating the stack is empty.
2. **`isEmpty()`**: Returns `True` if `top` is `-1`, meaning the stack is empty.
3. **`isFull()`**: Returns `True` if `top` equals `max_size - 1`, indicating the stack is full.
4. **`push(element)`**: Adds an element to the top of the stack if it's not full.
5. **`pop()`**: Removes and returns the top element from the stack. If the stack is empty, it returns `None`.
6. **`peek()`**: Returns the top element without removing it, or `None` if the stack is empty.
7. **`display()`**: Displays the current stack elements.

### Example Output

```bash
Pushed 10
Pushed 20
Pushed 30
Stack elements: [10, 20, 30]
Popped 30
Top element: 20
Stack elements: [10, 20]
```

---

This Markdown format should be easy to include in your notes!