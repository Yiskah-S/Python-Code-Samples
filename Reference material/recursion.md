# Table of Contents

- [Table of Contents](#table-of-contents)
    - [Components of a Recursive Function](#components-of-a-recursive-function)
- [Recursive Function Components](#recursive-function-components)
  - [Overview](#overview)
  - [Key Components](#key-components)
  - [Examples of Recursive Functions](#examples-of-recursive-functions)
    - [Hello Repeat Recursive](#hello-repeat-recursive)
    - [Modified Hello Repeat Recursive](#modified-hello-repeat-recursive)
    - [Factorial Calculation](#factorial-calculation)
    - [Fibonacci Sequence](#fibonacci-sequence)
    - [Sum of Numbers](#sum-of-numbers)
    - [Binary Search](#binary-search)
    - [Tower of Hanoi](#tower-of-hanoi)
    - [Palindrome Check](#palindrome-check)
    - [Power Calculation](#power-calculation)
    - [Linked List Operations](#linked-list-operations)
    - [Tree Traversal (in order)](#tree-traversal-in-order)
    - [Maze Solving](#maze-solving)
    - [Tic-Tac-Toe Game](#tic-tac-toe-game)
    - [Ackermann Function](#ackermann-function)
    - [Merge Sort](#merge-sort)
    - [Quick Sort](#quick-sort)
    - [Parentheses Matching](#parentheses-matching)
    - [Counting Occurrences](#counting-occurrences)
    - [Sum of Digits](#sum-of-digits)
    - [Print All Subsets](#print-all-subsets)
    - [Calculate GCD (Greatest Common Divisor)](#calculate-gcd-greatest-common-divisor)
    - [Reverse a String](#reverse-a-string)
    - [Fibonacci with Memoization](#fibonacci-with-memoization)
    - [Pascal's Triangle](#pascals-triangle)
    - [Counting Elements in a List](#counting-elements-in-a-list)
    - [Print Numbers in Reverse](#print-numbers-in-reverse)
    - [File System Search](#file-system-search)
    - [Linked List Operations](#linked-list-operations-1)
    - [Tree Traversal (In-order)](#tree-traversal-in-order-1)
    - [Permutations and Combinations](#permutations-and-combinations)
    - [Print Patterns](#print-patterns)

### Components of a Recursive Function
A recursive function should always have two basic components. The first is the base case which is our end condition. In other words, the base case is the condition under which we want to stop making recursive calls. Often the base case is the smallest subproblem of the overall problem we are working to solve.

The second component in a recursive function is the recursive case. The code we execute in the recursive case will run for all subproblems (including the overall problem) that do not match the base case. 

```Python
def hello_repeat_recursive(num):
    print(f"Hello {num}!")
    if num == 1:
        return
    else:
        hello_repeat_recursive(num - 1)
```

Input: 5 
Output:  
"Hello 5!"  
"Hello 4!"  
"Hello 3!"  
"Hello 2!"  
"Hello 1!"

```Python
def hello_repeat_recursive(num):
    if num == 0:
        return
    else:
        hello_repeat_recursive(num - 1)
        print(f"Hello {num}!")
```

Input: 5  
Output:  
"Hello 1!"  
"Hello 2!"  
"Hello 3!"  
"Hello 4!"  
"Hello 5!"   


# Recursive Function Components

## Overview
Recursive functions are fundamental in programming, particularly for solving problems that can be broken down into smaller, similar subproblems. These functions are defined in terms of themselves and are highly effective in various scenarios, including mathematical computations, algorithmic problem-solving, and data structure manipulations.

## Key Components
A recursive function typically comprises two essential components:

1. **Base Case**: This is the terminating condition. It defines the scenario under which the recursive calls should cease, thus preventing infinite recursion. It often represents the smallest subproblem or an edge case.

2. **Recursive Case**: This part of the function handles the general case. It includes the logic for breaking down the problem into smaller instances and making recursive calls. These calls eventually lead to the base case.

## Examples of Recursive Functions

### Hello Repeat Recursive
```python
def hello_repeat_recursive(num):
    print(f"Hello {num}!")
    if num == 1:
        return
    else:
        hello_repeat_recursive(num - 1)
```
Input: 5 
Output:  
"Hello 5!"  
"Hello 4!"  
"Hello 3!"  
"Hello 2!"  
"Hello 1!"

### Modified Hello Repeat Recursive
```python
def hello_repeat_recursive(num):
    if num == 0:
        return
    else:
        hello_repeat_recursive(num - 1)
        print(f"Hello {num}!")
```
Input: 5  
Output:  
"Hello 1!"  
"Hello 2!"  
"Hello 3!"  
"Hello 4!"  
"Hello 5!"  

### Factorial Calculation

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)
```

### Fibonacci Sequence

```python
def fibonacci(n):
    if n <= 1:
        return n
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
```

### Sum of Numbers

```python
def sum_of_numbers(n):
    if n == 1:
        return 1
    else:
        return n + sum_of_numbers(n - 1)
```

### Binary Search

```python
def binary_search(arr, target, left, right):
    if left <= right:
        mid = left + (right - left) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            return binary_search(arr, target, mid + 1, right)
        else:
            return binary_search(arr, target, left, mid - 1)
    else:
        return -1
```

### Tower of Hanoi

```python
def tower_of_hanoi(n, source, auxiliary, target):
    if n == 1:
        print(f"Move disk 1 from {source} to {target}")
        return
    tower_of_hanoi(n - 1, source, target, auxiliary)
    print(f"Move disk {n} from {source} to {target}")
    tower_of_hanoi(n - 1, auxiliary, source, target)
```

### Palindrome Check

```python
def is_palindrome(s):
    s = s.lower()
    s = ''.join(filter(str.isalnum, s))
    if len(s) <= 1:
        return True
    elif s[0] == s[-1]:
        return is_palindrome(s[1:-1])
    else:
        return False
```

### Power Calculation

```python
def power(x, n):
    if n == 0:
        return 1
    else:
        return x * power(x, n - 1)
```

### Linked List Operations

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def print_linked_list(head):
    if head is None:
        return
    print(head.val)
    print_linked_list(head.next)

def reverse_linked_list(head):
    if head is None or head.next is None:
        return head
    new_head = reverse_linked_list(head.next)
    head.next.next = head
    head.next = None
    return new_head
```

### Tree Traversal (in order)

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def in_order_traversal(root):
    if root:
        in_order_traversal(root.left)
        print(root.val)
        in_order_traversal(root.right)
```

### Maze Solving

```Python
def solve_maze(maze, start, end):
    if start == end:
        return [end]
    x, y = start
    if maze[x][y] == 1:
        return None
    if x < len(maze) - 1 and solve_maze(maze, (x + 1, y), end):
        return [(x, y)] + solve_maze(maze, (x + 1, y), end)
    if y < len(maze[0]) - 1 and solve_maze(maze, (x, y + 1), end):
        return [(x, y)] + solve_maze(maze, (x, y + 1), end)
    return None
```

### Tic-Tac-Toe Game

```Python
def check_win(board, player):
    for row in board:
        if all(cell == player for cell in row):
            return True
    for col in range(len(board[0])):
        if all(board[row][col] == player for row in range(len(board))):
            return True
    if all(board[i][i] == player for i in range(len(board))) or all(board[i][len(board) - i - 1] == player for i in range(len(board))):
        return True
    return False
```

### Ackermann Function

```Python
def ackermann(m, n):
    if m == 0:
        return n + 1
    elif m > 0 and n == 0:
        return ackermann(m - 1, 1)
    else:
        return ackermann(m - 1, ackermann(m, n - 1))
```

### Merge Sort

```Python
def merge_sort(arr):
    if len(arr) > 1:
        mid = len(arr) // 2
        left_half = arr[:mid]
        right_half = arr[mid:]

        merge_sort(left_half)
        merge_sort(right_half)

        i = j = k = 0

        while i < len(left_half) and j < len(right_half):
            if left_half[i] < right_half[j]:
                arr[k] = left_half[i]
                i += 1
            else:
                arr[k] = right_half[j]
                j += 1
            k += 1

        while i < len(left_half):
            arr[k] = left_half[i]
            i += 1
            k += 1

        while j < len(right_half):
            arr[k] = right_half[j]
            j += 1
            k += 1
```

### Quick Sort

```Python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + middle + quick_sort(right)
```

### Parentheses Matching

```Python
def is_balanced_parentheses(s):
    def is_balanced(s, stack):
        if not s:
            return not stack
        if s[0] == "(":
            stack.append("(")
        elif s[0] == ")":
            if not stack:
                return False
            stack.pop()
        return is_balanced(s[1:], stack)

    return is_balanced(s, [])
```

### Counting Occurrences

```Python
def count_occurrences(arr, target):
    if not arr:
        return 0
    if arr[0] == target:
        return 1 + count_occurrences(arr[1:], target)
    else:
        return count_occurrences(arr[1:], target)
```

### Sum of Digits

```Python
def sum_of_digits(n):
    if n < 10:
        return n
    else:
        return n % 10 + sum_of_digits(n // 10)
```

### Print All Subsets

```Python
def generate_subsets(nums):
    def backtrack(start, subset):
        result.append(subset[:])
        for i in range(start, len(nums)):
            subset.append(nums[i])
            backtrack(i + 1, subset)
            subset.pop()

    result = []
    backtrack(0, [])
    return result
```

### Calculate GCD (Greatest Common Divisor)

```Python
def gcd(a, b):
    if b == 0:
        return a
    else:
        return gcd(b, a % b)
```

### Reverse a String

```Python
def reverse_string(s):
    if len(s) == 0:
        return s
    else:
        return reverse_string(s[1:]) + s[0]
```

### Fibonacci with Memoization

```Python
def fibonacci_memoization(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_memoization(n - 1, memo) + fibonacci_memoization(n - 2, memo)
    return memo[n]
```

### Pascal's Triangle

```Python
def generate_pascals_triangle(n):
    if n == 0:
        return []
    elif n == 1:
        return [[1]]
    else:
        triangle = generate_pascals_triangle(n - 1)
        prev_row = triangle[-1]
        new_row = [1]
        for i in range(1, n - 1):
            new_row.append(prev_row[i - 1] + prev_row[i])
        new_row.append(1)
        triangle.append(new_row)
        return triangle
```

### Counting Elements in a List

Use Case: Counting the number of elements in a list.

```Python
def count_elements(lst):
    if not lst:
        return 0
    else:
        return 1 + count_elements(lst[1:])
```

### Print Numbers in Reverse

Use Case: Printing numbers from n to 1 in reverse order.

```Python
def print_reverse(n):
    if n >= 1:
        print(n)
        print_reverse(n - 1)
```

### File System Search

Use Case: Searching for a file or directory in a file system.

```Python
import os

def file_search(root, target):
    for item in os.listdir(root):
        if os.path.isdir(os.path.join(root, item)):
            file_search(os.path.join(root, item), target)
        elif item == target:
            print(f"Found: {os.path.join(root, item)}")
```

### Linked List Operations

Use Case: Traversing and manipulating linked lists.

```Python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def print_linked_list(head):
    if head is None:
        return
    print(head.val)
    print_linked_list(head.next)

def reverse_linked_list(head):
    if head is None or head.next is None:
        return head
    new_head = reverse_linked_list(head.next)
    head.next.next = head
    head.next = None
    return new_head
```

### Tree Traversal (In-order)

Use Case: Traversing binary trees.

```Python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def in_order_traversal(root):
    if root:
        in_order_traversal(root.left)
        print(root.val)
        in_order_traversal(root.right)
```

### Permutations and Combinations

Use Case: Generating permutations or combinations of elements.

```Python
def permutations(arr):
    if len(arr) == 0:
        return [[]]
    result = []
    for i in range(len(arr)):
        rest = arr[:i] + arr[i + 1:]
        for p in permutations(rest):
            result.append([arr[i]] + p)
    return result
```

### Print Patterns

Use Case: Printing patterns using recursion.

```Python
def print_triangle(n):
    if n == 0:
        return
    print("*" * n)
    print_triangle(n - 1)
```


https://learn-2.galvanize.com/cohorts/3646/blocks/1277/content_files/01-algorithms/03-recursion.md