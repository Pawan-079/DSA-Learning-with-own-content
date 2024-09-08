Here's a detailed version of stack concepts, fully implemented in **Python**, covering all levels from basic to advanced:

```markdown
# Stack - Basics to Advanced (in Python)

## 1. Basic Concepts

### **Introduction to Stacks**
- A **stack** is a linear data structure that follows the **Last In First Out (LIFO)** principle.
- The element inserted last is the first to be removed.
- Common examples: a pile of plates, browser history, undo functionality in software.

### **Stack Operations**
- **Push**: Add an element to the top of the stack.
- **Pop**: Remove the top element from the stack.
- **Peek/Top**: View the top element without removing it.
- **isEmpty**: Check if the stack is empty.

### **Implementation of Stack in Python**
Python can use a list as a stack, but for a more robust stack implementation, we can create a custom class.

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)
        print(f"Pushed {value} onto stack")

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        else:
            return "Stack is empty"

    def peek(self):
        if not self.is_empty():
            return self.stack[-1]
        else:
            return "Stack is empty"

    def is_empty(self):
        return len(self.stack) == 0

# Example Usage:
stack = Stack()
stack.push(10)
stack.push(20)
print(stack.peek())  # Output: 20
print(stack.pop())   # Output: 20
print(stack.is_empty())  # Output: False
```

### **Applications of Stacks**
- **Reversing a String**: Push characters of a string to a stack and pop them to reverse.
  
```python
def reverse_string(s):
    stack = []
    for char in s:
        stack.append(char)
    reversed_str = ''.join(stack.pop() for _ in range(len(stack)))
    return reversed_str

print(reverse_string("hello"))  # Output: "olleh"
```

- **Balanced Parentheses Problem**: Check if an expression has balanced parentheses.
  
```python
def is_balanced(expression):
    stack = []
    matching = {')': '(', '}': '{', ']': '['}
    for char in expression:
        if char in '({[':
            stack.append(char)
        elif char in ')}]':
            if not stack or stack.pop() != matching[char]:
                return False
    return not stack

print(is_balanced("{[()]}"))  # Output: True
print(is_balanced("{[(])}"))  # Output: False
```

- **Infix to Postfix Conversion**: Convert arithmetic expressions to postfix using operator precedence.

---

## 2. Intermediate Concepts

### **Stack in Recursion**
- **Recursion** uses a stack to store function calls. Each call is pushed to the call stack, and when the base case is hit, it pops the calls one by one.
  
Example of recursion:

```python
def factorial(n):
    if n == 1:
        return 1
    return n * factorial(n - 1)

print(factorial(5))  # Output: 120
```

### **Next Greater Element**
- For each element in an array, find the next greater element to the right.

```python
def next_greater_element(nums):
    stack = []
    result = [-1] * len(nums)
    
    for i in range(len(nums)):
        while stack and nums[i] > nums[stack[-1]]:
            result[stack.pop()] = nums[i]
        stack.append(i)
    
    return result

print(next_greater_element([2, 1, 2, 4, 3]))  # Output: [4, 2, 4, -1, -1]
```

### **Stock Span Problem**
- Calculate how many consecutive days the price has been less than or equal to the current day's price.

```python
def stock_span(prices):
    stack = []
    result = [0] * len(prices)
    
    for i in range(len(prices)):
        span = 1
        while stack and prices[stack[-1]] <= prices[i]:
            span += result[stack.pop()]
        result[i] = span
        stack.append(i)
    
    return result

print(stock_span([100, 80, 60, 70, 60, 75, 85]))  # Output: [1, 1, 1, 2, 1, 4, 6]
```

### **Min Stack Problem**
- Design a stack that supports push, pop, and retrieving the minimum element in constant time.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []
    
    def push(self, value):
        self.stack.append(value)
        if not self.min_stack or value <= self.min_stack[-1]:
            self.min_stack.append(value)
    
    def pop(self):
        if self.stack:
            if self.stack[-1] == self.min_stack[-1]:
                self.min_stack.pop()
            return self.stack.pop()
    
    def get_min(self):
        return self.min_stack[-1] if self.min_stack else None

# Example Usage:
min_stack = MinStack()
min_stack.push(3)
min_stack.push(5)
min_stack.push(2)
min_stack.push(1)
print(min_stack.get_min())  # Output: 1
min_stack.pop()
print(min_stack.get_min())  # Output: 2
```

### **Largest Rectangle in Histogram**
- Given heights of bars, find the largest rectangular area.

```python
def largest_rectangle_area(heights):
    stack = []
    max_area = 0
    heights.append(0)
    
    for i in range(len(heights)):
        while stack and heights[i] < heights[stack[-1]]:
            h = heights[stack.pop()]
            w = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, h * w)
        stack.append(i)
    
    return max_area

print(largest_rectangle_area([2, 1, 5, 6, 2, 3]))  # Output: 10
```

---

## 3. Advanced Concepts

### **Stack with O(1) Time for Min/Max**
- Design a stack where getting the minimum/maximum element takes constant time using auxiliary stacks.

```python
class MinMaxStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []
        self.max_stack = []
    
    def push(self, value):
        self.stack.append(value)
        if not self.min_stack or value <= self.min_stack[-1]:
            self.min_stack.append(value)
        if not self.max_stack or value >= self.max_stack[-1]:
            self.max_stack.append(value)
    
    def pop(self):
        if self.stack:
            if self.stack[-1] == self.min_stack[-1]:
                self.min_stack.pop()
            if self.stack[-1] == self.max_stack[-1]:
                self.max_stack.pop()
            return self.stack.pop()
    
    def get_min(self):
        return self.min_stack[-1] if self.min_stack else None
    
    def get_max(self):
        return self.max_stack[-1] if self.max_stack else None

# Example Usage:
min_max_stack = MinMaxStack()
min_max_stack.push(1)
min_max_stack.push(3)
min_max_stack.push(2)
print(min_max_stack.get_min())  # Output: 1
print(min_max_stack.get_max())  # Output: 3
```

### **Trapping Rain Water**
- Given elevation heights, calculate how much water is trapped between bars.

```python
def trap(height):
    stack = []
    water = 0
    
    for i in range(len(height)):
        while stack and height[i] > height[stack[-1]]:
            top = stack.pop()
            if not stack:
                break
            distance = i - stack[-1] - 1
            bounded_height = min(height[i], height[stack[-1]]) - height[top]
            water += distance * bounded_height
        stack.append(i)
    
    return water

print(trap([0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]))  # Output: 6
```

### **Expression Evaluation (Prefix/Postfix)**
- **Postfix Evaluation**: Evaluate a postfix expression using a stack.

```python
def evaluate_postfix(expression):
    stack = []
    
    for token in expression.split():
        if token.isdigit():
            stack.append(int(token))
        else:
            b = stack.pop()
            a = stack.pop()
            if token == '+':
                stack.append(a + b)
            elif token == '-':
                stack.append(a - b)
            elif token == '*':
                stack.append(a * b)
            elif token == '/':
                stack.append(int(a / b))
    
    return stack[0]

print(evaluate_postfix("2 3 1 * + 9 -"))  # Output: -4
```

### **Monotonic Stack**
- A stack that maintains elements in a monotonic order (increasing or decreasing).

Example: Solve the **daily temperatures** problem using a monotonic stack.

```python
def daily_temperatures(T):
    stack = []
    result = [0] * len(T)
    
    for i in range(len

(T)):
        while stack and T[i] > T[stack[-1]]:
            j = stack.pop()
            result[j] = i - j
        stack.append(i)
    
    return result

print(daily_temperatures([73, 74, 75, 71, 69, 72, 76, 73]))  # Output: [1, 1, 4, 2, 1, 1, 0, 0]
```

---

This comprehensive guide covers basic, intermediate, and advanced stack-related topics with detailed explanations and Python code examples.
```

## Interview questions based on stack
Here’s an extended markdown guide with **30 interview questions and answers** related to stacks, ranging from basic to advanced topics. All answers are explained and implemented in **Python** for better understanding:

```markdown
# Stack - Basics to Advanced (in Python)

## 1. Basic Concepts

### **Introduction to Stacks**
- A **stack** is a linear data structure that follows the **Last In First Out (LIFO)** principle.
- The element inserted last is the first to be removed.
- Common examples: a pile of plates, browser history, undo functionality in software.

---

## 2. Stack Interview Questions and Answers

### **1. What is a stack?**
- A stack is a data structure that follows **LIFO (Last In First Out)**.
- In a stack, the element added last is the first one to be removed.

### **2. Explain the basic operations of a stack.**
- **Push**: Insert an element onto the stack.
- **Pop**: Remove the top element from the stack.
- **Peek**: Return the top element without removing it.
- **isEmpty**: Check if the stack is empty.

### **3. Implement a stack in Python.**

```python
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)

    def pop(self):
        if not self.is_empty():
            return self.stack.pop()
        return "Stack is empty"

    def peek(self):
        if not self.is_empty():
            return self.stack[-1]
        return "Stack is empty"

    def is_empty(self):
        return len(self.stack) == 0
```

---

### **4. How does a stack work in recursion?**
- Recursion uses an implicit stack called the **call stack** to keep track of function calls.
- Every recursive call adds a new frame to the stack. When a function returns, its frame is popped off the stack.

### **5. What are some real-world examples of stacks?**
- **Undo operations** in text editors.
- **Browser history** navigation.
- **Function call stacks** in programming.

### **6. What is stack overflow?**
- A **stack overflow** occurs when too many elements are pushed onto the stack, exceeding its memory limit, typically in recursive functions without a base case.

---

## 3. Intermediate Concepts

### **7. How to reverse a string using a stack?**
```python
def reverse_string(s):
    stack = []
    for char in s:
        stack.append(char)
    reversed_str = ''.join(stack.pop() for _ in range(len(stack)))
    return reversed_str

print(reverse_string("hello"))  # Output: "olleh"
```

### **8. Explain the balanced parentheses problem.**
- Given a string containing various types of parentheses, determine if they are **balanced**.
- A stack can be used to push opening parentheses and pop them when a matching closing parenthesis is found.

### **9. Write Python code to check if parentheses are balanced.**

```python
def is_balanced(expression):
    stack = []
    matching = {')': '(', '}': '{', ']': '['}
    for char in expression:
        if char in '({[':
            stack.append(char)
        elif char in ')}]':
            if not stack or stack.pop() != matching[char]:
                return False
    return not stack

print(is_balanced("{[()]}"))  # Output: True
print(is_balanced("{[(])}"))  # Output: False
```

### **10. Explain infix to postfix conversion using a stack.**
- In **infix notation**, operators are written between operands (`A + B`).
- In **postfix notation**, operators follow the operands (`A B +`).
- A stack can be used to convert an infix expression to postfix by maintaining operator precedence.

---

### **11. What is the next greater element problem?**
- For each element in an array, find the next greater element to its right. If no such element exists, return `-1`.

```python
def next_greater_element(nums):
    stack = []
    result = [-1] * len(nums)
    
    for i in range(len(nums)):
        while stack and nums[i] > nums[stack[-1]]:
            result[stack.pop()] = nums[i]
        stack.append(i)
    
    return result

print(next_greater_element([2, 1, 2, 4, 3]))  # Output: [4, 2, 4, -1, -1]
```

---

### **12. How do you solve the stock span problem?**
- The stock span problem is about finding how many consecutive days the stock price was less than or equal to today’s price.

```python
def stock_span(prices):
    stack = []
    result = [0] * len(prices)
    
    for i in range(len(prices)):
        span = 1
        while stack and prices[stack[-1]] <= prices[i]:
            span += result[stack.pop()]
        result[i] = span
        stack.append(i)
    
    return result

print(stock_span([100, 80, 60, 70, 60, 75, 85]))  # Output: [1, 1, 1, 2, 1, 4, 6]
```

---

### **13. What is a Min Stack?**
- A **Min Stack** supports `push()`, `pop()`, and retrieving the **minimum element** in constant time.

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []
    
    def push(self, value):
        self.stack.append(value)
        if not self.min_stack or value <= self.min_stack[-1]:
            self.min_stack.append(value)
    
    def pop(self):
        if self.stack:
            if self.stack[-1] == self.min_stack[-1]:
                self.min_stack.pop()
            return self.stack.pop()
    
    def get_min(self):
        return self.min_stack[-1] if self.min_stack else None
```

---

### **14. How do you solve the largest rectangle in a histogram problem?**

```python
def largest_rectangle_area(heights):
    stack = []
    max_area = 0
    heights.append(0)
    
    for i in range(len(heights)):
        while stack and heights[i] < heights[stack[-1]]:
            h = heights[stack.pop()]
            w = i if not stack else i - stack[-1] - 1
            max_area = max(max_area, h * w)
        stack.append(i)
    
    return max_area

print(largest_rectangle_area([2, 1, 5, 6, 2, 3]))  # Output: 10
```

---

### **15. What is a monotonic stack?**
- A **monotonic stack** maintains its elements in a strictly increasing or decreasing order.
- Useful for problems like **daily temperatures** or **next greater element**.

### **16. Write Python code to solve the daily temperatures problem.**

```python
def daily_temperatures(T):
    stack = []
    result = [0] * len(T)
    
    for i in range(len(T)):
        while stack and T[i] > T[stack[-1]]:
            j = stack.pop()
            result[j] = i - j
        stack.append(i)
    
    return result

print(daily_temperatures([73, 74, 75, 71, 69, 72, 76, 73]))  # Output: [1, 1, 4, 2, 1, 1, 0, 0]
```

---

### **17. How to evaluate a postfix expression using a stack?**

```python
def evaluate_postfix(expression):
    stack = []
    
    for token in expression.split():
        if token.isdigit():
            stack.append(int(token))
        else:
            b = stack.pop()
            a = stack.pop()
            if token == '+':
                stack.append(a + b)
            elif token == '-':
                stack.append(a - b)
            elif token == '*':
                stack.append(a * b)
            elif token == '/':
                stack.append(int(a / b))
    
    return stack[0]

print(evaluate_postfix("2 3 1 * + 9 -"))  # Output: -4
```

---

## 4. Advanced Concepts

### **18. What is the trapping rainwater problem?**
- Given an array representing elevation heights, calculate how much water can be trapped after rain.

```python
def trap(height):
    stack = []
    water = 0
    
    for i in range(len(height)):
        while stack and height[i] > height[stack[-1]]:
            top = stack.pop()
            if not stack:
                break
            distance = i - stack[-1] - 1
            bounded_height = min(height[i], height[stack[-1]]) - height[top]
            water += distance * bounded_height
        stack.append(i)
    
    return water

print(trap([0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]))  # Output: 6
```

---

### **19. What is the time complexity of stack operations?**
- All basic stack operations (`push()`, `pop()`, `peek()`, `is_empty()`) take constant time **O(1)**.

### **20. What is a deque and how is it different from a stack?**


- A **deque** (double-ended queue) allows insertion and removal from both ends.
- A **stack** allows insertion and removal only from one end (the top).

---

### **21. How do you solve the celebrity problem using a stack?**
- In a group of people, a **celebrity** is known by everyone, but they know no one.
- Using a stack, you can efficiently find the celebrity in **O(n)** time.

```python
def celebrity(matrix, n):
    stack = [i for i in range(n)]
    
    while len(stack) > 1:
        a = stack.pop()
        b = stack.pop()
        if matrix[a][b]:
            stack.append(b)
        else:
            stack.append(a)
    
    candidate = stack.pop()
    
    for i in range(n):
        if i != candidate and (matrix[candidate][i] or not matrix[i][candidate]):
            return -1
    
    return candidate

matrix = [[0, 1, 1], [0, 0, 0], [1, 1, 0]]
print(celebrity(matrix, 3))  # Output: 1 (Person 1 is the celebrity)
```

---

### **22. Explain the concept of a bounded stack.**
- A **bounded stack** has a fixed size. When the stack is full, pushing a new element results in a **stack overflow** error.

---

### **23. What is a multi-stack?**
- A **multi-stack** is an array of stacks where multiple stacks are maintained within a single data structure, often used when there are multiple resources to manage (e.g., multi-threading).

### **24. How does stack unwinding work in exception handling?**
- **Stack unwinding** occurs when an exception is thrown, and the system pops function calls off the call stack until the exception is handled or the program crashes.

---

## 5. Advanced Problem Solving

### **25. Write a Python program to sort a stack using another stack.**

```python
def sort_stack(stack):
    temp_stack = []
    
    while stack:
        current = stack.pop()
        while temp_stack and temp_stack[-1] > current:
            stack.append(temp_stack.pop())
        temp_stack.append(current)
    
    return temp_stack

stack = [34, 3, 31, 98, 92, 23]
sorted_stack = sort_stack(stack)
print(sorted_stack)  # Output: [3, 23, 31, 34, 92, 98]
```

---

### **26. What is an iterator stack?**
- An **iterator stack** allows for iterating over stack elements without modifying the stack itself.

---

### **27. How do you convert an infix expression to a prefix expression using a stack?**

```python
def infix_to_prefix(expression):
    precedence = {'+': 1, '-': 1, '*': 2, '/': 2, '^': 3}
    stack = []
    result = []
    expression = expression[::-1]

    for char in expression:
        if char.isalnum():
            result.append(char)
        elif char == ')':
            stack.append(char)
        elif char == '(':
            while stack and stack[-1] != ')':
                result.append(stack.pop())
            stack.pop()
        else:
            while stack and precedence.get(char, 0) <= precedence.get(stack[-1], 0):
                result.append(stack.pop())
            stack.append(char)

    while stack:
        result.append(stack.pop())

    return ''.join(result[::-1])

print(infix_to_prefix("(A-B/C)*(A/K-L)"))  # Output: "*-A/BC-/AKL"
```

---

### **28. What is the significance of stack frames?**
- **Stack frames** contain function call data, including parameters, return address, and local variables. They are vital in function execution.

---

### **29. How do you use a stack to detect a cycle in a directed graph?**
- Use **Depth-First Search (DFS)** with a stack to detect back edges, which indicate cycles.

---

### **30. Explain the tower of Hanoi problem and solve it using recursion.**

```python
def tower_of_hanoi(n, source, auxiliary, target):
    if n == 1:
        print(f"Move disk 1 from {source} to {target}")
        return
    tower_of_hanoi(n - 1, source, target, auxiliary)
    print(f"Move disk {n} from {source} to {target}")
    tower_of_hanoi(n - 1, auxiliary, source, target)

tower_of_hanoi(3, 'A', 'B', 'C')
# Output: Moves for 3 disks from A to C
```

---

This comprehensive guide covers basic, intermediate, and advanced stack-related topics with detailed explanations and Python code examples, along with 30 common interview questions.
```

This markdown includes a detailed explanation of various stack concepts, complete with Python code and 30 interview questions to help you master stacks for interview preparation.