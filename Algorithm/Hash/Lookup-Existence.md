1️⃣ Lookup / Existence

Key idea:
To determine whether an element (character, number, or symbol) exists, or whether two elements form a pair or duplicate.
Typically, a hash set is used to store elements that have already appeared.
Each lookup runs in O(1) average time.

🧩 Example 1 – Contains Duplicate

(LeetCode 217)

Given an integer array nums, return true if any value appears at least twice in the array, and false if every element is distinct.

Code:

def containsDuplicate(nums):
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False


⏱ Time: O(N) 💾 Space: O(N)

🧩 Example 2 – Intersection of Two Arrays

(LeetCode 349)

Given two integer arrays nums1 and nums2, return their intersection.
Each element in the result must be unique.

Code:

def intersection(nums1, nums2):
    s1 = set(nums1)
    s2 = set(nums2)
    return list(s1 & s2)


⏱ Time: O(M + N) 💾 Space: O(M + N)

🧩 Example 3 – Two Sum

(LeetCode 1)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

Code:

def two_sum(nums, target):
    mapp = {}
    for i, n in enumerate(nums):
        complement = target - n
        if complement in mapp:
            return [mapp[complement], i]
        mapp[n] = i


⏱ Time: O(N) 💾 Space: O(N)

🔸 Other LeetCode problems

219.Contains Duplicate II

128.Longest Consecutive Sequence

202.Happy Number
