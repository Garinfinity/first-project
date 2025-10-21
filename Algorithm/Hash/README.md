# Hash Map / Hash Set Algorithms

## 📋 Table of Contents
- [Lookup & Existence](./Lookup-Existence.md)
- [Counting & Frequency](./Counting-Frequency.md)
- [String Hash Mapping](./String-Mapping.md)
- [Mapping Relations](./Mapping-Relations.md)

## 🔹 Background
A hash table (or hash map / hash set) stores data in key-value pairs and allows O(1) average-time access for insertion, deletion, and search.

It uses a hash function to map each key to an index in an array. Hash-based structures are powerful because they can quickly handle tasks such as frequency counting, removing duplicates, checking existence, and verifying patterns.

## 🎯 Common Use Cases
- **Lookups**: Checking if an element exists in a set or dictionary
- **Counting**: Tracking frequency of elements (e.g., counting words)  
- **Mapping**: Storing associations like ID-Name or Key-Value pairs
- **Deduplication**: Removing duplicate elements from collections

## 📊 Summary Table
| Category | Structure | Key Concept | Typical Problems |
|----------|-----------|-------------|------------------|
| Lookup / Existence | HashSet | Existence, duplicates | 217, 349, 1 |
| Counting / Frequency | HashMap | Count, frequency, top K | 169, 242, 347 |
| String Mapping | HashMap | Character frequency / index | 387, 3 |
| Mapping Relation | HashMap | One-to-one pattern match | 205, 290 |
