# Table of Contents
- [Table of Contents](#table-of-contents)
    - [1. Iterative Binary Search:](#1-iterative-binary-search)
    - [2. Recursive Binary Search:](#2-recursive-binary-search)
    - [3. Binary Search with Bounds:](#3-binary-search-with-bounds)
    - [4. Binary Search with Custom Comparator:](#4-binary-search-with-custom-comparator)
    - [5. Generic Binary Search (Finding the First Occurrence):](#5-generic-binary-search-finding-the-first-occurrence)
    - [6. Generic Binary Search (Finding the Last Occurrence):](#6-generic-binary-search-finding-the-last-occurrence)
    - [7. Binary Search with Early Exit:](#7-binary-search-with-early-exit)
    - [8. Binary Search on Rotated Sorted Array:](#8-binary-search-on-rotated-sorted-array)
    - [9. Binary Search with Duplicates (Find Any Occurrence):](#9-binary-search-with-duplicates-find-any-occurrence)
  - [10. Binary Search with Lower and Upper Bound:](#10-binary-search-with-lower-and-upper-bound)

### 1. Iterative Binary Search:

- **Pros**: Simple, efficient, and doesn't require extra memory.
- **Cons**: Not recursive, which may be less intuitive for some.

```python
def iterative_binary_search(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return -1
```

<br><br>

### 2. Recursive Binary Search:

- **Pros**: Elegant and often easier to understand.
- **Cons**: May use more memory due to the recursive call stack.

```python
def recursive_binary_search(arr, target, low, high):
    if low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            return recursive_binary_search(arr, target, mid + 1, high)
        else:
            return recursive_binary_search(arr, target, low, mid - 1)
    else:
        return -1
```
<br><br>

### 3. Binary Search with Bounds:

- **Use Case**: You want to search within a specific range of values in a sorted list.
- **Example**:In a database application, finding all records within a certain date range or price range efficiently.

```python
def binary_search_with_bounds(arr, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            start = mid + 1
        else:
            end = mid - 1
    
    return -1
```

```python
def binary_search_with_bounds(arr, target, left_bound, right_bound):
    lower_bound = -1  # Initialize lower bound to -1 (target not found yet)
    upper_bound = -1  # Initialize upper bound to -1 (target not found yet)
    
    left, right = left_bound, right_bound
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            lower_bound = mid if lower_bound == -1 else min(lower_bound, mid)
            upper_bound = mid if upper_bound == -1 else max(upper_bound, mid)
            
            left = mid + 1
            right = mid - 1
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return lower_bound, upper_bound
```

<br><br>

### 4. Binary Search with Custom Comparator:

**Use Case**:Perform binary search in a list of custom objects where the comparison is not based on the default comparison.
- **Example**:Searching for a specific book title in a list of books based on a custom comparison function that considers author names or publication years.


```python
def binary_search_with_custom_comparator(arr, target, comparator):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        compare_result = comparator(arr[mid], target)
        
        if compare_result == 0:
            return mid
        elif compare_result < 0:
            low = mid + 1
        else:
            high = mid - 1
    
    return -1

```

<br><br>

### 5. Generic Binary Search (Finding the First Occurrence):

- **Use Case**: Find the index of the first occurrence of a specific element in a sorted list.
- **Example**: Finding the index of the first occurrence of a specific word in a sorted dictionary or the first occurrence of a specific date in a sorted log file.

```python
def binary_search_first_occurrence(arr, target):
    low, high, result = 0, len(arr) - 1, -1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            result = mid
            high = mid - 1  # Continue searching to the left for the first occurrence
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return result
```
<br><br>


### 6. Generic Binary Search (Finding the Last Occurrence):

- **Use Case**: Find the index of the last occurrence of a specific element in a sorted list.
- **Example**: Finding the index of the last occurrence of a particular error code in a sorted log file.

```python
def binary_search_last_occurrence(arr, target):
    low, high, result = 0, len(arr) - 1, -1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            result = mid
            low = mid + 1  # Continue searching to the right for the last occurrence
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return result
```
<br><br>


### 7. Binary Search with Early Exit:

- **Use Case**: Searching for a specific value in a large, sorted dataset where you only need to know if it exists, but you don't need all occurrences.
- **Example**: In a list of stock prices over time, you want to find the first instance where the price exceeds a certain threshold.


```python
def binary_search_with_early_exit(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid  # Exit early when the element is found
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return -1
```
<br><br>


### 8. Binary Search on Rotated Sorted Array:

- **Use Case**: Search in a rotated sorted array, such as when finding an element in a circularly sorted list.
- **Example**: Searching for a value in a rotated list of dates to find the date closest to a given date.


```python
def search_in_rotated_sorted_array(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] >= arr[low]:  # Left half is sorted
            if arr[low] <= target < arr[mid]:
                high = mid - 1
            else:
                low = mid + 1
        else:  # Right half is sorted
            if arr[mid] < target <= arr[high]:
                low = mid + 1
            else:
                high = mid - 1
    
    return -1
```
<br><br>


### 9. Binary Search with Duplicates (Find Any Occurrence):

- **Use Case**: Finding the index of any occurrence of a specific value in a sorted list.
- **Example**: In an e-commerce website, determining if a product with a certain ID exists in a sorted list of product IDs.


```python
def binary_search_any_occurrence(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return -1
```
<br><br>

## 10. Binary Search with Lower and Upper Bound:

- **Pros**: Can be used to find the range of indices where a value lies in a sorted list.
- **Cons**: Requires additional code for finding the lower and upper bounds.


```python
def binary_search_lower_bound(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    
    return low

def binary_search_upper_bound(arr, target):
    low, high = 0, len(arr) - 1
    
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] <= target:
            low = mid + 1
        else:
            high = mid - 1
    
    return high