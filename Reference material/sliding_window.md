When to Apply the Sliding Window Technique
What types of data can the sliding window technique be applied to?

Contiguous Stream of Data
When determining whether the sliding window technique is an appropriate approach for a given problem, the first thing we want to consider is what type of data we will be looking at. Our input should be a contiguous, linear, and iterable set of data stored such that we can create a window over it.

For example, we could perform the sliding window technique on an array, because we can create a window variable that holds some subset of the data using list slicing.

Contiguous Subset
In order for the sliding window technique to be applicable, the problem must also ask us to find a contiguous subset of the problem.

For example, say you are given an array of integers and asked to find all adjacent pairs of integers in the list that add up to a given sum. This could be solved using the sliding window technique. Our window would be of size two and we can check each adjacent pair by starting the left end of the window at index 0 and shifting our window by one each iteration until the right end of the window is at the last index in the array.


Minimum Sum Subarray of Size K
Consider the following problem:

Given an array of integers numbers and an integer k, return the sum of the minimum sum subarray of size k.

In other words, given the array of integers numbers, calculate the minimum sum of k consecutive elements in the array.

Here are some example inputs

Example 1 Input: numbers = [-1, 5, 3, 1, -3, 2] k = 2 Output: -2

the minimum sum subarray would be [1, -3]
Example 2 Input: numbers = [1, 2, 3, 4, 5] k = 3 Output: 6

the minimum sum subarray would be [1, 2, 3]
Input: numbers = [1,2,3] k = 4 Output: ValueError

the subarray must be shorter than the length of the original array
def min_sum(numbers, k):

    #find the length of the given array
    nums_len = len(numbers)

    # if the subarray is longer than the original array, raise an error
    if nums_len < k:
        raise ValueError("k must be an integer between 1 and len(numbers)")

    # get the sum of the first window
    window_sum = sum(numbers[:k])
    
    # initialize the minimum overall sum to the sum of the first window
    min_sum = window_sum

    # our for loop will be the start index of each window
    # our last window will start at nums_len - k
    for i in range(nums_len - k):
        # to shift the window, subtract the value at the window's current starting index from its sum
        window_sum -= numbers[i] 
        # shift the window to the right by adding the value at the k + ith index to replace the value just removed
        window_sum += numbers[k + i]
        # set the overall minimum subarray sum to either the sum of the new window
        # or the minimum subarray sum calculated so far, whichever is smaller
        min_sum = min(min_sum, window_sum)
    
    # return the minimum sum
    return min_sum




Given an array of integers and a number k, find the maximum sum of a subarray of size k. 

Examples: 

Input  : arr[] = {100, 200, 300, 400},  k = 2
Output : 700

Input  : arr[] = {1, 4, 2, 10, 23, 3, 1, 0, 20}, k = 4 
Output : 39
Explanation: We get maximum sum by adding subarray {4, 2, 10, 23} of size 4.

Input  : arr[] = {2, 3}, k = 3
Output : Invalid
Explanation: There is no subarray of size 3 as size of whole array is 2. 



Find zeroes to be flipped so that number of consecutive 1’s is maximized
Read
Discuss(70)
Courses
Practice
Given a binary array and an integer m, find the position of zeroes flipping which creates maximum number of consecutive 1’s in array.

Examples : 

Input:   arr[] = {1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1}
         m = 2
Output:  5 7
We are allowed to flip maximum 2 zeroes. If we flip
arr[5] and arr[7], we get 8 consecutive 1's which is
maximum possible under given constraints 

Input:   arr[] = {1, 0, 0, 1, 1, 0, 1, 0, 1, 1, 1}
         m = 1
Output:  7
We are allowed to flip maximum 1 zero. If we flip 
arr[7], we get 5 consecutive 1's which is maximum 
possible under given constraints.

Input:   arr[] = {0, 0, 0, 1}
         m = 4
Output:  0 1 2
Since m is more than number of zeroes, we can flip
all zeroes.


76. Minimum Window Substring
Hard
16.6K
680
Companies
Given two strings s and t of lengths m and n respectively, return the minimum window 
substring
 of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".

The testcases will be generated such that the answer is unique.

 

Example 1:

Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
Example 2:

Input: s = "a", t = "a"
Output: "a"
Explanation: The entire string s is the minimum window.
Example 3:

Input: s = "a", t = "aa"
Output: ""
Explanation: Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
 

Constraints:

m == s.length
n == t.length
1 <= m, n <= 105
s and t consist of uppercase and lowercase English letters.
 

Follow up: Could you find an algorithm that runs in O(m + n) time?



https://learn-2.galvanize.com/cohorts/3646/blocks/1277/content_files/01-algorithms/05-sliding-window.md