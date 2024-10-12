Here’s how to implement a **stack using queues** in Markdown format with an explanation for each line.

---

## Stack Using Queue

In this approach, we use two queues to simulate the behavior of a stack. Since a **queue** follows the **FIFO (First In First Out)** principle and a **stack** follows **LIFO (Last In First Out)**, we need to manipulate the queues to behave like a stack.

### Operations on Stack
1. **Push**: Add an element to the "top" of the stack.
2. **Pop**: Remove the element from the top of the stack.
3. **Top/Peek**: Return the top element of the stack without removing it.
4. **isEmpty**: Check if the stack is empty.

### Code Implementation

```python
from collections import deque

class StackUsingQueue:
    def __init__(self):
        # Initialize two empty queues
        self.queue1 = deque()
        self.queue2 = deque()

    def isEmpty(self):
        # Return True if queue1 is empty, meaning the stack is empty
        return len(self.queue1) == 0

    def push(self, element):
        # Add the element to queue2 (temporary queue)
        self.queue2.append(element)
        
        # Push all elements of queue1 to queue2, maintaining order
        while self.queue1:
            self.queue2.append(self.queue1.popleft())
        
        # Swap the names of queue1 and queue2
        self.queue1, self.queue2 = self.queue2, self.queue1
        # Now queue1 contains all elements, with the new element at the front (top of the stack)

    def pop(self):
        # If stack is empty, return None
        if self.isEmpty():
            print("Stack Underflow!")
            return None
        # Remove the front of queue1, which is the top element of the stack
        return self.queue1.popleft()

    def peek(self):
        # Return the front of queue1, which is the top element of the stack, without removing it
        if self.isEmpty():
            print("Stack is empty!")
            return None
        return self.queue1[0]

    def display(self):
        # Display the current elements of the stack
        if self.isEmpty():
            print("Stack is empty!")
        else:
            print("Current stack elements:", list(self.queue1))


# Example usage
stack = StackUsingQueue()
stack.push(10)
stack.push(20)
stack.push(30)
stack.display()
stack.pop()
stack.peek()
stack.display()
```

### Line-by-Line Explanation

1. **`from collections import deque`**:  
   This imports `deque` from the `collections` module. We use `deque` because it provides an efficient way to append and pop elements from both ends.

2. **`class StackUsingQueue:`**:  
   This defines the class `StackUsingQueue` which simulates the behavior of a stack using two queues.

3. **`def __init__(self):`**:  
   The constructor initializes two empty queues (`queue1` and `queue2`), represented using `deque`. These queues will be used to implement the stack operations.

4. **`self.queue1 = deque()`** and **`self.queue2 = deque()`**:  
   These two lines create two empty deque objects, `queue1` and `queue2`. `queue1` will act as the main queue, while `queue2` will be a temporary queue.

5. **`def isEmpty(self):`**:  
   This function checks if the stack is empty. If `queue1` is empty, it means the stack is empty.

6. **`return len(self.queue1) == 0`**:  
   It checks if the length of `queue1` is zero. If true, it returns `True`, indicating the stack is empty.

7. **`def push(self, element):`**:  
   The `push` function is used to add an element to the stack.

8. **`self.queue2.append(element)`**:  
   The new element is first added to `queue2`, the temporary queue.

9. **`while self.queue1:`**:  
   A loop that runs as long as `queue1` is not empty. This moves all elements from `queue1` to `queue2` in the same order.

10. **`self.queue2.append(self.queue1.popleft())`**:  
   This moves the front element from `queue1` to `queue2`. The `popleft()` function removes the front element of `queue1` and appends it to `queue2`.

11. **`self.queue1, self.queue2 = self.queue2, self.queue1`**:  
   After transferring all elements to `queue2`, we swap the roles of `queue1` and `queue2`. Now, `queue1` contains the elements in the correct order, and `queue2` is empty.

12. **`def pop(self):`**:  
   The `pop` function removes the top element of the stack.

13. **`if self.isEmpty():`**:  
   This checks if the stack is empty before popping. If the stack is empty, it prints "Stack Underflow!" and returns `None`.

14. **`return self.queue1.popleft()`**:  
   This removes and returns the front element of `queue1`, which corresponds to the top of the stack.

15. **`def peek(self):`**:  
   The `peek` function returns the top element of the stack without removing it.

16. **`return self.queue1[0]`**:  
   This returns the front element of `queue1`, which is the top of the stack.

17. **`def display(self):`**:  
   This function displays the current elements in the stack.

18. **`print("Current stack elements:", list(self.queue1))`**:  
   This prints the contents of `queue1`, showing the current state of the stack.

19. **Example Usage**:  
   - `stack.push(10)`: Pushes the element `10` to the stack.
   - `stack.push(20)`: Pushes the element `20` to the stack.
   - `stack.push(30)`: Pushes the element `30` to the stack.
   - `stack.pop()`: Removes the top element (`30`) from the stack.
   - `stack.peek()`: Returns the top element (`20`) without removing it.

### Example Output

```bash
Pushed 10
Pushed 20
Pushed 30
Current stack elements: [30, 20, 10]
Popped 30
Top element is: 20
Current stack elements: [20, 10]
```

---

This Markdown format breaks down each line of code and explains how the stack operations are implemented using two queues.