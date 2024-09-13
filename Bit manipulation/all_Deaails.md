Certainly! Here's a comprehensive guide on bit manipulation in Python, formatted in Markdown:

---

# Bit Manipulation in Python

Bit manipulation involves using bitwise operators to perform operations on binary representations of numbers. Python provides several bitwise operators and functions to manipulate bits.

## Bitwise Operators

### 1. **AND (`&`)**

Performs a bitwise AND operation between two integers.

**Syntax:**
```python
a & b
```

**Example:**
```python
a = 5      # 0b0101
b = 3      # 0b0011
result = a & b   # 0b0001 (1 in decimal)
```

### 2. **OR (`|`)**

Performs a bitwise OR operation between two integers.

**Syntax:**
```python
a | b
```

**Example:**
```python
a = 5      # 0b0101
b = 3      # 0b0011
result = a | b   # 0b0111 (7 in decimal)
```

### 3. **XOR (`^`)**

Performs a bitwise XOR (exclusive OR) operation between two integers.

**Syntax:**
```python
a ^ b
```

**Example:**
```python
a = 5      # 0b0101
b = 3      # 0b0011
result = a ^ b   # 0b0110 (6 in decimal)
```

### 4. **NOT (`~`)**

Performs a bitwise NOT (complement) operation, which inverts all the bits.

**Syntax:**
```python
~a
```

**Example:**
```python
a = 5      # 0b0101
result = ~a   # -0b0110 (-6 in decimal, due to two's complement representation)
```

### 5. **Left Shift (`<<`)**

Shifts the bits of a number to the left by a specified number of positions.

**Syntax:**
```python
a << n
```

**Example:**
```python
a = 5      # 0b0101
result = a << 1   # 0b1010 (10 in decimal)
```

### 6. **Right Shift (`>>`)**

Shifts the bits of a number to the right by a specified number of positions.

**Syntax:**
```python
a >> n
```

**Example:**
```python
a = 5      # 0b0101
result = a >> 1   # 0b0010 (2 in decimal)
```

## Bit Manipulation Techniques

### 1. **Checking if a Number is Power of 2**

A number is a power of 2 if it has exactly one bit set in its binary representation.

**Code:**
```python
def is_power_of_two(n):
    return (n & (n - 1)) == 0 and n > 0
```

**Example:**
```python
print(is_power_of_two(16))  # True
print(is_power_of_two(18))  # False
```

### 2. **Counting Set Bits (Hamming Weight)**

Counts the number of bits set to 1 in the binary representation of a number.

**Code:**
```python
def count_set_bits(n):
    count = 0
    while n:
        count += n & 1
        n >>= 1
    return count
```

**Example:**
```python
print(count_set_bits(9))  # 2 (binary: 1001)
```

### 3. **Finding the Only Non-Duplicated Element**

Given an array where every element occurs exactly twice except for one, find the non-duplicated element.

**Code:**
```python
def find_non_duplicated_element(nums):
    result = 0
    for num in nums:
        result ^= num
    return result
```

**Example:**
```python
print(find_non_duplicated_element([1, 2, 3, 2, 1]))  # 3
```

### 4. **Swapping Two Numbers**

Swaps two numbers without using a temporary variable.

**Code:**
```python
a = 5
b = 10
a ^= b
b ^= a
a ^= b
```

**Example:**
```python
print(a, b)  # 10 5
```

### 5. **Extracting Specific Bits**

Extracts specific bits from a number using bitwise operations.

**Code:**
```python
def extract_bits(num, start, length):
    mask = ((1 << length) - 1) << start
    return (num & mask) >> start
```

**Example:**
```python
print(extract_bits(0b101110, 1, 3))  # 0b011 (3 in decimal)
```

---

This guide should cover the essential aspects of bit manipulation in Python. Feel free to ask if you have any more questions or need further details!