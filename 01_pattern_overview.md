# Pattern Overview: The Big Picture

## Why Patterns Help
You do not need to memorize a separate solution for every problem. Many problems share the same useful idea. Recognizing that idea gives you a place to start, but you still need to check that it fits the problem's rules and edge cases.

## The 18 Patterns in This Guide

 1. **Two Pointers** 👉👈
- **When**: Array/string problems, need to compare or find pairs
- **Clue**: "Find pair that sums to X", "Remove duplicates", "Palindrome"
- **Typical benefit**: Avoids checking every pair when the pointer rule is valid

 2. **Sliding Window** 🪟
- **When**: Contiguous subarray/substring problems
- **Clue**: "Maximum sum of subarray size k", "Longest substring with...", "Find all anagrams"
- **Typical benefit**: Reuses work as a contiguous range changes

 3. **Fast & Slow Pointers** 🐇🐢
- **When**: Linked list cycle detection, finding middle
- **Clue**: "Detect cycle", "Find middle", "Happy number"
- **Typical benefit**: Often detects a cycle without storing visited nodes

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
- **Typical benefit**: Cuts a sorted or monotonic search range in half

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

 16. **Graphs** 🕸️
- **When**: Problems involving nodes and connections/relationships
- **Clue**: "Provinces", "Islands", "Course schedule", "Network", "Shortest path"
- **Sub-patterns**: BFS (shortest), DFS (cycle/paths), Topological Sort (ordering), Dijkstra (weighted shortest), Union-Find (connectivity)

 17. **Monotonic Stack** 📉
- **When**: Need next greater/smaller element, span, or area in a sequence
- **Clue**: "Next warmer day", "Next greater element", "Largest rectangle", "Trapping water"
- **Trick**: Stack stores indices; pop while order is broken

 18. **Trie (Prefix Tree)** 🔤
- **When**: Prefix-based dictionary/word problems
- **Clue**: "Autocomplete", "Starts with", "Word search in grid", "Dictionary"
- **Structure**: Tree where each path from root spells a word character by character

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

Nodes + connections/dependencies?
├─ Find shortest path (unweighted)? → BFS on Graph
├─ Ordering with prerequisites? → TOPOLOGICAL SORT
├─ Shortest path (weighted)? → DIJKSTRA
└─ Are two nodes connected? → UNION-FIND

Next greater/smaller element? → MONOTONIC STACK

Prefix/word dictionary problems? → TRIE
```

---

 🚨 Pattern Confusion Buster

These are the 4 pairs that almost every learner mixes up. Read this before your first LeetCode session.

---

 **1. Two Pointers vs Sliding Window**

| | Two Pointers | Sliding Window |
|---|---|---|
| Pointers move | Toward each other (or one chases other) | Same direction, window expands/shrinks |
| What you're doing | Comparing or matching specific elements | Tracking a property of a RANGE |
| Example | "Find pair that sums to X" | "Longest substring with K distinct chars" |

**Quick test**: Is your answer a single pair of elements, or a subarray/substring? → Pair = Two Pointers, Subarray = Sliding Window.

---

 **2. BFS vs DFS (Tree/Graph)**

| | BFS | DFS |
|---|---|---|
| Goal | Explore in order of distance | Follow a branch before exploring another |
| Tool | Queue | Recursion / Stack |
| Ask yourself | "What is the MINIMUM..." | "Find ALL..." or "Does ANY path exist..." |
| Example | Minimum depth of tree | All root-to-leaf paths |

**Quick test**: For an unweighted graph's shortest path, use BFS. For exploring branches or computing values recursively, DFS is a common choice. The required output and graph structure decide which fits.

---

 **3. Greedy vs Dynamic Programming**

| | Greedy | DP |
|---|---|---|
| Strategy | Make a choice and keep it | Compare choices while reusing smaller results |
| Speed | Fast: O(n) or O(n log n) | Slower: O(n²) typical |
| Risk | Wrong unless the choice is justified | Depends on defining the right state and recurrence |
| Example | Activity selection (sort by end time) | 0/1 Knapsack |

**Quick test**: A choice that looks best now is not enough to prove greedy is correct. If choices interact, consider DP and define what information each smaller problem needs.

---

 **4. Backtracking vs Dynamic Programming**

| | Backtracking | DP |
|---|---|---|
| Common use | Build and list valid candidates | Count ways or find a best value |
| Example | "Generate all subsets" | "Count the number of subsets with sum K" |
| Memory | Builds candidates and removes them | Fills a table |

**Quick test**: Listing actual solutions often calls for backtracking. Counting or optimizing may call for DP, but the constraints and repeated subproblems matter too.

---

 Next Steps
1. Read pattern details: `02_two_pointers.md` through `19_tries.md`
2. For each pattern, understand the template
3. Solve 2-3 problems per pattern
4. Use `pattern_cheatsheet.md` as quick reference

**Study tip**: Learn one pattern at a time. Move on when you can explain the idea and solve a fresh problem with it; revisit it later to check that you still remember it.

---

 🧠 Active Recall Self-Quiz

**How to use**: Read each problem below. Write your pattern guess on paper. Then check the answers. Do this BEFORE opening LeetCode — this is the single most effective learning habit.

> Trying to recall an idea before checking your notes can reveal what you understand and what needs another review.

| # | Problem Description | Your Answer |
|---|--------------------|--------------|
| 1 | Given a sorted array, find if two numbers sum to a target | ? |
| 2 | Find the longest substring without any repeating characters | ? |
| 3 | Detect if a linked list has a cycle | ? |
| 4 | Return the level-by-level values of a binary tree | ? |
| 5 | Find all possible subsets of an array | ? |
| 6 | Minimum cost to climb stairs (1 or 2 steps at a time) | ? |
| 7 | Merge all overlapping intervals | ? |
| 8 | Given intervals, find minimum meeting rooms needed | ? |
| 9 | Find minimum coins to make a given amount | ? |
| 10 | Find all root-to-leaf paths in a binary tree | ? |

<details>
<summary>Answers (click only after writing your guesses)</summary>

1. **Two Pointers** — sorted array + find pair
2. **Sliding Window** — "longest substring with condition"
3. **Fast & Slow Pointers** — cycle detection keyword
4. **BFS** — level by level = queue
5. **Backtracking** — "all possible" = explore + undo
6. **Dynamic Programming** — count ways / minimize cost with overlapping subproblems
7. **Merge Intervals** — overlapping ranges keyword
8. **Merge Intervals** — meeting rooms = interval overlap counting (trick question!)
9. **Dynamic Programming** — greedy fails here (see Greedy file for why!)
10. **DFS** — "all paths" = depth first

</details>

**Score yourself**:
- 9–10 correct → Pattern recognition is sharp. Start LeetCode.
- 6–8 correct → Re-read the pattern overview, then retry.
- Below 6 → Spend another day on `01_pattern_overview.md` and `pattern_cheatsheet.md` before coding.

> **Tutor's rule**: Do this quiz again after every 5 LeetCode problems you solve. Your score should increase each time.
