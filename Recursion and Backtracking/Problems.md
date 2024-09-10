## - Problems:
#  - Fibonacci Sequence
#  - N-Queens Problem
# - Rat in a Maze
```md
## Backtracking Problems

### 1. Fibonacci Sequence (Using Recursion)

The **Fibonacci Sequence** is a series of numbers in which each number is the sum of the two preceding ones, starting from 0 and 1. The sequence follows this pattern:

\[
F(0) = 0, \quad F(1) = 1
\]
\[
F(n) = F(n-1) + F(n-2) \text{ for } n \geq 2
\]

### Python Code for Fibonacci Sequence Using Recursion:
```python
def fibonacci(n):
    # Base case
    if n == 0:
        return 0
    elif n == 1:
        return 1
    # Recursive case
    return fibonacci(n - 1) + fibonacci(n - 2)

# Testing the Fibonacci function
num = 10
print(f"Fibonacci sequence at position {num}: {fibonacci(num)}")
```

### Explanation:
- The `fibonacci(n)` function recursively calls itself until it reaches the base cases (`n == 0` or `n == 1`).
- It computes the sum of the two previous Fibonacci numbers for `n >= 2`.

### Time Complexity:
- **O(2^n)** due to overlapping subproblems.
- Can be optimized using **Dynamic Programming** or **Memoization**.

---

### 2. N-Queens Problem (Backtracking)

The **N-Queens problem** involves placing N queens on an N×N chessboard such that no two queens threaten each other. This means:
- No two queens should share the same row, column, or diagonal.

### Python Code for N-Queens Problem:
```python
def is_safe(board, row, col, N):
    # Check this row on the left side
    for i in range(col):
        if board[row][i] == 1:
            return False
    # Check upper diagonal on the left side
    for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
    # Check lower diagonal on the left side
    for i, j in zip(range(row, N), range(col, -1, -1)):
        if board[i][j] == 1:
            return False
    return True

def solve_nqueens(board, col, N):
    if col >= N:
        return True
    for i in range(N):
        if is_safe(board, i, col, N):
            board[i][col] = 1
            if solve_nqueens(board, col + 1, N):
                return True
            board[i][col] = 0
    return False

def nqueens(N):
    board = [[0 for _ in range(N)] for _ in range(N)]
    if not solve_nqueens(board, 0, N):
        print("Solution does not exist.")
        return
    for row in board:
        print(row)

# Testing N-Queens for N = 4
nqueens(4)
```

### Explanation:
- The function `is_safe` checks if placing a queen at a given position is safe.
- The `solve_nqueens` function tries to place queens one by one and backtracks when it encounters a conflict.
- The chessboard is printed with `1` representing the position of a queen and `0` for empty spaces.

### Time Complexity:
- **O(N!)**, as the problem explores all possible arrangements of queens.

---

### 3. Rat in a Maze (Backtracking)

The **Rat in a Maze** problem is a grid-based problem where a rat has to find a path from the start to the destination while only moving through valid (open) cells. The rat can move up, down, left, or right.

### Problem Setup:
- Given a 2D grid (maze), where `1` represents an open path and `0` represents a blocked cell, the rat starts at the top-left corner (0, 0) and has to reach the bottom-right corner (N-1, N-1).

### Python Code for Rat in a Maze Problem:
```python
def is_safe(maze, x, y, N):
    return 0 <= x < N and 0 <= y < N and maze[x][y] == 1

def solve_maze_util(maze, x, y, sol, N):
    # If the rat reaches the destination
    if x == N - 1 and y == N - 1 and maze[x][y] == 1:
        sol[x][y] = 1
        return True

    # Check if maze[x][y] is valid
    if is_safe(maze, x, y, N):
        # Mark this cell as part of the solution
        sol[x][y] = 1
        
        # Move right in the maze
        if solve_maze_util(maze, x, y + 1, sol, N):
            return True
        
        # Move down in the maze
        if solve_maze_util(maze, x + 1, y, sol, N):
            return True
        
        # If neither move is valid, backtrack
        sol[x][y] = 0
        return False
    return False

def solve_maze(maze, N):
    sol = [[0 for _ in range(N)] for _ in range(N)]
    if not solve_maze_util(maze, 0, 0, sol, N):
        print("No solution exists.")
        return
    for row in sol:
        print(row)

# Example maze (4x4)
maze = [
    [1, 0, 0, 0],
    [1, 1, 0, 1],
    [0, 1, 0, 0],
    [1, 1, 1, 1]
]

# Testing Rat in a Maze for N = 4
solve_maze(maze, 4)
```

### Explanation:
- The function `is_safe` checks if the rat can move to a particular cell.
- `solve_maze_util` explores all possible paths (right or down), and if it hits a dead-end, it backtracks and tries another path.
- The solution matrix `sol` is updated with `1` representing the path taken by the rat.

### Time Complexity:
- **O(2^(N^2))**, as the rat can move in two directions (right or down) and the algorithm explores all possible paths.

---

### Summary

| Problem            | Approach   | Time Complexity  | Explanation                                         |
|--------------------|------------|------------------|-----------------------------------------------------|
| **Fibonacci**       | Recursion  | O(2^n)           | Simple recursion to compute the Fibonacci series.    |
| **N-Queens**        | Backtracking | O(N!)            | Place N queens on an N×N board without conflicts.    |
| **Rat in a Maze**   | Backtracking | O(2^(N^2))       | Find a path from start to end in a maze using recursion. |
```

This Markdown contains explanations and code for each of the three backtracking problems, including Fibonacci sequence, N-Queens problem, and Rat in a Maze, along with time complexities and example outputs.