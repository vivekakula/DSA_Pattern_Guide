# Pattern Overview - The Big Picture

## Why Patterns Matter
Instead of memorizing 1000 problems, learn 15 patterns. When you see a new problem, you'll think: "I've seen this pattern before!"

 The 15 Essential Patterns

 1. **Two Pointers** 👉👈
- **When**: Array/string problems, need to compare or find pairs
- **Clue**: "Find pair that sums to X", "Remove duplicates", "Palindrome"
- **Time Saved**: O(n²) → O(n)

 2. **Sliding Window** 🪟
- **When**: Contiguous subarray/substring problems
- **Clue**: "Maximum sum of subarray size k", "Longest substring with...", "Find all anagrams"
- **Time Saved**: O(n²) → O(n)

 3. **Fast & Slow Pointers** 🐇🐢
- **When**: Linked list cycle detection, finding middle
- **Clue**: "Detect cycle", "Find middle", "Happy number"
- **Time Saved**: O(n) space → O(1) space

 4. **Merge Intervals** 📊
- **When**: Overlapping ranges/intervals
- **Clue**: "Merge overlapping intervals", "Insert interval", "Meeting rooms"
- **Pattern**: Sort → Compare → Merge

 5. **Cyclic Sort** 🔄
- **When**: Array with numbers in range [1, n]
- **Clue**: "Find missing number", "Find duplicate", numbers in specific range
- **Time**: O(n) with O(1) space

 6. **In-place Reversal of LinkedList** ↩️
- **When**: Reverse parts of a linked list
- **Clue**: "Reverse linked list", "Reverse k-group"
- **Space**: O(n) → O(1)

 7. **BFS (Tree Level Order)** 🌳
- **When**: Tree/graph traversal level by level
- **Clue**: "Level order traversal", "Minimum depth", "Right side view"
- **Tool**: Queue

 8. **DFS (Tree Depth)** 🌲
- **When**: Explore all paths in tree/graph
- **Clue**: "All paths", "Path sum", "Diameter"
- **Tool**: Recursion or Stack

 9. **Binary Search** 🔍
- **When**: Sorted array or "search space" problems
- **Clue**: "Find in sorted array", "Search in rotated", "Find peak"
- **Time**: O(n) → O(log n)

 10. **Top K Elements** 🏆
- **When**: Find largest/smallest K elements
- **Clue**: "K largest", "K frequent", "K closest"
- **Tool**: Heap (Priority Queue)

 11. **K-way Merge** 🔀
- **When**: Multiple sorted arrays/lists
- **Clue**: "Merge K sorted lists", "Smallest range"
- **Tool**: Min Heap

 12. **Modified Binary Search** 🎯
- **When**: Binary search with a twist
- **Clue**: "Rotated array", "First/last occurrence", "Search in matrix"

 13. **Backtracking** ⬅️➡️
- **When**: Generate all combinations/permutations
- **Clue**: "All subsets", "Permutations", "N-Queens", "Generate parentheses"
- **Pattern**: Choose → Explore → Unchoose

 14. **Dynamic Programming** 💰
- **When**: Optimization problems with overlapping subproblems
- **Clue**: "Maximum/Minimum", "Count ways", "Longest/Shortest"
- **Types**: 0/1 Knapsack, Unbounded Knapsack, LCS, LIS, Palindrome

 15. **Greedy** 🤑
- **When**: Local optimal leads to global optimal
- **Clue**: "Minimum coins", "Jump game", "Meeting rooms"
- **Note**: Prove greedy works before using!

---

 Pattern Recognition Flowchart

```
Is it about arrays/strings?
├─ Need to find pairs/triplets? → TWO POINTERS
├─ Contiguous subarray/substring? → SLIDING WINDOW
└─ Numbers in range [1,n]? → CYCLIC SORT

Is it about linked lists?
├─ Detect cycle? → FAST & SLOW POINTERS
└─ Reverse part of it? → IN-PLACE REVERSAL

Is it about trees/graphs?
├─ Level by level? → BFS
├─ All paths? → DFS
└─ BST property? → DFS with constraints

Is it sorted or can be sorted?
├─ Search in sorted array? → BINARY SEARCH
└─ Merge sorted lists? → K-WAY MERGE

Is it about intervals/ranges? → MERGE INTERVALS

Need top K elements? → HEAP (TOP K ELEMENTS)

Generate all combinations? → BACKTRACKING

Optimization with subproblems? → DYNAMIC PROGRAMMING

Local optimal = global? → GREEDY
```

---

 Next Steps
1. Read pattern details: `02_two_pointers.md` through `16_greedy.md`
2. For each pattern, understand the template
3. Solve 2-3 problems per pattern
4. Use `pattern_cheatsheet.md` as quick reference

**Pro Tip**: Don't try to learn all at once. Master 2-3 patterns per day!
