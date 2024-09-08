Here's a comprehensive Markdown file for the Queue data structure, covering from basic to advanced levels, including interview questions and detailed explanations.

---

# Queue Data Structure

## Table of Contents
- [Introduction to Queue](#introduction-to-queue)
- [Queue Operations](#queue-operations)
- [Types of Queue](#types-of-queue)
- [Queue Implementations](#queue-implementations)
    - [Array-based Queue](#array-based-queue)
    - [Linked List-based Queue](#linked-list-based-queue)
- [Circular Queue](#circular-queue)
- [Deque (Double-ended Queue)](#deque-double-ended-queue)
- [Priority Queue](#priority-queue)
- [Applications of Queue](#applications-of-queue)
- [Time and Space Complexity](#time-and-space-complexity)
- [Interview Questions](#interview-questions)

---

## Introduction to Queue

A **Queue** is a linear data structure that follows the **First In, First Out (FIFO)** principle. The element that is inserted first will be the first one to be removed.

- **Enqueue**: Add an element to the end (rear) of the queue.
- **Dequeue**: Remove an element from the front of the queue.

### Real-life Example:
Think of a line at a ticket counter. The first person in line is the first one served, and people are added to the end of the line.

---

## Queue Operations

Here are the main operations supported by a queue:

1. **Enqueue**: Add an element to the rear of the queue.
2. **Dequeue**: Remove an element from the front of the queue.
3. **Front/Peek**: Get the front element of the queue without removing it.
4. **IsEmpty**: Check if the queue is empty.
5. **Size**: Return the number of elements in the queue.

### Code Example (Basic Queue Operations in Python)
```python
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, item):
        self.queue.append(item)

    def dequeue(self):
        if not self.is_empty():
            return self.queue.pop(0)
        return "Queue is empty!"

    def peek(self):
        if not self.is_empty():
            return self.queue[0]
        return "Queue is empty!"

    def is_empty(self):
        return len(self.queue) == 0

    def size(self):
        return len(self.queue)
```

---

## Types of Queue

1. **Simple Queue (Linear Queue)**: Elements are added at the rear and removed from the front.
2. **Circular Queue**: The last position is connected back to the first position, making the queue circular.
3. **Priority Queue**: Each element has a priority. Elements are dequeued based on their priority rather than their insertion order.
4. **Double-ended Queue (Deque)**: Elements can be added or removed from both the front and rear of the queue.

---

## Queue Implementations

### Array-based Queue
In this approach, a queue is implemented using a static array. When the queue is full, no more elements can be added.

#### Code Example:
```python
class ArrayQueue:
    def __init__(self, size):
        self.queue = [None] * size
        self.front = self.rear = -1
        self.size = size

    def enqueue(self, item):
        if self.rear == self.size - 1:
            return "Queue is full!"
        else:
            self.rear += 1
            self.queue[self.rear] = item
            if self.front == -1:
                self.front = 0

    def dequeue(self):
        if self.front == -1:
            return "Queue is empty!"
        else:
            item = self.queue[self.front]
            self.queue[self.front] = None
            if self.front == self.rear:
                self.front = self.rear = -1
            else:
                self.front += 1
            return item
```

### Linked List-based Queue
This uses a linked list where each node points to the next node. The front pointer keeps track of the first element, and the rear pointer tracks the last element.

#### Code Example:
```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedQueue:
    def __init__(self):
        self.front = self.rear = None

    def enqueue(self, item):
        new_node = Node(item)
        if self.rear is None:
            self.front = self.rear = new_node
            return
        self.rear.next = new_node
        self.rear = new_node

    def dequeue(self):
        if self.front is None:
            return "Queue is empty!"
        item = self.front.data
        self.front = self.front.next
        if self.front is None:
            self.rear = None
        return item
```

---

## Circular Queue

In a circular queue, the end of the queue is connected back to the front, creating a circle. This allows efficient utilization of storage, as elements can be added to the queue even if there are empty spaces before the rear.

#### Code Example:
```python
class CircularQueue:
    def __init__(self, size):
        self.queue = [None] * size
        self.size = size
        self.front = self.rear = -1

    def enqueue(self, item):
        if (self.rear + 1) % self.size == self.front:
            return "Queue is full!"
        elif self.front == -1:
            self.front = self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.size
        self.queue[self.rear] = item

    def dequeue(self):
        if self.front == -1:
            return "Queue is empty!"
        data = self.queue[self.front]
        if self.front == self.rear:
            self.front = self.rear = -1
        else:
            self.front = (self.front + 1) % self.size
        return data
```

---

## Deque (Double-ended Queue)

A **Deque** (pronounced "deck") allows insertion and deletion from both ends, making it more flexible than a simple queue.

#### Code Example:
```python
from collections import deque

d = deque()

# Add to the right end
d.append(1)

# Add to the left end
d.appendleft(2)

# Remove from the right end
d.pop()

# Remove from the left end
d.popleft()
```

---

## Priority Queue

In a priority queue, each element is associated with a priority. Elements with higher priority are dequeued before elements with lower priority.

#### Code Example using Python’s `heapq`:
```python
import heapq

class PriorityQueue:
    def __init__(self):
        self.queue = []
    
    def enqueue(self, item, priority):
        heapq.heappush(self.queue, (priority, item))
    
    def dequeue(self):
        if len(self.queue) == 0:
            return "Queue is empty!"
        return heapq.heappop(self.queue)[1]
```

---

## Applications of Queue

1. **CPU Scheduling**: Queues are used in operating systems to schedule tasks.
2. **Printer Queue**: Print jobs are handled in the order they are added.
3. **Breadth-First Search (BFS)**: In graph traversal, a queue helps explore nodes in layers.
4. **Cache Implementation**: Queues help implement caches like LRU (Least Recently Used).

---

## Time and Space Complexity

| Operation  | Array-based Queue | Linked List-based Queue | Circular Queue |
|------------|-------------------|-------------------------|----------------|
| Enqueue    | O(1)              | O(1)                    | O(1)           |
| Dequeue    | O(1)              | O(1)                    | O(1)           |
| Peek       | O(1)              | O(1)                    | O(1)           |
| Space      | O(n)              | O(n)                    | O(n)           |

---

## Interview Questions

1. **What is the difference between a queue and a stack?**
    - Queue follows **FIFO** (First In First Out), while stack follows **LIFO** (Last In First Out).

2. **How is a circular queue different from a regular queue?**
    - In a circular queue, the last position connects back to the first position, allowing better space utilization.

3. **How would you implement a queue using two stacks?**
    - **Answer**: Use one stack for enqueuing elements and another stack for dequeuing. For dequeuing, reverse the first stack into the second.

4. **Explain the concept of a priority queue.**
    - **Answer**: A priority queue dequeues elements based on their priority, not just the order of insertion.

5. **What are some real-world applications of queues?**
    - **Answer**: Queues are used in task scheduling, print jobs, BFS traversal in graphs, and handling asynchronous data (message queues).

6. **What is a deque, and how is it different from a queue?**
    - **Answer**: A deque allows insertion and removal of elements from both ends, unlike a queue where operations are restricted to the front and rear.

7. **How would you implement an LRU cache using a queue?**
    - **Answer**: Use a doubly linked list and a hash map to efficiently track and remove least recently used items in constant time.

## 50 Interview Questions
Here are 50 additional interview questions with short answers related to the **Queue** data structure, including code examples where necessary:

---

### 1. **How do you check if a queue is empty?**
   - **Answer**: By checking if the front or the rear index is equal to -1 or by checking the length of the queue.
   - **Code**:
   ```python
   def is_empty(self):
       return len(self.queue) == 0
   ```

### 2. **What is a real-world analogy for a queue?**
   - **Answer**: A line of people waiting for a bus or a printer queue.

### 3. **What are the primary use cases of a queue?**
   - **Answer**: Task scheduling, BFS traversal in graphs, asynchronous data transfer, and CPU scheduling.

### 4. **How can you implement a queue using stacks?**
   - **Answer**: Use two stacks: one for enqueue operations and the other for dequeue operations.
   - **Code**:
   ```python
   class QueueWithStacks:
       def __init__(self):
           self.stack1 = []
           self.stack2 = []

       def enqueue(self, item):
           self.stack1.append(item)

       def dequeue(self):
           if not self.stack2:
               while self.stack1:
                   self.stack2.append(self.stack1.pop())
           return self.stack2.pop() if self.stack2 else "Queue is empty!"
   ```

### 5. **How do you implement a queue using linked lists?**
   - **Answer**: Use a linked list where each node points to the next node, maintaining front and rear pointers.
   - **Code**:
   ```python
   class Node:
       def __init__(self, data):
           self.data = data
           self.next = None

   class LinkedListQueue:
       def __init__(self):
           self.front = self.rear = None

       def enqueue(self, item):
           new_node = Node(item)
           if self.rear is None:
               self.front = self.rear = new_node
           else:
               self.rear.next = new_node
               self.rear = new_node

       def dequeue(self):
           if self.front is None:
               return "Queue is empty!"
           temp = self.front
           self.front = temp.next
           if self.front is None:
               self.rear = None
           return temp.data
   ```

### 6. **How does a circular queue differ from a regular queue?**
   - **Answer**: In a circular queue, the rear and front are connected, making better use of space.

### 7. **What is the time complexity for enqueue and dequeue operations in a queue?**
   - **Answer**: Both enqueue and dequeue operations are **O(1)** in a standard queue.

### 8. **How would you implement a circular queue using arrays?**
   - **Answer**: By using a modulo operation to wrap around the indices.
   - **Code**:
   ```python
   class CircularQueue:
       def __init__(self, size):
           self.queue = [None] * size
           self.size = size
           self.front = self.rear = -1

       def enqueue(self, item):
           if (self.rear + 1) % self.size == self.front:
               return "Queue is full!"
           elif self.front == -1:
               self.front = self.rear = 0
           else:
               self.rear = (self.rear + 1) % self.size
           self.queue[self.rear] = item

       def dequeue(self):
           if self.front == -1:
               return "Queue is empty!"
           data = self.queue[self.front]
           if self.front == self.rear:
               self.front = self.rear = -1
           else:
               self.front = (self.front + 1) % self.size
           return data
   ```

### 9. **What are some disadvantages of using a static array to implement a queue?**
   - **Answer**: Wasted space if elements are dequeued and limited capacity unless the array is resized.

### 10. **Can a queue be implemented using recursion?**
   - **Answer**: Yes, using recursive calls to simulate enqueue and dequeue operations.

---

### 11. **Explain the concept of a priority queue.**
   - **Answer**: In a priority queue, elements are dequeued based on their priority, not just the insertion order.

### 12. **How do you implement a priority queue using a heap?**
   - **Answer**: Use Python’s `heapq` to maintain a heap structure.
   - **Code**:
   ```python
   import heapq
   class PriorityQueue:
       def __init__(self):
           self.queue = []
       
       def enqueue(self, item, priority):
           heapq.heappush(self.queue, (priority, item))

       def dequeue(self):
           return heapq.heappop(self.queue)[1] if self.queue else "Queue is empty!"
   ```

### 13. **What is the difference between a deque and a queue?**
   - **Answer**: A **deque** allows insertion and deletion from both ends, while a **queue** only allows insertion at the rear and deletion from the front.

### 14. **What is a double-ended queue (deque)?**
   - **Answer**: A deque is a queue that allows elements to be added or removed from both ends.

### 15. **How can you implement a deque using a doubly linked list?**
   - **Answer**: Use a doubly linked list where both the front and rear pointers can be updated.
   - **Code**:
   ```python
   class DequeNode:
       def __init__(self, data):
           self.data = data
           self.prev = self.next = None

   class Deque:
       def __init__(self):
           self.front = self.rear = None

       def add_front(self, item):
           new_node = DequeNode(item)
           if self.front is None:
               self.front = self.rear = new_node
           else:
               new_node.next = self.front
               self.front.prev = new_node
               self.front = new_node

       def add_rear(self, item):
           new_node = DequeNode(item)
           if self.rear is None:
               self.front = self.rear = new_node
           else:
               self.rear.next = new_node
               new_node.prev = self.rear
               self.rear = new_node

       def remove_front(self):
           if self.front is None:
               return "Deque is empty!"
           temp = self.front
           self.front = self.front.next
           if self.front is None:
               self.rear = None
           else:
               self.front.prev = None
           return temp.data

       def remove_rear(self):
           if self.rear is None:
               return "Deque is empty!"
           temp = self.rear
           self.rear = self.rear.prev
           if self.rear is None:
               self.front = None
           else:
               self.rear.next = None
           return temp.data
   ```

---

### 16. **How does the LRU (Least Recently Used) cache algorithm use a queue?**
   - **Answer**: It uses a doubly linked list to maintain the order of usage and a hash map for quick lookups.

### 17. **How would you design an LRU cache using a queue?**
   - **Answer**: Use a doubly linked list to track recent usage and a hash map to store the key-value pairs.

### 18. **What is the difference between BFS and DFS?**
   - **Answer**: BFS uses a queue and explores neighbors layer by layer, while DFS uses a stack and explores as deep as possible.

### 19. **What is the time complexity for enqueuing an element in a priority queue implemented with a binary heap?**
   - **Answer**: **O(log n)** due to heap insertion operations.

### 20. **What is the space complexity of a queue implemented using a linked list?**
   - **Answer**: **O(n)** where `n` is the number of elements in the queue.

---

### 21. **What is a monotonic queue?**
   - **Answer**: A monotonic queue maintains elements in a specific order (increasing or decreasing) to answer range queries efficiently.

### 22. **How would you implement a monotonic queue?**
   - **Answer**: Use a deque and ensure elements are inserted in sorted order.

### 23. **What are the key differences between a stack and a queue?**
   - **Answer**: A **stack** is LIFO (Last In, First Out), while a **queue** is FIFO (First In, First Out).

### 24. **How do you detect a cycle in a graph using BFS?**
   - **Answer**: By using a queue to traverse the graph and marking visited nodes. If a node is visited twice, there is a cycle.

### 25. **How do you reverse a queue?**
   - **Answer**: Use a stack to reverse the order of the queue.
   - **Code**:
   ```python
   def reverse_queue(queue):
       stack = []
       while not queue.is_empty():
           stack.append(queue.dequeue())
       while stack:
           queue.enqueue(stack.pop())
   ```

---

### 26. **How can you design a message queue system?**
   - **Answer**: Use a priority queue or a simple queue for message ordering, and dequeuer processes messages based on FIFO or



 priority.

### 27. **What is a bounded queue?**
   - **Answer**: A queue with a fixed maximum size. Once it reaches its capacity, no more elements can be enqueued.

### 28. **How would you handle overflow in a bounded queue?**
   - **Answer**: By raising an exception or dropping the oldest elements (circular queue).

### 29. **How does Java's `BlockingQueue` work?**
   - **Answer**: A `BlockingQueue` waits for the queue to become non-empty when dequeuing and non-full when enqueuing.

### 30. **How do you merge `k` sorted lists using a priority queue?**
   - **Answer**: Insert the first element of each list into a min-heap (priority queue), then repeatedly extract the smallest element and insert the next element from the corresponding list.

Here are 20 more questions to add, completing a total of 50 interview questions on the **Queue** data structure:


### 31. **How do you merge `k` sorted arrays using a queue?**
   - **Answer**: Place the first element of each array into a priority queue. Extract the minimum element, then insert the next element from the same array into the queue.
   - **Code**:
   ```python
   import heapq

   def merge_k_sorted(arrays):
       heap = []
       result = []
       
       # Insert the first element of each array into the heap
       for idx, array in enumerate(arrays):
           if array:
               heapq.heappush(heap, (array[0], idx, 0))

       while heap:
           val, arr_idx, ele_idx = heapq.heappop(heap)
           result.append(val)
           # If the array has more elements, insert the next one
           if ele_idx + 1 < len(arrays[arr_idx]):
               heapq.heappush(heap, (arrays[arr_idx][ele_idx + 1], arr_idx, ele_idx + 1))

       return result
   ```

### 32. **How can you implement a `First-In-First-Out (FIFO)` cache using a queue?**
   - **Answer**: Use a queue to maintain the order of the items, evicting the oldest item when capacity is reached.

### 33. **What is a deque, and where is it commonly used?**
   - **Answer**: A **deque** (double-ended queue) is a data structure that allows adding and removing elements from both ends. It is commonly used in sliding window problems.

### 34. **How do you implement a queue using a single stack?**
   - **Answer**: Use recursion to dequeue elements by popping all items from the stack, then push them back after retrieving the bottom-most element.
   - **Code**:
   ```python
   class QueueWithOneStack:
       def __init__(self):
           self.stack = []

       def enqueue(self, item):
           self.stack.append(item)

       def dequeue(self):
           if not self.stack:
               return "Queue is empty!"
           if len(self.stack) == 1:
               return self.stack.pop()
           temp = self.stack.pop()
           result = self.dequeue()
           self.stack.append(temp)
           return result
   ```

### 35. **What is a circular buffer, and how is it related to a queue?**
   - **Answer**: A circular buffer is a fixed-size queue where the tail wraps around to the head, making efficient use of space.

### 36. **How do you check for balanced parentheses using a queue?**
   - **Answer**: A queue is not suitable for checking balanced parentheses, but a stack can be used effectively for this purpose.

### 37. **What is a multi-level queue?**
   - **Answer**: It is a scheduling algorithm where processes are divided into multiple queues based on their priority or other criteria.

### 38. **Explain how a `PriorityQueue` in Java differs from a regular queue.**
   - **Answer**: A `PriorityQueue` orders its elements based on their priority (natural or custom), whereas a regular queue orders by insertion time (FIFO).

### 39. **Can you implement a queue with a max capacity in Python?**
   - **Answer**: Yes, using the `collections.deque` with a `maxlen` argument.
   - **Code**:
   ```python
   from collections import deque

   queue = deque(maxlen=5)
   queue.append(1)  # Enqueue
   queue.popleft()  # Dequeue
   ```

### 40. **What is the primary difference between a circular queue and a linear queue?**
   - **Answer**: A **circular queue** wraps around when the end is reached, whereas a **linear queue** stops at the end of the array, potentially wasting space.

---

### 41. **How do you implement a task scheduler using a queue?**
   - **Answer**: Enqueue tasks and process them in FIFO order, using a priority queue if tasks have varying priority.

### 42. **How can a queue be used to implement the producer-consumer problem?**
   - **Answer**: A bounded queue is used as a buffer between the producer (enqueue) and consumer (dequeue) processes.

### 43. **How would you reverse the first `k` elements of a queue?**
   - **Answer**: Use a stack to reverse the first `k` elements, then append them back to the queue.
   - **Code**:
   ```python
   from collections import deque

   def reverse_first_k(queue, k):
       stack = []
       for _ in range(k):
           stack.append(queue.popleft())
       while stack:
           queue.append(stack.pop())
       for _ in range(len(queue) - k):
           queue.append(queue.popleft())
   ```

### 44. **Explain the concept of a sliding window and how a deque is used in its implementation.**
   - **Answer**: In sliding window problems, a deque is used to store useful elements for each window, helping find maximums, minimums, or other properties in the window efficiently.

### 45. **What is the difference between an unbounded queue and a bounded queue?**
   - **Answer**: A **bounded queue** has a fixed maximum size, while an **unbounded queue** can grow indefinitely.

### 46. **What is the worst-case time complexity of the `dequeue()` operation in a queue implemented with an array?**
   - **Answer**: **O(n)** because all elements need to be shifted left after a dequeue operation.

### 47. **How do you sort a queue?**
   - **Answer**: Convert the queue to a list, sort it, and re-enqueue the elements.
   - **Code**:
   ```python
   from queue import Queue

   def sort_queue(q):
       lst = []
       while not q.empty():
           lst.append(q.get())
       lst.sort()
       for item in lst:
           q.put(item)
   ```

### 48. **What are the key differences between a queue and a priority queue?**
   - **Answer**: In a **queue**, elements are dequeued in FIFO order, while in a **priority queue**, elements are dequeued based on priority.

### 49. **What is a circular deque?**
   - **Answer**: A circular deque is a deque where both ends wrap around the circular buffer.

### 50. **How would you implement a simple printer job queue system?**
   - **Answer**: Use a queue to hold print jobs, where the jobs are processed in the order they are received.

---

This completes the set of 50 interview questions on the **Queue** data structure, covering various concepts, use cases, and implementations. Let me know if you need any further explanations or modifications!