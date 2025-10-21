Mapping Relation

Key idea:
Focus not on actual characters but on pattern structure — whether the relationship between characters is consistent.

For instance:

“aba” ↔ “tpt” → same pattern (0,1,0)

“aba” ↔ “ttt” → different pattern (0,1,0) vs (0,0,0)

We assign IDs to characters based on first appearance:

New char → assign new number

Repeated char → reuse old number

Code (Pattern Extraction):

def pattern(s):
    mapping = {}
    pattern_list = []
    next_id = 0
    for ch in s:
        if ch not in mapping:
            mapping[ch] = next_id
            next_id += 1
        pattern_list.append(mapping[ch])
    return pattern_list

print(pattern("aba"))  # [0,1,0]
print(pattern("tpt"))  # [0,1,0]

🔸 LeetCode problems

205.Isomorphic Strings

290.Word Pattern

🧰 Additional Note: Counter vs defaultdict
Feature	Counter	defaultdict(int)
Purpose	Counting frequencies	Flexible default values
Default value	Automatically 0 for new keys	Depends on provided function (e.g. int() → 0)
Import	from collections import Counter	from collections import defaultdict
Usage example	cnt = Counter(nums)	cnt = defaultdict(int); cnt[x]+=1
When to use	Simple counting	More flexible (custom initialization, grouping, etc.)


🧩 Summary Table
Category	Structure	Key Concept	Typical Problems
Lookup / Existence	HashSet	Existence, duplicates	217, 349, 1
Counting / Frequency	HashMap	Count, frequency, top K	169, 242, 347
String Mapping	HashMap	Character frequency / index	387, 3
Mapping Relation	HashMap	One-to-one pattern match	205, 290
