Here’s how you can implement a **queue using an array** in Python. This implementation includes basic operations such as **enqueue** (push), **dequeue** (pop), and checking if the queue is empty or full.

### Queue Using Array

---

## Operations on Queue:
1. **Enqueue (push)**: Add an element to the end of the queue.
2. **Dequeue (pop)**: Remove the front element from the queue.
3. **isEmpty**: Check if the queue is empty.
4. **isFull**: Check if the queue is full (fixed-size array).
5. **Peek**: View the front element without removing it.

### Code Implementation:

```python
class QueueUsingArray:
    def __init__(self, max_size):
        # Initialize the queue with a fixed-size array
        self.queue = [None] * max_size
        self.front = 0  # Index of the front element
        self.rear = -1  # Index of the rear element
        self.max_size = max_size  # Maximum capacity of the queue
        self.size = 0  # Number of elements in the queue

    def isEmpty(self):
        # Check if the queue is empty
        return self.size == 0

    def isFull(self):
        # Check if the queue is full
        return self.size == self.max_size

    def enqueue(self, element):
        # Add an element to the queue
        if self.isFull():
            print("Queue Overflow! Cannot enqueue")
        else:
            # Circular increment of rear pointer
            self.rear = (self.rear + 1) % self.max_size
            self.queue[self.rear] = element
            self.size += 1
            print(f"Enqueued {element}")

    def dequeue(self):
        # Remove the front element of the queue
        if self.isEmpty():
            print("Queue Underflow! Cannot dequeue")
            return None
        else:
            element = self.queue[self.front]
            # Circular increment of front pointer
            self.front = (self.front + 1) % self.max_size
            self.size -= 1
            return element

    def peek(self):
        # Return the front element without removing it
        if self.isEmpty():
            print("Queue is empty!")
            return None
        else:
            return self.queue[self.front]

    def display(self):
        # Display the current state of the queue
        if self.isEmpty():
            print("Queue is empty!")
        else:
            print("Queue elements:", end=" ")
            index = self.front
            for i in range(self.size):
                print(self.queue[index], end=" ")
                index = (index + 1) % self.max_size
            print()


# Example usage
queue = QueueUsingArray(5)
queue.enqueue(10)
queue.enqueue(20)
queue.enqueue(30)
queue.display()
print("Dequeued:", queue.dequeue())
print("Front element:", queue.peek())
queue.display()
```

### Explanation:

1. **Constructor (`__init__`)**: 
   - Initializes the queue with a fixed size (`max_size`). The `queue` is an array of size `max_size` initialized with `None`.
   - `front` and `rear` are pointers to the front and rear of the queue, initialized to `0` and `-1` respectively.
   - `size` keeps track of the number of elements currently in the queue.

2. **`isEmpty()`**:
   - Returns `True` if `size == 0`, meaning the queue is empty.

3. **`isFull()`**:
   - Returns `True` if `size == max_size`, meaning the queue is full.

4. **`enqueue(element)`**:
   - Adds an element to the rear of the queue. If the queue is full, it prints an error message.
   - The `rear` is incremented using circular logic: `(rear + 1) % max_size`. This handles cases where the queue "wraps around" in a circular fashion.

5. **`dequeue()`**:
   - Removes the front element of the queue. If the queue is empty, it prints an error message and returns `None`.
   - The `front` is incremented using circular logic: `(front + 1) % max_size`.

6. **`peek()`**:
   - Returns the front element without removing it. If the queue is empty, it returns `None`.

7. **`display()`**:
   - Displays the elements of the queue starting from the front and going to the rear, considering the circular nature of the queue.

### Example Output

```bash
Enqueued 10
Enqueued 20
Enqueued 30
Queue elements: 10 20 30 
Dequeued: 10
Front element: 20
Queue elements: 20 30 
```

---



## question queue using array
'''
Here is the complete implementation for a **queue** using Python, including the `push` (enqueue) and `pop` (dequeue) methods. 

```python
class MyQueue:
    
    def __init__(self):
        # Initialize an empty list to act as the queue
        self.queue = []
    
    # Function to push an element x in a queue.
    def push(self, x):
        """
        Adds an element x to the end of the queue.
        """
        self.queue.append(x)
    
    # Function to pop an element from the queue and return that element.
    def pop(self): 
        """
        Removes and returns the front element of the queue. 
        If the queue is empty, returns -1.
        """
        if not self.queue:
            return -1  # If the queue is empty
        else:
            return self.queue.pop(0)  # Remove the front element

# Example usage:
q = MyQueue()
q.push(10)
q.push(20)
print(q.pop())  # Output: 10 (first element is removed)
print(q.pop())  # Output: 20 (second element is removed)
print(q.pop())  # Output: -1 (queue is empty)
```

### Explanation of Each Part:

1. **`__init__(self)`**:
   - Initializes an empty list `self.queue`, which acts as the queue to store elements.

2. **`push(self, x)`**:
   - This method adds an element `x` to the **end** of the queue using `append()`. This operation is known as **enqueue** in a queue.

3. **`pop(self)`**:
   - This method removes and returns the **front** element from the queue.
   - If the queue is empty (checked using `not self.queue`), it returns `-1` to indicate that no element is available to pop.
   - If the queue has elements, it removes the first element (using `pop(0)`).

### Example Output:

```bash
10
20
-1
```

In this simple implementation:
- `push(10)` adds `10` to the queue.
- `push(20)` adds `20` to the queue.
- `pop()` removes and returns the front element (first in, first out).

'''

This implementation uses a **circular queue** concept where the `rear` and `front` pointers wrap around when they reach the end of the array, preventing wasted space in a fixed-size array.