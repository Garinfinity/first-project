Counting / Frequency

Key idea:
Use a hash map to count how many times each element appears.
Then analyze the frequency, find maximum/minimum counts, or check relationships between frequencies.

🧩 Example – Majority Element

(LeetCode 169)

Return the element that appears more than ⌊n / 2⌋ times.

Code:

from collections import Counter

def majorityElement(nums):
    count = Counter(nums)
    return max(count, key=count.get)


⏱ Time: O(N) 💾 Space: O(N)

🧩 Example – Valid Anagram

(LeetCode 242)

Determine if two strings are anagrams of each other.

Code:

from collections import Counter

def isAnagram(s, t):
    return Counter(s) == Counter(t)

🔸 Other LeetCode problems

347.Top K Frequent Elements

451.Sort Characters by Frequency

383.Ransom Note

409.Longest Palindrome
