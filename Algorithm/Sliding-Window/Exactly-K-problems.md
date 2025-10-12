# Exactly-K Sliding Window Problems

## 1. Basic Concept
Exactly-K problems require the window to satisfy an exact condition (e.g., exactly K distinct elements, exactly K odd numbers). The key insight is converting "exactly K" into the difference between "at most K" and "at most K-1".

## 2. Core Mathematical Insight
exactly(k)=at_most(k)-at_most(k-1)

This transformation allows us to use standard sliding window techniques for "at most" problems and derive the "exactly" count.

## 3. Generic Template

### Main Function:
```python
def exactly_k(nums, k):
    return at_most_k(nums, k) - at_most_k(nums, k - 1)

At Most K Helper:
def at_most_k(nums, k):
    count = {}
    left = 0
    result = 0
    
    for right in range(len(nums)):
        # Expand window
        if nums[right] not in count or count[nums[right]] == 0:
            k -= 1
        count[nums[right]] = count.get(nums[right], 0) + 1
        
        # Shrink window if needed
        while k < 0:
            count[nums[left]] -= 1
            if count[nums[left]] == 0:
                k += 1
            left += 1
        
        # Count valid subarrays ending at right
        result += right - left + 1
    
    return result

4. Example 1: LeetCode 992- Subarrays with K different Integers
Problem Description:
Count the numbers of subbarrays with exactly K distinct integers.

Solution:
def subarrays_with_k_distinct(nums, k):
    def at_most_k_distinct(k):
        count = {}
        left = 0
        result = 0
        
        for right in range(len(nums)):
            # Add right element
            if nums[right] not in count or count[nums[right]] == 0:
                k -= 1
            count[nums[right]] = count.get(nums[right], 0) + 1
            
            # Shrink window if too many distinct elements
            while k < 0:
                count[nums[left]] -= 1
                if count[nums[left]] == 0:
                    k += 1
                left += 1
            
            # Count subarrays ending at right
            result += right - left + 1
        
        return result
    
    return at_most_k_distinct(k) - at_most_k_distinct(k - 1)
Time complexity:O(N) Space complexity:O(K)

5. Example 2: Subarrays with Exactly K odd Numbers
Problem variation:
Count subarrays with exactly K odd numbers
Solution:
def subarrays_with_k_odd(nums, k):
    def at_most_k_odd(k):
        left = 0
        odd_count = 0
        result = 0
        
        for right in range(len(nums)):
            # Count odd numbers
            if nums[right] % 2 == 1:
                odd_count += 1
            
            # Shrink window if too many odds
            while odd_count > k:
                if nums[left] % 2 == 1:
                    odd_count -= 1
                left += 1
            
            # Count valid subarrays
            result += right - left + 1
        
        return result
    
    return at_most_k_odd(k) - at_most_k_odd(k - 1)

6.Example 3: Binary subarrays with Exactly K ones
- LeetCode 1248 - Count Number of Nice subarrays
Solution:
def number_of_subarrays(nums, k):
    def at_most_k(k):
        left = 0
        odd_count = 0
        result = 0
        
        for right in range(len(nums)):
            if nums[right] % 2 == 1:
                odd_count += 1
            
            while odd_count > k:
                if nums[left] % 2 == 1:
                    odd_count -= 1
                left += 1
            
            result += right - left + 1
        
        return result

7. Advanced patterns: Exactly K with Additional Constraints
Mutiple conditions:
def exactly_k_with_conditions(nums, k, min_val, max_val):
    def at_most_k_with_conditions(k):
        # Implement sliding window with multiple constraints
        left = 0
        count = 0  # Track condition satisfaction
        result = 0
        
        for right in range(len(nums)):
            # Update condition tracking
            if satisfies_condition(nums[right], min_val, max_val):
                count += 1
            
            # Shrink window
            while count > k:
                if satisfies_condition(nums[left], min_val, max_val):
                    count -= 1
                left += 1
            
            result += right - left + 1
        
        return result
    
    return at_most_k_with_conditions(k) - at_most_k_with_conditions(k - 1)
8. Common Exactly-K Problem Types

Distinct Elements:

· 992. Subarrays with K Different Integers
· Substrings with exactly K unique characters

Numerical Conditions:

· 1248. Count Number of Nice Subarrays (exactly K odds)
· Subarrays with exactly K ones (binary arrays)
· Subarrays with sum exactly K (using prefix sums)

Character Frequency:

· Substrings with exactly K occurrences of a character
· Subarrays with frequency exactly K for specific elements

9. Optimization Techniques

1. Early Termination: Return 0 if k > total possible distinct elements
2. Boundary Handling: Handle k = 0 and k = 1 cases separately if needed
3. Space Optimization: Use arrays instead of hash maps for limited value ranges
4. Two-Pass vs One-Pass: Consider computing both at_most values in one pass

10.Edge Cases
  - k==0:
  if k == 0:
    return 0  # Or handle according to problem

  - k> maximum possible
  max_distinct = len(set(nums))
  if k > max_distinct:
    return 0

  - Empty array:
  if not nums:
    return 0

11. Complexity Analysis

· Time Complexity: O(2N) = O(N) - two passes for at_most calculations
· Space Complexity: O(K) - for storing counts of distinct elements
· Window Operations: Each element enters and leaves the window at most twice

12. When to Use Exactly-K Pattern

· Problem asks for "exactly K" of something
· "At most K" is easier to implement with sliding window
· Counting problems where direct exactly-K counting is complex
· Subarray/substring enumeration with precise constraints
    
return at_most_k(k) - at_most_k(k - 1)
