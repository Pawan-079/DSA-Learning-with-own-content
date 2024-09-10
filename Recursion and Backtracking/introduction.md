Sure! Here's the introduction to recursion in **Markdown** format with the necessary Python code for your notes.

```md
## Recursion

### Introduction to Recursion

Recursion is a method where a function calls itself to solve smaller instances of a problem. The function keeps calling itself with different arguments until it reaches a base case. 

### Key Components of Recursion:
1. **Base Case**: This is the condition at which the recursive function stops calling itself. Without a base case, the function would call itself indefinitely, leading to a stack overflow.
2. **Recursive Case**: This is the part where the function calls itself to solve a smaller version of the problem, working its way towards the base case.

### Example: Factorial of a Number

The factorial of a number `n`, denoted as `n!`, is the product of all positive integers up to `n`. Mathematically, it can be defined as:

\[
n! = 
\begin{cases} 
1 & \text{if } n = 0 \\
n \times (n-1)! & \text{if } n > 0
\end{cases}
\]

### Python Code for Factorial using Recursion:
```python
def factorial(n):
    # Base case: factorial of 0 is 1
    if n == 0:
        return 1
    # Recursive case: n * factorial(n-1)
    return n * factorial(n - 1)

# Testing the factorial function
num = 5
print(f"Factorial of {num} is: {factorial(num)}")
```

### Explanation:

1. The function `factorial(n)` calls itself with a smaller value of `n` (i.e., `n-1`) until it reaches the base case where `n == 0`.
2. When the base case is reached, it returns `1`, and the recursion starts to unwind, calculating the product of `n` and the result of `factorial(n-1)`.

### Trace of Recursive Calls (for `n = 5`):

- `factorial(5)` calls `factorial(4)`
- `factorial(4)` calls `factorial(3)`
- `factorial(3)` calls `factorial(2)`
- `factorial(2)` calls `factorial(1)`
- `factorial(1)` calls `factorial(0)` (base case reached)
- Now, the results are returned back up:
  - `factorial(1) = 1`
  - `factorial(2) = 2 * 1 = 2`
  - `factorial(3) = 3 * 2 = 6`
  - `factorial(4) = 4 * 6 = 24`
  - `factorial(5) = 5 * 24 = 120`

Thus, `factorial(5)` returns `120`.

```

This explanation covers the introduction to recursion, the factorial example, and the necessary Python code with explanations.