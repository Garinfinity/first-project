String Hash Mapping

Idea:
Use a hash map to record character relationships, frequency, or index positions in a string.
This helps identify repeating characters, first unique characters, or character mappings.

🧩 Example – First Unique Character in a String

(LeetCode 387)

Find the first character that appears only once in a string.

Code:

from collections import Counter

def firstUniqChar(s):
    count = Counter(s)
    for i, ch in enumerate(s):
        if count[ch] == 1:
            return i
    return -1

🔸 Other LeetCode problems

3.Longest Substring Without Repeating Characters

205.Isomorphic Strings (also fits Mapping category)

290.Word Pattern
