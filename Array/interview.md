Here are some array-related interview questions in Python, formatted in Markdown:

```markdown
# Array Interview Questions in Python

## 1. Two Sum
**Problem:**
Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

**Example:**
```python
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Solution:**
```python
def two_sum(nums, target):
    lookup = {}
    for i, num in enumerate(nums):
        if target - num in lookup:
            return [lookup[target - num], i]
        lookup[num] = i
```

---

## 2. Find the Missing Number
**Problem:**
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

**Example:**
```python
Input: nums = [3, 0, 1]
Output: 2
```

**Solution:**
```python
def missing_number(nums):
    n = len(nums)
    total = n * (n + 1) // 2
    return total - sum(nums)
```

---

## 3. Maximum Subarray (Kadane’s Algorithm)
**Problem:**
Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**
```python
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The contiguous subarray [4,-1,2,1] has the largest sum = 6.
```

**Solution:**
```python
def max_subarray(nums):
    current_sum = max_sum = nums[0]
    for num in nums[1:]:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)
    return max_sum
```

---

## 4. Product of Array Except Self
**Problem:**
Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Example:**
```python
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Solution:**
```python
def product_except_self(nums):
    length = len(nums)
    answer = [0] * length
    answer[0] = 1

    for i in range(1, length):
        answer[i] = nums[i - 1] * answer[i - 1]

    right_product = 1
    for i in reversed(range(length)):
        answer[i] *= right_product
        right_product *= nums[i]

    return answer
```

---

## 5. Merge Two Sorted Arrays
**Problem:**
Given two sorted integer arrays `nums1` and `nums2`, merge `nums2` into `nums1` as one sorted array.

**Example:**
```python
Input: nums1 = [1,2,3,0,0,0], nums2 = [2,5,6]
Output: [1,2,2,3,5,6]
```

**Solution:**
```python
def merge(nums1, m, nums2, n):
    while m > 0 and n > 0:
        if nums1[m - 1] > nums2[n - 1]:
            nums1[m + n - 1] = nums1[m - 1]
            m -= 1
        else:
            nums1[m + n - 1] = nums2[n - 1]
            n -= 1
    if n > 0:
        nums1[:n] = nums2[:n]
```

---

## 6. Find All Duplicates in an Array
**Problem:**
Given an integer array `nums` of length `n` where all the integers are in the range `[1, n]` and each integer appears once or twice, return an array of all the integers that appear twice.

**Example:**
```python
Input: nums = [4,3,2,7,8,2,3,1]
Output: [2, 3]
```

**Solution:**
```python
def find_duplicates(nums):
    result = []
    for num in nums:
        if nums[abs(num) - 1] < 0:
            result.append(abs(num))
        else:
            nums[abs(num) - 1] *= -1
    return result
```

---

## 7. Rotate Array
**Problem:**
Given an array, rotate the array to the right by `k` steps, where `k` is non-negative.

**Example:**
```python
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]
```

**Solution:**
```python
def rotate(nums, k):
    k %= len(nums)
    nums[:] = nums[-k:] + nums[:-k]
```

---

## 8. First Missing Positive
**Problem:**
Given an unsorted integer array `nums`, return the smallest missing positive integer.

**Example:**
```python
Input: nums = [3,4,-1,1]
Output: 2
```

**Solution:**
```python
def first_missing_positive(nums):
    n = len(nums)
    for i in range(n):
        while 1 <= nums[i] <= n and nums[nums[i] - 1] != nums[i]:
            nums[nums[i] - 1], nums[i] = nums[i], nums[nums[i] - 1]

    for i in range(n):
        if nums[i] != i + 1:
            return i + 1
    return n + 1
```

---

## 9. Move Zeroes
**Problem:**
Given an array `nums`, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

**Example:**
```python
Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]
```

**Solution:**
```python
def move_zeroes(nums):
    non_zero_pos = 0
    for i in range(len(nums)):
        if nums[i] != 0:
            nums[non_zero_pos], nums[i] = nums[i], nums[non_zero_pos]
            non_zero_pos += 1
```

---

## 10. Trapping Rain Water
**Problem:**
Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

**Example:**
```python
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

**Solution:**
```python
def trap(height):
    if not height:
        return 0
    left, right = 0, len(height) - 1
    left_max, right_max = height[left], height[right]
    water = 0

    while left < right:
        if height[left] < height[right]:
            left += 1
            left_max = max(left_max, height[left])
            water += left_max - height[left]
        else:
            right -= 1
            right_max = max(right_max, height[right])
            water += right_max - height[right]
    
    return water
```
```

These are some common array-based interview questions in Python. Each solution uses efficient algorithms and patterns that are often discussed in technical interviews.