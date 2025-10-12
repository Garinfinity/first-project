# Counting Sliding Window

## 1. Basic Concept
Counting window specializes in problems that require tracking frequencies, counts, or distributions of elements within the window. It often uses hash maps or arrays to maintain character/element counts.

## 2. Characteristic Features
- **Frequency Tracking**: Uses dictionaries/arrays to count element occurrences
- **Condition Validation**: Window validity depends on count conditions
- **Efficient Updates**: Increment/decrement counts in O(1) time

## 3. Core Algorithm Template

### Using Hash Map:
```python
def counting_window(s):
    left = 0
    count = {}
    result = 0
    
    for right in range(len(s)):
        # Add right character to count
        count[s[right]] = count.get(s[right], 0) + 1
        
        # Check and maintain window validity
        while not is_valid(count):  # Define validation condition
            count[s[left]] -= 1
            if count[s[left]] == 0:
                del count[s[left]]
            left += 1
        
        # Process valid window
        result = update_result(result, left, right)
    
    return result

Using Fixed Array(for lowercase letters):
def counting_window_array(s):
    left = 0
    count = [0] * 26  # For 26 lowercase letters
    result = 0
    
    for right in range(len(s)):
        # Add right character
        count[ord(s[right]) - ord('a')] += 1
        
        # Maintain window validity
        while not is_valid_array(count):
            count[ord(s[left]) - ord('a')] -= 1
            left += 1
        
        # Update result
        result = max(result, right - left + 1)
    
    return result

4. Example 1: Character Frequency problems
- Leetcode 424 Longest Repeating Character Replacement
def character_replacement(s, k):
    count = {}
    left = 0
    max_len = 0
    max_freq = 0
    
    for right in range(len(s)):
        count[s[right]] = count.get(s[right], 0) + 1
        max_freq = max(max_freq, count[s[right]])
        
        # Window is invalid if (window_size - max_freq) > k
        while (right - left + 1) - max_freq > k:
            count[s[left]] -= 1
            left += 1
        
        max_len = max(max_len, right - left + 1)
    
    return max_len
Time Complexity: O(n)
Space Complexity: O(26) could be consider as O(1)

5. Example 2: Distinct Character Counting
- LeetCode 1358- Number of substrings containing all three characters
def number_of_substrings(s):
    count = {'a': 0, 'b': 0, 'c': 0}
    left = 0
    result = 0
    
    for right in range(len(s)):
        count[s[right]] += 1
        
        # Shrink while all three characters are present
        while all(count.values()):
            result += len(s) - right  # All substrings ending at right
            count[s[left]] -= 1
            left += 1
    
    return result

6.Example 3: Frequency-Based Validation
def find_anagrams(s, p):
    if len(s) < len(p):
        return []
    
    p_count = [0] * 26
    s_count = [0] * 26
    result = []
    
    # Initialize pattern counts
    for char in p:
        p_count[ord(char) - ord('a')] += 1
    
    # Sliding window
    for i in range(len(s)):
        # Add right character
        s_count[ord(s[i]) - ord('a')] += 1
        
        # Remove left character if window exceeds pattern length
        if i >= len(p):
            s_count[ord(s[i - len(p)]) - ord('a')] -= 1
        
        # Check if current window is an anagram
        if i >= len(p) - 1 and s_count == p_count:
            result.append(i - len(p) + 1)
    
    return result

7. Advanded Counting patterns
&7.1 Mutiple Constraint Counting
def complex_counting_window(s, k):
    char_count = [0] * 26
    vowel_count = 0
    left = 0
    result = 0
    
    for right in range(len(s)):
        # Update counts
        idx = ord(s[right]) - ord('a')
        char_count[idx] += 1
        if s[right] in 'aeiou':
            vowel_count += 1
        
        # Maintain multiple constraints
        while vowel_count > k or max(char_count) > 2:
            left_idx = ord(s[left]) - ord('a')
            char_count[left_idx] -= 1
            if s[left] in 'aeiou':
                vowel_count -= 1
            left += 1
        
        result = max(result, right - left + 1)
    
    return result

&7.2 Rolling Frequency Comparison
def compare_frequency_window(s1, s2):
    # Compare frequency distributions in sliding windows
    pass

8. Common Problem Types

Frequency Validation:

· 424. Longest Repeating Character Replacement
· 567. Permutation in String
· 438. Find All Anagrams in a String

Distinct Element Counting:

· 1358. Number of Substrings Containing All Three Characters
· 1248. Count Number of Nice Subarrays

Multi-Constraint Counting:

· Problems with multiple frequency conditions
· Combined character and numeric constraints

9. Optimization Tips

1. Use Arrays over Hash Maps when character set is small (e.g., lowercase letters)
2. Track Maximum Frequency efficiently without scanning entire count array
3. Early Termination when window cannot possibly satisfy conditions
4. Batch Processing for multiple constraint checks

10. Time & Space Complexity

· Time: Typically O(N) - each element processed once
· Space: O(K) where K is character set size (usually O(1) for fixed sets)
