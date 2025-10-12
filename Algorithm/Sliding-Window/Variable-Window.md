# Variable-Size Sliding Window

## 1. Basic Concept
The window size can expand or shrink dynamically, usually under constraints like "at most..." or "no more than...".

## 2. Main Application Scenarios
- Find the longest/shortest subarray
- Find the longest/shortest substring  
- Count the number of subarrays or substrings satisfying certain conditions

## 3. Core Algorithm Template

### Basic Template:
```python
def variable_window(s, k):
    left = 0
    count = {}  # or use a variable to track condition
    max_len = 0
    
    for right in range(len(s)):
        # Expand window: add right character
        count[s[right]] = count.get(s[right], 0) + 1
        
        # Shrink window until condition is satisfied
        while condition_violated(count, k):  # Define your condition
            count[s[left]] -= 1
            if count[s[left]] == 0:
                del count[s[left]]
            left += 1
            
        # Update result
        max_len = max(max_len, right - left + 1)
    
    return max_len


4. Example 1: LeetCode 1004 - Max Consecutive Ones III

Problem Description
Given a binary array, flip at most k 0's to 1's. Find the longest contiguous subarray of 1's.

Solution 1: Using Variable Tracking
def longest_ones(nums, k):
    zero_count = 0
    left = 0
    max_len = 0
    
    for right in range(len(nums)):
        if nums[right] == 0:
            zero_count += 1
            
        while zero_count > k:
            if nums[left] == 0:
                zero_count -= 1
            left += 1
            
        max_len = max(max_len, right - left + 1)
    
    return max_len

Time Complexity: O(N)
Space Complexity: O(1)

Solution 2: Using Hash Map
from collections import defaultdict

def longest_ones(nums, k):
    count = defaultdict(int)
    left = 0
    max_len = 0
    
    for right in range(len(nums)):
        count[nums[right]] += 1
        
        while count[0] > k:
            count[nums[left]] -= 1
            left += 1
            
        max_len = max(max_len, right - left + 1)
    
    return max_len

5. Example 2: Subarray Counting Problems

Problem Pattern:
Count the number of subarrays satisfying a condition.

Key Insight:
If [left, right] is valid, then all [left+1, right], [left+2, right], ..., [right, right] are also valid.

Example: Count Subarrays with Product Less Than K
def num_subarray_product_less_than_k(nums, k):
    if k <= 1:
        return 0
        
    ans = 0
    left = 0
    product = 1
    
    for right in range(len(nums)):
        product *= nums[right]
        
        while product >= k:
            product //= nums[left]
            left += 1
            
        ans += right - left + 1
    
    return ans

6. Common Problem Types

6.1 Longest Subarray/Substring

· 3. Longest Substring Without Repeating Characters
· 209. Minimum Size Subarray Sum
· 424. Longest Repeating Character Replacement
· 159. Longest Substring with At Most Two Distinct Characters
· 340. Longest Substring with At Most K Distinct Characters

6.2 Subarray Counting

· Count subarrays with sum/product constraints
· Count substrings with character frequency limits

7. When to Use Variable-Size Window

· Problem asks for "longest" or "shortest" subarray/substring
· Constraints involve "at most" or "no more than"
· Need to find optimal sub-interval under conditions
· Counting valid subarrays with sliding properties


