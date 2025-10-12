# Fixed-Size Sliding Window

## 1. Basic Concept
The window length is constant (k), suitable for problems involving subarrays of fixed length.

**Key Insight**: When a problem requires picking numbers from neither left nor right ends but maintaining a middle segment, consider fixed-size window.

## 2. Algorithm Thought Process

### Visual Representation:
Initial window:    [a,    b,    c]     (size = 3)
Add new element:   [a,    b,    c,    d]
Remove leftmost:          [b,    c,    d]    (maintain size = 3)


### Core Mechanism:
- Maintain a window of fixed size k
- Slide the window one element at a time
- Add new element on the right, remove oldest element on the left
- Update the result based on window content

## 3. Example: 643. Maximum Average Subarray I

### Problem Description
Given an array, find the maximum average value of any contiguous subarray of size k.

### Solution Approach
- Find the maximum sum of subarray with size k
- Convert to average by dividing by k
- No need for additional checks since k ≤ array length

### Code Implementation
```python
def max_average(nums, k):
    n = len(nums)
    max_sum = current_sum = sum(nums[:k])  # Initial window
    
    for i in range(k, n):
        # Add new element, remove leftmost element
        current_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, current_sum)
    
    return float(max_sum / k)
Time Complexity: O(n)
Space Complexity: O(1)

## 4. Template Code
def fixed_window_template(nums, k):
    # Initialize with first window
    current_value = calculate_initial_value(nums, k)
    result = current_value
    
    for i in range(k, len(nums)):
        # Remove element exiting the window
        current_value -= contribution_of(nums[i - k])
        # Add element entering the window  
        current_value += contribution_of(nums[i])
        # Update result
        result = update_result(result, current_value)
    
    return result

## 5. Related problems
Essential Practice:

· 643. Maximum Average Subarray I
· 1423. Maximum Points You Can Obtain from Cards
· 567. Permutation in String
· 1343. Number of Sub-arrays of Size K and Average ≥ Threshold

Advanced Applications:

1. Minimum/Maximum Average Subarray of Size K
2. Count Distinct Elements in Every Window of Size K
3. First Negative Number in Every Window of Size K
4. Maximum of All Subarrays of Size K
5. Number of Substrings of Size K with K Distinct Characters
6. Check If Any Subarray of Size K Meets Condition

## 6. When to Use Fixed-Size Window

 - Problem explicitly specifies subarray/substring length
 - Need to process all contiguous subarrays of size k
 - Statistical calculations over fixed intervals
 - Pattern matching with fixed window size


