Sure! Here's the previous content formatted in **Markdown**.

---

# Bit Manipulation Questions and Solutions

## 1. Set a Specific Bit

**Question:**  
Set the bit at a given position to `1`.

**Code:**
```python
def set_bit(num, pos):
    return num | (1 << pos)
```

**Example:**
```python
num = 10  # Binary: 1010
pos = 1
print(set_bit(num, pos))  # Output: 10 (binary: 1010, as bit 1 is already set)
pos = 2
print(set_bit(num, pos))  # Output: 14 (binary: 1110, as bit 2 is set)
```

---

## 2. Clear a Specific Bit

**Question:**  
Clear the bit at a given position (set it to `0`).

**Code:**
```python
def clear_bit(num, pos):
    return num & ~(1 << pos)
```

**Example:**
```python
num = 10  # Binary: 1010
pos = 3
print(clear_bit(num, pos))  # Output: 2 (binary: 0010, bit 3 is cleared)
```

---

## 3. Toggle a Specific Bit

**Question:**  
Toggle the bit at a given position (if it's `1`, change it to `0`, and vice versa).

**Code:**
```python
def toggle_bit(num, pos):
    return num ^ (1 << pos)
```

**Example:**
```python
num = 10  # Binary: 1010
pos = 1
print(toggle_bit(num, pos))  # Output: 8 (binary: 1000, bit 1 is toggled to 0)
pos = 3
print(toggle_bit(num, pos))  # Output: 2 (binary: 0010, bit 3 is toggled to 0)
```

---

## 4. Check if a Bit is Set

**Question:**  
Check if the bit at a given position is set to `1`.

**Code:**
```python
def is_bit_set(num, pos):
    return (num & (1 << pos)) != 0
```

**Example:**
```python
num = 10  # Binary: 1010
pos = 3
print(is_bit_set(num, pos))  # Output: True (bit 3 is 1)
pos = 1
print(is_bit_set(num, pos))  # Output: True (bit 1 is 1)
```

---

## 5. Turn Off the Rightmost 1-Bit

**Question:**  
Turn off the rightmost `1`-bit in a number (i.e., set it to `0`).

**Code:**
```python
def turn_off_rightmost_bit(n):
    return n & (n - 1)
```

**Example:**
```python
n = 12  # Binary: 1100
print(turn_off_rightmost_bit(n))  # Output: 8 (binary: 1000)
```

---

## 6. Isolate the Rightmost 1-Bit

**Question:**  
Isolate (extract) the rightmost `1`-bit in a number.

**Code:**
```python
def isolate_rightmost_bit(n):
    return n & -n
```

**Example:**
```python
n = 12  # Binary: 1100
print(isolate_rightmost_bit(n))  # Output: 4 (binary: 0100)
```

---

## 7. Reverse the Bits of a Number

**Question:**  
Reverse the bits of a given 32-bit unsigned integer.

**Code:**
```python
def reverse_bits(n):
    result = 0
    for i in range(32):
        result <<= 1
        result |= (n & 1)
        n >>= 1
    return result
```

**Example:**
```python
n = 43261596  # Binary: 00000010100101000001111010011100
print(reverse_bits(n))  # Output: 964176192 (binary: 00111001011110000010100101000000)
```

---

## 8. Count the Number of Leading Zeros

**Question:**  
Count the number of leading zeros in the binary representation of a number.

**Code:**
```python
def count_leading_zeros(num):
    if num == 0:
        return 32  # For 32-bit integers
    count = 0
    for i in range(31, -1, -1):
        if (num & (1 << i)) == 0:
            count += 1
        else:
            break
    return count
```

**Example:**
```python
num = 8  # Binary: 00000000000000000000000000001000
print(count_leading_zeros(num))  # Output: 28
```

---

## 9. Count the Number of Trailing Zeros

**Question:**  
Count the number of trailing zeros in the binary representation of a number.

**Code:**
```python
def count_trailing_zeros(n):
    if n == 0:
        return 32
    count = 0
    while (n & 1) == 0:
        count += 1
        n >>= 1
    return count
```

**Example:**
```python
n = 16  # Binary: 00000000000000000000000000010000
print(count_trailing_zeros(n))  # Output: 4
```

---

## 10. Find Position of Most Significant Set Bit

**Question:**  
Find the position of the most significant set bit (the leftmost `1` in binary representation).

**Code:**
```python
def find_most_significant_bit(num):
    pos = -1
    while num > 0:
        pos += 1
        num >>= 1
    return pos
```

**Example:**
```python
num = 18  # Binary: 10010
print(find_most_significant_bit(num))  # Output: 4 (as the most significant bit is at position 4)
```

---

## 11. Find XOR of All Numbers from 1 to n

**Question:**  
Find the XOR of all numbers from `1` to `n`.

**Code:**
```python
def xor_from_1_to_n(n):
    if n % 4 == 0:
        return n
    elif n % 4 == 1:
        return 1
    elif n % 4 == 2:
        return n + 1
    else:
        return 0
```

**Example:**
```python
n = 6
print(xor_from_1_to_n(n))  # Output: 7
```

---

## 12. Check if a Number Has Alternating Bits

**Question:**  
Check if a number has alternating `0`s and `1`s in its binary representation.

**Code:**
```python
def has_alternating_bits(n):
    n ^= (n >> 1)
    return (n & (n + 1)) == 0
```

**Example:**
```python
n = 5  # Binary: 101
print(has_alternating_bits(n))  # Output: True
n = 7  # Binary: 111
print(has_alternating_bits(n))  # Output: False
```

---

This list of questions and solutions should help you grasp various bit manipulation techniques commonly used in coding challenges and interviews.