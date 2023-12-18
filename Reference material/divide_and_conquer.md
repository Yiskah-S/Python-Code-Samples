
# Table of Contents
- [Table of Contents](#table-of-contents)
    - [1. Merge Sort](#1-merge-sort)
    - [2. Quick Sort](#2-quick-sort)
    - [3. Karatsuba Algorithm for Large Number Multiplication](#3-karatsuba-algorithm-for-large-number-multiplication)
    - [4. Ternary Search:](#4-ternary-search)
      - [5. Smallest Missing Number:](#5-smallest-missing-number)
      - [6. Find Min and Max:](#6-find-min-and-max)

Overview
Divide and Conquer is an approach to problem solving that breaks down a large problem into multiple, smaller subproblems. We combine the results of those subproblems to solve the original problem.

When we write a divide-and-conquer solution we can follow these steps:

Break the problem into subproblems of the same type
Recursively solve the subproblems
Combine the solved subproblems to solve the larger problem
There can be several subproblems within a single problem, so we need to choose the correct subproblem involved. Most situations require us to divide the problem into two equal parts, but there are cases where a divide and conquer algorithm may require us to split the problem into three parts or more.

Solving the subproblems recursively requires us to carefully consider the input parameters for the recursive call of each subproblem. It is also crucial for us to have the correct base case for the recursion. To do so, we need to identify the smallest version of the subproblem for which we already know the solution.

Afterwards, we identify the correct operation for combining the solutions of the subproblems to get our final result.




### 1. Merge Sort

![Merge Sort](/images/mergesort.png)

- **Pros**: Highly efficient for large datasets.
- **Cons**: Requires additional memory for merging.


```python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        L = arr[:mid]
        R = arr[mid:]

        merge_sort(L)
        merge_sort(R)

        i = j = k = 0

        while i < len(L) and j < len(R):
            if L[i] < R[j]:
                arr[k] = L[i]
                i += 1
            else:
                arr[k] = R[j]
                j += 1
            k += 1

        while i < len(L):
            arr[k] = L[i]
            i += 1
            k += 1

        while j < len(R):
            arr[k] = R[j]
            j += 1
            k += 1
```

### 2. Quick Sort

![Quick Sort](/images/quicksort.png)

- **Pros**: Fast and requires little additional memory.
- **Cons**: Performance can degrade on sorted or nearly sorted data.

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + [pivot] + quick_sort(right)
```


### 3. Karatsuba Algorithm for Large Number Multiplication

- **Use Case**: Multiplying large numbers.
- **Pros**: Faster than traditional multiplication algorithms.
- **Cons**: More complex and less intuitive.

```python
def karatsuba_multiplication(x, y):
    # Convert numbers to strings for easier manipulation
    x_str = str(x)
    y_str = str(y)

    # Base case: If either of the numbers is single-digit, use regular multiplication
    if len(x_str) == 1 or len(y_str) == 1:
        return x * y

    # Make the lengths of x and y equal by padding with leading zeros if necessary
    max_len = max(len(x_str), len(y_str))
    x_str = x_str.zfill(max_len)
    y_str = y_str.zfill(max_len)

    # Split the numbers into halves
    mid = max_len // 2
    x_high, x_low = int(x_str[:-mid]), int(x_str[-mid:])
    y_high, y_low = int(y_str[:-mid]), int(y_str[-mid:])

    # Recursive calls for subproblems
    a = karatsuba_multiplication(x_high, y_high)
    b = karatsuba_multiplication(x_low, y_low)
    c = karatsuba_multiplication(x_high + x_low, y_high + y_low) - a - b

    # Combine the results using the Karatsuba formula
    result = a * (10 ** (2 * mid)) + c * (10 ** mid) + b

    return result
```


### 4. Ternary Search:

- **Use Case**: Finding the maximum or minimum of a unimodal function.
- **Pros**: Decreases the number of comparisons in some cases compared to binary search.
- **Cons**: The convergence rate is slower than binary search in the worst case.

```python
def ternary_search(f, left, right, absolute_precision):
    while abs(right - left) > absolute_precision:
        left_third = left + (right - left) / 3
        right_third = right - (right - left) / 3

        if f(left_third) < f(right_third):
            left = left_third
        else:
            right = right_third
    return (left + right) / 2
```

#### 5. Smallest Missing Number:

- **Use Case**: Finding the smallest missing number in a sorted array.
- **Pros**: Faster than linear search.
- **Cons**: Requires a sorted array.

```python
def smallest_missing_num(nums):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        mid = left + (right - left) // 2  # Calculate the middle index

        # If the element at the middle index matches its expected value (mid),
        # the smallest missing element must be to the right.
        if nums[mid] == mid:
            left = mid + 1
        else:
            right = mid - 1

    # After the loop, 'left' will be pointing to the first index where
    # the element does not match its expected value, which is the smallest missing element.
    return left

```
```python
def smallest_missing_num_helper(nums, left, right):  
    # base case
    # if the left index is greater than the right index
    if left > right:
        # the left index is the first missing number
        return left

    # calculate the middle index
    mid = (left + right) // 2

    # if the mid index matches with its value, then the mismatch must lie on the right half
    if nums[mid] == mid:
        return smallest_missing_num_helper(nums, mid + 1, right)
    # otherwise, the mismatch must lie on the left half
    else:
        return smallest_missing_num_helper(nums, left, mid - 1)

def smallest_missing_num(nums):
    return smallest_missing_num_helper(nums, 0, len(nums) - 1)
```
```python
def smallest_missing_num(nums, left=0, right=None):
    if right is None:
        right = len(nums) - 1

    if left > right:
        return left

    mid = left + (right - left) // 2
    if nums[mid] > mid:
        return smallest_missing_num(nums, left, mid - 1)
    else:
        return smallest_missing_num(nums, mid + 1, right)
```

#### 6. Find Min and Max:

- **Use Case**: Finding the minimum and maximum of an array.
- **Pros**: Faster than linear search.
- **Cons**: Requires a sorted array.

```python
import sys

# set initial values to the largest/smallest possible int (infinity)
def min_max_helper(nums, left, right, lowest_int=sys.maxsize, largest_int=-sys.maxsize):
    # base case, list size is 1
    if left == right:
        # initialize vars to min/max num from the list being looked at
        lowest_int = min(nums[left], lowest_int)
        largest_int = max(nums[left], largest_int)
        return lowest_int, largest_int
    
    mid = (left + right) // 2
    
    # recursion until all nums are looked at
    lowest_int, largest_int = min_max_helper(nums, left, mid, lowest_int, largest_int)
    lowest_int, largest_int = min_max_helper(nums, mid + 1, right, lowest_int, largest_int)
    
    return lowest_int, largest_int

def min_max(nums):
    return min_max_helper(nums, 0, len(nums) - 1)
```

```python
def min_max(nums):
    # Base case: If there's only one element in the list, return it as both min and max
    if len(nums) == 1:
        return (nums[0], nums[0])

    # Base case: If there are two elements, compare them and return as min and max
    if len(nums) == 2:
        return (min(nums[0], nums[1]), max(nums[0], nums[1]))

    # Divide the array into two halves
    mid = len(nums) // 2
    left_half = nums[:mid]
    right_half = nums[mid:]

    # Recursively find min and max in both halves
    left_min, left_max = min_max(left_half)
    right_min, right_max = min_max(right_half)

    # Combine the results
    overall_min = min(left_min, right_min)
    overall_max = max(left_max, right_max)

    return (overall_min, overall_max)
```



https://learn-2.galvanize.com/cohorts/3646/blocks/1277/content_files/01-algorithms/04-algorithms-divide-conquer.md