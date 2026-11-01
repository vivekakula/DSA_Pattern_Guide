# Pattern Daily Session Breakdown 📚

How to study the 18 pattern chapters, session by session. Dynamic programming is split into 1D and 2D study blocks.

> **Format**: Each pattern shows exactly what to do in every 90-minute session.  
> **Session structure**: 15 min review → 45 min learn/trace → 30 min code.  
> **LC day structure**: 15 min review → 75 min solve (timed, no hints).  
> Numbers in parentheses are time targets — treat them as guidelines, not hard limits.

---

## Pattern 0 — Setup & Overview (Week 1, Mon)
**File**: `01_pattern_overview.md`, `pattern_cheatsheet.md`, `README.md`

**Session (90 min)**:
1. Read `README.md` — understand the folder structure (10 min)
2. Read `01_pattern_overview.md` — scan the 18 pattern entries and their "When to Use" clues (20 min)
3. Read `pattern_cheatsheet.md` — scan every keyword row. Do NOT memorize yet, just recognize (20 min)
4. On paper, without looking: write down as many pattern names as you remember (10 min)
5. Check what you missed. Circle those patterns. (5 min)
6. Re-read `01_pattern_overview.md` flowchart — trace the decision tree with your finger (10 min)
7. Write the "Big 5" pattern keywords that appear most often on interviews (15 min)

**Key insight**: You are not memorizing today. You are building a mental map of the territory.

**Self-check**: Can you name several patterns and explain when they might apply? If not, review the overview before moving on.

---

## Pattern 1 — Two Pointers
**File**: `02_two_pointers.md` | **Week 1 (Tue + Wed)**

### Session A — Tue: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what does "two pointers" mean? When would you use it? Don't open any file.
2. **Read** (25 min): Read `02_two_pointers.md` completely. Pay attention to:
   - The 3 configurations: opposite ends, same direction, two arrays
   - The keyword trigger list (sorted array, palindrome, pair sum)
3. **Trace on paper** (30 min): Do the Two Sum dry-run table manually:
   - Draw `arr = [1, 2, 3, 4, 6]`, `target = 6`
   - Write columns: `left | right | arr[left] | arr[right] | sum | Decision`
   - Fill every row until you find the pair — check your table against the file
4. **Trace second example** (20 min): Remove Duplicates — draw the array, trace `left` and `right` values at each step on paper

**Goal**: Understand *why* the two pointers converge — not just that they do.

---

### Session B — Wed: Code + LeetCode (90 min)
1. **Review** (15 min): Without opening the file, write the Two Pointers template skeleton:
   ```
   left = 0, right = n-1
   while (left < right) { ... move left or right ... }
   ```
   If you got it wrong, note what was missing.
2. **Code from scratch** (30 min):
   - Code Two Sum (sorted array) without looking at the file
   - Stuck after 10 min? Peek at the structure only — not the full solution
   - Code Remove Duplicates from scratch
3. **LeetCode** (45 min, timed):
   - LC 125 — Valid Palindrome (Easy, 15 min max)
   - LC 26 — Remove Duplicates from Sorted Array (Easy, 15 min max)
   - LC 15 — 3Sum (Medium, 20 min — uses two pointers inside a loop)

**Key insight**: Two pointers works on sorted data because sorting gives you a guarantee — moving left increases sum, moving right decreases it.

**Self-check**: Can you write the template from memory? Can you explain why we move `left` vs `right`?

---

## Pattern 2 — Sliding Window
**File**: `03_sliding_window.md` | **Week 1 (Thu + Fri) + Week 2 (Mon + Tue)**

### Session A — Week 1 Thu: Fixed Window Read + Trace (90 min)
1. **Review** (15 min): Write from memory — difference between two pointers and sliding window.
2. **Read** (25 min): Read `03_sliding_window.md` — focus on Template 1 (fixed size) only. Read the "When to Use" trigger keywords.
3. **Trace fixed window** (30 min): Max Sum Subarray of size 3, `arr = [2, 1, 5, 1, 3, 2]`:
   - Draw columns: `i | element added | element removed | window_sum | max_sum`
   - Fill each row — trace the window sliding right
4. **Understand the core idea** (20 min): Write in your own words: "In a fixed window, every step I add `arr[i]` and remove `arr[i - k]`." Verify this matches the template.

---

### Session B — Week 1 Fri: Fixed Window Code + LC (90 min)
1. **Review** (15 min): Write Template 1 from memory. Check it.
2. **Code fixed window** (35 min): Code Max Sum Subarray of size K from scratch — no file open
3. **LeetCode** (40 min, timed):
   - LC 643 — Maximum Average Subarray I (Easy, 15 min)
   - LC 1004 — Max Consecutive Ones III (Medium, 25 min)

---

### Session C — Week 2 Mon: Dynamic Window Read + Trace (90 min)
1. **Review** (15 min): Write fixed window template from memory.
2. **Read** (25 min): `03_sliding_window.md` — focus on Template 2 (dynamic size). Understand expand/shrink logic.
3. **Trace dynamic window** (35 min): Longest Unique Substring, `s = "abcabcbb"`:
   - Draw columns: `right | s[right] | char_set before | char_set after | window | max_length`
   - Fill each row — when do you shrink left?
4. **Compare** (15 min): Write side by side — when is window fixed vs dynamic?

---

### Session D — Week 2 Tue: Dynamic Window Code + LC (90 min)
1. **Review** (15 min): Write Template 2 from memory (the expand/shrink loop).
2. **Code dynamic window** (30 min): Code Longest Substring Without Repeating Characters from scratch
3. **LeetCode** (45 min, timed):
   - LC 3 — Longest Substring Without Repeating Characters (Medium, 20 min)
   - LC 904 — Fruit Into Baskets (Medium, 25 min) — same pattern, different constraint

**Key insight**: Fixed window = known size, slide right every step. Dynamic window = unknown size, expand right until invalid, shrink left until valid again.

**Self-check**: Can you identify which template to use without thinking? Keyword "exactly K" → fixed. Keyword "at most / longest / minimum" → dynamic.

---

## Pattern 3 — Fast & Slow Pointers
**File**: `04_fast_slow_pointers.md` | **Week 2 (Wed + Thu)**

### Session A — Wed: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — when do slow/fast pointers meet?
2. **Read** (25 min): `04_fast_slow_pointers.md` completely. Focus on: cycle detection logic, finding middle, why fast=2×slow.
3. **Trace cycle detection** (35 min): Draw linked list `1→2→3→4→2` (cycle at node 2):
   - Write columns: `Step | slow | fast | Equal?`
   - Move slow 1 step, fast 2 steps each row — fill until they meet
   - Answer: where do they meet? Why?
4. **Reflect** (15 min): Answer the "After Solving" questions in the file for cycle detection.

---

### Session B — Thu: Code + LC (90 min)
1. **Review** (15 min): Write the fast/slow template from memory:
   ```
   slow = head, fast = head
   while (fast && fast->next) { slow = slow->next; fast = fast->next->next; }
   ```
2. **Code from scratch** (35 min):
   - Code Cycle Detection (return true/false)
   - Code Find Middle of Linked List
   - Both without looking at file
3. **LeetCode** (40 min, timed):
   - LC 141 — Linked List Cycle (Easy, 10 min)
   - LC 876 — Middle of the Linked List (Easy, 10 min)
   - LC 287 — Find the Duplicate Number (Medium, 20 min) — treats array as linked list

**Key insight**: slow and fast always meet inside the cycle. fast moves 2× so the gap between them closes by 1 each step.

**Self-check**: Without looking — why does `fast = head` (not `fast = fast`) when you restart to find cycle start? Draw it out.

---

## Pattern 4 — Binary Search
**File**: `10_binary_search.md` | **Week 3 (Mon + Tue + Wed)**

### Session A — Mon: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what condition must be true to use binary search?
2. **Read** (30 min): `10_binary_search.md` — the standard template section + "After Solving, Ask Yourself." Read the tutor warning: pick ONE template and stick to it.
3. **Trace standard binary search** (30 min): `arr = [1, 3, 5, 7, 9, 11]`, `target = 7`:
   - Write columns: `left | right | mid | arr[mid] | Decision`
   - Fill 3 iterations — which half do you cut each time?
4. **Write** (15 min): In your own words, why is `mid = left + (right - left) / 2` safer than `(left + right) / 2`?

---

### Session B — Tue: Code Variations (90 min)
1. **Review** (15 min): Write the standard binary search template from memory. Check it character by character — `<=` not `<`, `mid + 1` not `mid`.
2. **Code from scratch** (50 min):
   - Standard binary search (target exists)
   - Find first occurrence of target (leftmost)
   - Find last occurrence of target (rightmost)
   - Each one without looking — if stuck after 10 min, read ONLY the condition, not the full code
3. **Understand edge cases** (25 min): What happens when `left = right`? What if target is not in array? Trace both on paper.

---

### Session C — Wed: LC Day (90 min)
1. **Review** (15 min): Write binary search template from memory. Write the "leftmost" variation too.
2. **LeetCode** (75 min, timed):
   - LC 704 — Binary Search (Easy, 10 min)
   - LC 34 — Find First and Last Position in Sorted Array (Medium, 20 min)
   - LC 33 — Search in Rotated Sorted Array (Medium, 25 min)
   - LC 162 — Find Peak Element (Medium, 20 min)

**Key insight**: Binary search is not just for searching arrays. It's for any problem where the answer space is monotonic (as X increases, result never decreases).

**Self-check**: Given a new problem — how do you decide if binary search applies? Write your 3-step check: (1) sorted or monotonic? (2) can I check if a value is feasible in O(log n)? (3) am I looking for a boundary?

---

## Pattern 5 — Merge Intervals
**File**: `05_merge_intervals.md` | **Week 3 (Thu + Fri)**

### Session A — Thu: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what does "overlapping intervals" mean? When do two intervals NOT overlap?
2. **Read** (25 min): `05_merge_intervals.md` completely. The key is the sort-then-scan strategy.
3. **Trace merge** (35 min): `intervals = [[1,4],[2,6],[8,10],[15,18]]`:
   - Sort by start
   - Draw a number line with the intervals
   - Work through each interval: does it overlap with last result interval?
   - Write out the result array after each step
4. **Understand** (15 min): There are 3 cases when merging two intervals — write them: (a) fully contained, (b) partially overlapping, (c) no overlap. Draw each.

---

### Session B — Fri: Code + LC (90 min)
1. **Review** (15 min): Write the merge intervals template from memory:
   - Sort
   - Push first interval
   - For each next interval: overlap → extend back(), no overlap → push new
2. **Code from scratch** (35 min):
   - Merge Overlapping Intervals
   - Insert New Interval into sorted list
3. **LeetCode** (40 min, timed):
   - LC 56 — Merge Intervals (Medium, 15 min)
   - LC 57 — Insert Interval (Medium, 25 min)

**Key insight**: Always sort by start time first. Two intervals `[a,b]` and `[c,d]` overlap if and only if `c <= b`. The merged interval end is `max(b, d)`.

**Self-check**: Can you draw the overlap check condition `intervals[i][0] <= result.back()[1]` as a diagram?

---

## Pattern 6 — BFS (Tree)
**File**: `08_bfs_tree.md` | **Week 4 (Mon + Tue)**

### Session A — Mon: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what data structure does BFS use? What does "level order" mean?
2. **Read** (25 min): `08_bfs_tree.md` — focus on the level-order traversal. Read the key insight about `level_size`.
3. **Trace level-order** (35 min): Tree `[3, 9, 20, null, null, 15, 7]`:
   - Draw the tree
   - Simulate the queue state at each step: what was popped, what was pushed, what's in `current_level`
   - Write the final result array
4. **Understand** (15 min): Why must `level_size = q.size()` be captured BEFORE the inner loop? What breaks if you use `q.size()` directly in the for-condition?

---

### Session B — Tue: Code + LC (90 min)
1. **Review** (15 min): Write BFS level-order template from memory — queue, outer while, `level_size`, inner for loop.
2. **Code from scratch** (35 min):
   - Level Order Traversal (returns `vector<vector<int>>`)
   - Zigzag Level Order (alternating direction per level)
3. **LeetCode** (40 min, timed):
   - LC 102 — Binary Tree Level Order Traversal (Medium, 15 min)
   - LC 199 — Binary Tree Right Side View (Medium, 25 min)

**Key insight**: BFS guarantees you process nodes level by level. Capture `level_size` before the inner loop — the queue grows as you push children, so reading `q.size()` mid-loop gives the wrong count.

---

## Pattern 7 — DFS (Tree)
**File**: `09_dfs_tree.md` | **Week 4 (Wed + Thu)**

### Session A — Wed: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — BFS uses a queue. DFS uses what? What are preorder / inorder / postorder?
2. **Read** (25 min): `09_dfs_tree.md` — path sum problems, max depth, and tree diameter. Focus on the recursive template.
3. **Trace path sum** (35 min): Tree `[5, 4, 8, 11, null, 13, 4, 7, 2]`, target=22:
   - Trace the recursion — which branch is pursued first?
   - Write the call stack at each step (just node values)
   - At what point does it return true?
4. **Compare** (15 min): Write: "Use BFS when _____. Use DFS when _____." Fill both blanks.

---

### Session B — Thu: Code + LC (90 min)
1. **Review** (15 min): Write recursive DFS template from memory:
   ```
   if (!root) return base_case;
   left = dfs(root->left);
   right = dfs(root->right);
   return combine(left, right, root->val);
   ```
2. **Code from scratch** (35 min):
   - Max Depth of Binary Tree
   - Path Sum (return true/false)
   - Both without looking
3. **LeetCode** (40 min, timed):
   - LC 104 — Maximum Depth of Binary Tree (Easy, 10 min)
   - LC 113 — Path Sum II (Medium, 30 min) — collect all valid paths

**Session C — Fri (same week): BFS vs DFS Comparison + LC (90 min)**
1. **Review** (15 min): Explain to yourself when BFS wins vs DFS (BFS = shortest path / levels; DFS = paths / exhaustive). Write it.
2. **Problem-type drill** (30 min): For each problem below, decide BFS or DFS before coding:
   - "Return nodes at each level" → ?
   - "Does a path from root to leaf sum to X?" → ?
   - "Find the shortest path between two nodes" → ?
   - "Count all root-to-leaf paths with sum X" → ?
3. **LeetCode** (45 min):
   - LC 104 — solve using BFS this time (level count) — 10 min
   - LC 116 — Populating Next Right Pointers (Medium, 35 min) — BFS

**Key insight**: DFS goes deep first (uses recursion / stack). BFS goes wide first (uses queue). Both visit every node — the difference is *order*, which matters for certain problems.

**Self-check**: Can you write both templates from memory? Can you name one problem type that requires BFS (not DFS)?

---

## Pattern 8 — Top K Elements (Heap)
**File**: `11_top_k_elements.md` | **Week 5 (Mon + Tue)**

### Session A — Mon: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what is a min-heap? What does `priority_queue<int, vector<int>, greater<int>>` do?
2. **Read** (25 min): `11_top_k_elements.md` completely. The key insight: use a min-heap of size K to track K largest elements.
3. **Trace K-largest** (35 min): `nums = [3, 1, 5, 12, 2, 11]`, K=3:
   - Simulate the min-heap: push each number, pop when size > K
   - Write heap state after each operation: what's in heap, what's the top?
   - Final answer: what remains in heap?
4. **Understand** (15 min): Why does a **min**-heap give you the K **largest**? Explain the logic in your own words.

---

### Session B — Tue: Code + LC (90 min)
1. **Review** (15 min): Write the min-heap template and max-heap declaration from memory. Write when to use each.
2. **Code from scratch** (40 min):
   - K Largest Elements (min-heap, size K)
   - K Most Frequent Elements (use pair `{frequency, value}` in heap)
3. **LeetCode** (35 min, timed):
   - LC 215 — Kth Largest Element in Array (Medium, 15 min)
   - LC 347 — Top K Frequent Elements (Medium, 20 min)

**Key insight**:
- K largest → min-heap of size K (the root = Kth largest, acts as "bouncer")
- K smallest → max-heap of size K (the root = Kth smallest)
- K most frequent → sort by frequency, use heap with `{freq, val}` pairs

**Self-check**: Without looking — write the `priority_queue` declaration for a min-heap of pairs sorted by first element descending.

---

## Pattern 9 — Backtracking
**File**: `14_backtracking.md` | **Week 5 (Wed + Thu + Fri)**

### Session A — Wed: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what are the 3 steps in backtracking? (Choose, Explore, Unchoose)
2. **Read** (30 min): `14_backtracking.md` completely. Focus on the Choose→Explore→Unchoose framework and the pruning section.
3. **Trace Subsets** (30 min): `nums = [1, 2, 3]`:
   - Draw the decision tree — each node is a choice (include or exclude)
   - Write the `current` array at each leaf node
   - All 8 subsets should appear at the leaves
4. **Understand** (15 min): Why is `current.pop_back()` (unchoose) necessary? What happens if you skip it?

---

### Session B — Thu: Code Subsets (90 min)
1. **Review** (15 min): Write backtracking template from memory:
   ```
   backtrack(current, result, start) {
     result.push_back(current);
     for (i = start; i < nums.size(); i++) {
       current.push_back(nums[i]);
       backtrack(current, result, i + 1);
       current.pop_back();
     }
   }
   ```
2. **Code from scratch** (45 min):
   - Subsets (LC 78) — without looking
   - Subsets II with duplicates (sort first, skip `nums[i] == nums[i-1]` when `i > start`)
3. **LeetCode** (30 min):
   - LC 78 — Subsets (Medium, 15 min)
   - LC 90 — Subsets II (Medium, 15 min)

---

### Session C — Fri: Code Permutations + LC (90 min)
1. **Review** (15 min): Write backtracking template. Note the difference: subsets use `start` index; permutations use a `used[]` boolean array.
2. **Code from scratch** (35 min):
   - Permutations (no duplicates) — use `used[]` array
   - Combination Sum (unlimited reuse — pass `i` not `i+1` in recursive call)
3. **LeetCode** (40 min):
   - LC 46 — Permutations (Medium, 20 min)
   - LC 39 — Combination Sum (Medium, 20 min)

**Key insight**: Every backtracking problem is a decision tree. The template is identical — only the base case and pruning condition change. Master one version, and you can adapt it to any variant.

**Self-check**: Can you identify what changes between Subsets, Permutations, and Combination Sum? Write the 3 key differences.

---

## Pattern 10 — Dynamic Programming (1D)
**File**: `15_dynamic_programming.md` | **Week 6 (Mon + Tue + Wed)**

### Session A — Mon: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what is the difference between memoization and tabulation?
2. **Read** (30 min): `15_dynamic_programming.md` — read the plain-English Fibonacci analogy section first, then the "Jargon decoded" block. Do NOT skip the analogy.
3. **Trace Fibonacci with memo** (25 min): Compute `fib(5)` twice:
   - First: naive recursion (draw the full call tree — count duplicate calls)
   - Second: with memoization (draw the tree — how many calls are eliminated?)
4. **Trace tabulation** (20 min): Fill the `dp` array for Climbing Stairs, n=6:
   - `dp[1]=1, dp[2]=2`
   - Fill `dp[3]` through `dp[6]` — write each formula and result

---

### Session B — Tue: Code (90 min)
1. **Review** (15 min): Write the 1D DP (Fibonacci-style) template from memory:
   ```
   dp[0] = base; dp[1] = base;
   for (i = 2; i <= n; i++) dp[i] = dp[i-1] + dp[i-2];
   ```
2. **Code from scratch** (50 min):
   - Climbing Stairs (Fibonacci variant)
   - House Robber (`dp[i] = max(dp[i-1], dp[i-2] + nums[i])`)
   - Both without any references
3. **Verify logic** (25 min): For House Robber — trace `dp` array for `nums = [2, 7, 9, 3, 1]`. Write each `dp[i]` and which choice was made (rob or skip).

---

### Session C — Wed: Coin Change + LC (90 min)
1. **Review** (15 min): Write Climbing Stairs and House Robber recurrences from memory.
2. **New pattern — Coin Change** (30 min): `dp[i]` = min coins to make amount `i`:
   - `dp[0] = 0`, `dp[i] = min(dp[i - coin] + 1)` for all coins
   - Trace for `coins = [1, 5, 6]`, `amount = 11` — fill the dp table row by row
3. **Code from scratch** (20 min): Code Coin Change without looking
4. **LeetCode** (25 min):
   - LC 70 — Climbing Stairs (Easy, 8 min)
   - LC 198 — House Robber (Medium, 17 min)

**Key insight**: DP = answer to big problem is built from answers to smaller problems. Always identify: (1) what does `dp[i]` mean? (2) how does `dp[i]` depend on previous values?

**Self-check**: Explain House Robber in one sentence: "At each house, I choose between _____ and _____."

---

## Pattern 11 — Cyclic Sort
**File**: `06_cyclic_sort.md` | **Week 7 (Mon + Tue)**

### Session A — Mon: Read + Code (90 min)
1. **Review** (15 min): Write from memory — what range of values makes cyclic sort applicable? (Answer: values in range [1, n] or [0, n-1])
2. **Read** (20 min): `06_cyclic_sort.md` — the core idea: each number `nums[i]` should be at index `nums[i] - 1`. If it's not, swap it to the right place.
3. **Trace** (25 min): `nums = [3, 1, 5, 4, 2]`:
   - At i=0: nums[0]=3, should be at index 2. Swap nums[0] and nums[2].
   - Continue until every number is at its correct index
   - Write the array state after each swap
4. **Code from scratch** (30 min):
   - Sort the array using cyclic sort
   - Find Missing Number (after sort, scan for `nums[i] != i+1`)

---

### Session B — Tue: LC (90 min)
1. **Review** (15 min): Write the cyclic sort loop condition: `while (nums[i] != i + 1) swap(...)` — what is the termination condition?
2. **Code Find All Duplicates from scratch** (30 min): After cyclic sort, any `nums[i] != i+1` is a duplicate
3. **LeetCode** (45 min, timed):
   - LC 268 — Missing Number (Easy, 15 min)
   - LC 442 — Find All Duplicates in an Array (Medium, 30 min)

**Key insight**: The pattern only applies when values are in a known range [1,n]. The "correct position" rule `nums[i]` belongs at `index nums[i]-1` is the entire algorithm.

---

## Pattern 12 — In-place Reversal (Linked List)
**File**: `07_in_place_reversal.md` | **Week 7 (Wed + Thu)**

### Session A — Wed: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — how do you reverse a linked list? (prev, current, next pointers)
2. **Read** (20 min): `07_in_place_reversal.md` — full reversal + reverse a sublist (between positions m and n).
3. **Trace full reversal** (30 min): List `1→2→3→4→5`:
   - Write columns: `prev | current | next | list state`
   - Walk through each step — draw the arrows changing direction
4. **Trace reversal in k-group** (25 min): `1→2→3→4→5`, k=2:
   - Which groups get reversed? `[1,2]` and `[3,4]`, node 5 stays.
   - Draw the final linked list

---

### Session B — Thu: Code + LC (90 min)
1. **Review** (15 min): Write the 3-pointer reversal loop from memory:
   ```
   prev = nullptr;
   while (current) { next = current->next; current->next = prev; prev = current; current = next; }
   ```
2. **Code from scratch** (40 min):
   - Reverse Linked List (full)
   - Reverse Nodes in k-Group (harder — find group end, reverse, reconnect)
3. **LeetCode** (35 min):
   - LC 206 — Reverse Linked List (Easy, 10 min)
   - LC 92 — Reverse Linked List II (reverse only m to n) (Medium, 25 min)

**Key insight**: Every pointer reassignment needs the "save next" step first. Miss it once and the list is lost.

---

## Pattern 13 — K-way Merge
**File**: `12_k_way_merge.md` | **Week 7 (Fri)**

### Session (90 min — single session, lighter pattern)
1. **Review** (15 min): Write from memory — what data structure is used to efficiently get the minimum among K sorted lists?
2. **Read** (20 min): `12_k_way_merge.md` — the heap-based K-way merge. Each heap entry = `{value, list_index, element_index}`.
3. **Trace** (25 min): 3 sorted lists: `[1,4,7]`, `[2,5,8]`, `[3,6,9]`:
   - Initial heap state: `{1,0,0}`, `{2,1,0}`, `{3,2,0}`
   - Pop min, push next from same list — trace 5 steps, write heap contents each time
4. **Code from scratch** (30 min): Merge K Sorted Lists — use `priority_queue` with `{val, list_idx, node_ptr}`

**LeetCode**: LC 23 — Merge k Sorted Lists (Hard, 30 min — included in code session)

**Key insight**: Use a min-heap seeded with the first element of each list. Each pop gives you the global minimum; then push the *next* element from that same list.

---

## Pattern 14 — Modified Binary Search
**File**: `13_modified_binary_search.md` | **Week 8 (Mon + Tue + Wed)**

### Session A — Mon: Read + Trace (90 min)
1. **Review** (15 min): Write the standard binary search template from memory. You will modify it today.
2. **Read** (25 min): `13_modified_binary_search.md` — focus on "binary search on answer space" (not searching an array, searching for the minimum feasible answer).
3. **Trace "Koko Eating Bananas"** (30 min): `piles = [3, 6, 7, 11]`, h=8:
   - The search space is `k` (eating speed): `left=1`, `right=11`
   - At each mid: can Koko finish in h hours at speed mid? (sum of `ceil(pile/mid)`)
   - Trace 3 iterations — write `left`, `right`, `mid`, feasible? decision
4. **Key idea** (20 min): Write: "In binary search on answer, `feasible(mid)` returns ___. If true, move ___ half. If false, move ___ half."

---

### Session B — Tue: Code (90 min)
1. **Review** (15 min): Write the "binary search on answer" template from memory:
   ```
   left = min_val, right = max_val;
   while (left < right) {
     mid = left + (right - left) / 2;
     if (feasible(mid)) right = mid;
     else left = mid + 1;
   }
   return left;
   ```
2. **Code from scratch** (50 min):
   - Koko Eating Bananas (`feasible` = can finish all piles in h hours)
   - Capacity to Ship Packages in D Days (`feasible` = can ship all in D days at this capacity)
3. **Understand** (25 min): For Capacity to Ship — why is `right = sum(weights)` the upper bound? Why is `left = max(weights)` the lower bound?

---

### Session C — Wed: LC (90 min)
1. **Review** (15 min): Write both templates (array search + answer-space search) from memory.
2. **LeetCode** (75 min, timed):
   - LC 875 — Koko Eating Bananas (Medium, 25 min)
   - LC 1011 — Capacity to Ship Packages (Medium, 25 min)
   - LC 1482 — Minimum Days to Make m Bouquets (Medium, 25 min)

**Key insight**: If a problem asks "find the minimum X such that X is feasible" AND you can check feasibility in O(n), then the answer is binary searchable.

**Self-check**: Can you identify the search space bounds for a new problem? (lower bound = minimum possible answer, upper bound = maximum possible answer)

---

## Pattern 15 — Greedy
**File**: `16_greedy.md` | **Week 8 (Thu + Fri)**

### Session A — Thu: Read + Safety Check (90 min)
1. **Review** (15 min): Write from memory — when is greedy safe? When does it fail?
2. **Read** (25 min): `16_greedy.md` — read the "Is Greedy Safe? 3-Question Test" table and the counterexample (coins {1,3,4}, amount=6).
3. **Apply the 3-question test** (30 min): For each problem below, run the test:
   - Activity selection (pick most meetings that fit)
   - Coin change with standard denominations {1, 5, 10, 25}
   - Coin change with {1, 3, 4}, amount=6 (where greedy fails — WHY?)
4. **Trace Jump Game** (20 min): `nums = [2, 3, 1, 1, 4]`:
   - At each index, update `maxReach = max(maxReach, i + nums[i])`
   - Can you ever reach the last index?

---

### Session B — Fri: Code + LC (90 min)
1. **Review** (15 min): Write the 3-question greedy safety test from memory. Write Jump Game greedy logic.
2. **Code from scratch** (35 min):
   - Jump Game (can you reach last index? track `maxReach`)
   - Jump Game II (minimum jumps — track current reach + next reach)
3. **LeetCode** (40 min, timed):
   - LC 55 — Jump Game (Medium, 20 min)
   - LC 134 — Gas Station (Medium, 20 min)

**Key insight**: Greedy works when the local optimal choice leads to the global optimum. Always verify with the 3-question test or a counterexample before trusting greedy.

---

## Pattern 16 — Advanced DP (2D)
**File**: `15_dynamic_programming.md` | **Week 9 (Mon + Tue + Wed)**

### Session A — Mon: Read + Trace LCS (90 min)
1. **Review** (15 min): Write the 1D DP recurrence for House Robber from memory. Now think: what does a 2D `dp[i][j]` table represent?
2. **Read** (25 min): `15_dynamic_programming.md` — 2D DP section. Focus on LCS (Longest Common Subsequence).
3. **Trace LCS table** (35 min): `text1 = "abcde"`, `text2 = "ace"`:
   - Draw a 6×4 table (0-indexed rows for text1, columns for text2)
   - Fill row by row: if `text1[i-1] == text2[j-1]`, `dp[i][j] = dp[i-1][j-1] + 1`, else `max(dp[i-1][j], dp[i][j-1])`
   - Read the answer from `dp[5][3]`
4. **Understand** (15 min): Write in plain English what `dp[i][j]` means in LCS.

---

### Session B — Tue: Code Knapsack (90 min)
1. **Review** (15 min): Write the LCS recurrence from memory.
2. **Understand Knapsack** (20 min): `dp[i][w]` = max value using first i items with weight limit w. Recurrence:
   - If item i fits: `dp[i][w] = max(dp[i-1][w], dp[i-1][w - weight[i]] + value[i])`
   - If it doesn't fit: `dp[i][w] = dp[i-1][w]`
3. **Code from scratch** (50 min):
   - 0/1 Knapsack (classic)
   - LCS

---

### Session C — Wed: Edit Distance + LC (90 min)
1. **Review** (15 min): Write LCS and Knapsack recurrences from memory.
2. **Trace Edit Distance** (25 min): `word1 = "horse"`, `word2 = "ros"`:
   - `dp[i][j]` = min operations to convert `word1[0..i]` to `word2[0..j]`
   - If chars match: `dp[i][j] = dp[i-1][j-1]`
   - Else: `dp[i][j] = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1])`  (delete, insert, replace)
3. **Code Edit Distance from scratch** (20 min)
4. **LeetCode** (30 min):
   - LC 1143 — Longest Common Subsequence (Medium, 15 min)
   - LC 72 — Edit Distance (Hard, 15 min — you already traced it)

**Key insight**: 2D DP problems always have a 2D state. Ask: "what are the two changing variables?" Those become your table dimensions.

---

## Pattern 17 — Graphs
**File**: `17_graphs.md` | **Week 10 + Week 11**

### Session A — Week 10 Mon: Read Graph BFS + Trace (90 min)
1. **Review** (15 min): Write from memory — how is Graph BFS different from Tree BFS? (Answer: graphs need a `visited[]` array; trees don't have cycles)
2. **Read** (25 min): `17_graphs.md` — Pattern 1 (Graph BFS) and the Number of Provinces example.
3. **Trace Number of Provinces** (35 min): Adjacency matrix for 4 nodes:
   - Mark visited, push to queue, process neighbors
   - Write queue contents at each step — how many BFS calls = number of provinces?
4. **Understand** (15 min): Write the 3 things that differ from tree BFS: (1) `visited[]` array, (2) loop over all unvisited nodes, (3) adjacency list/matrix instead of children

---

### Session B — Week 10 Tue: Code Graph BFS + LC (90 min)
1. **Review** (15 min): Write Graph BFS template from memory — the outer loop, visited marking, queue.
2. **Code from scratch** (30 min): BFS that counts connected components (number of provinces)
3. **LeetCode** (45 min):
   - LC 547 — Number of Provinces (Medium, 20 min)
   - LC 994 — Rotten Oranges (Medium, 25 min) — multi-source BFS (push all rotten oranges first)

---

### Session C — Week 10 Wed: Graph DFS + Code (90 min)
1. **Review** (15 min): Write Graph BFS template. Now write Graph DFS skeleton — same but recursive, no queue.
2. **Read** (20 min): `17_graphs.md` — Pattern 2 (Graph DFS) and cycle detection
3. **Code from scratch** (35 min):
   - Graph DFS (count components)
   - Cycle detection in undirected graph (pass `parent` node to avoid false positive)
4. **LeetCode** (20 min): LC 200 — Number of Islands (Medium) — DFS flood-fill

---

### Session D — Week 10 Thu: Graph DFS LC (90 min)
1. **Review** (15 min): Write both Graph BFS and DFS templates.
2. **LeetCode** (75 min):
   - LC 733 — Flood Fill (Easy, 15 min)
   - LC 130 — Surrounded Regions (Medium, 30 min)
   - LC 417 — Pacific Atlantic Water Flow (Medium, 30 min)

---

### Session E — Week 10 Fri: Topological Sort Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what is topological sort? When is it valid?
2. **Read** (25 min): `17_graphs.md` — Pattern 3 (Kahn's Algorithm). Read the step-by-step in-degree trace example.
3. **Trace Kahn's** (35 min): 4 courses: `0←1, 0←2, 1←3, 2←3` (prerequisites):
   - Compute in-degrees: {0:2, 1:1, 2:1, 3:0}
   - Start: push node 3 (in_degree=0)
   - Each step: pop, reduce neighbor in_degrees, push any that hit 0
   - Write queue, order, and in-degree array at each step
4. **Check** (15 min): If `order.size() != n`, what does that mean?

---

### Session F — Week 11 Mon: Topological Sort Code + LC (90 min)
1. **Review** (15 min): Write Kahn's algorithm from memory — adjacency list, in-degree array, queue, order vector.
2. **Code from scratch** (35 min): Kahn's algorithm for course schedule (can all courses be completed?)
3. **LeetCode** (40 min):
   - LC 207 — Course Schedule (Medium, 20 min)
   - LC 210 — Course Schedule II (Medium, 20 min) — return the order

---

### Session G — Week 11 Tue: Topological Sort LC (90 min)
1. **Review** (15 min): Write Kahn's — focus on the cycle detection check at end.
2. **LeetCode** (75 min):
   - LC 802 — Find Eventual Safe States (Medium, 40 min)
   - LC 310 — Minimum Height Trees (Medium, 35 min)

---

### Session H — Week 11 Wed: Dijkstra Read + Trace (90 min)
1. **Review** (15 min): Write from memory — when do you use Dijkstra instead of BFS? (weighted edges, non-negative weights)
2. **Read** (25 min): `17_graphs.md` — Pattern 4 (Dijkstra). Read the distance table trace example.
3. **Trace Dijkstra** (35 min): 5-node graph with weighted edges:
   - Initial: `dist = [0, INF, INF, INF, INF]`, heap = `{(0,0)}`
   - Each step: pop min-distance node, relax neighbors, push updated distances
   - Write distance array and heap state at each step
4. **Understand** (15 min): Why does Dijkstra fail with negative edge weights? Draw a counterexample.

---

### Session I — Week 11 Thu: Dijkstra Code + LC (90 min)
1. **Review** (15 min): Write Dijkstra template from memory — `dist[]` init, min-heap with `{dist, node}`, relaxation.
2. **Code from scratch** (35 min): Dijkstra — shortest distance from source to all nodes
3. **LeetCode** (40 min):
   - LC 743 — Network Delay Time (Medium, 20 min)
   - LC 1631 — Path with Minimum Effort (Medium, 20 min)

---

### Session J — Week 11 Fri: Union-Find Read + Code + LC (90 min)
1. **Review** (15 min): Write from memory — what two operations does Union-Find support?
2. **Read** (20 min): `17_graphs.md` — Pattern 5 (Union-Find). Path compression + union by rank.
3. **Code from scratch** (30 min): `find(x)` with path compression + `unite(x, y)` with rank
4. **LeetCode** (25 min):
   - LC 323 — Number of Connected Components (Medium, 12 min)
   - LC 684 — Redundant Connection (Medium, 13 min)

**Key insight (Graphs)**: BFS = level order, shortest unweighted path. DFS = explore deep, good for connectivity and paths. Topo Sort = dependency ordering, detect cycles in directed graphs. Dijkstra = shortest weighted path. Union-Find = dynamic connectivity, cycle detection.

---

## Pattern 18 — Monotonic Stack
**File**: `18_monotonic_stack.md` | **Week 12 (Mon + Tue + Wed)**

### Session A — Mon: Read + Trace (90 min)
1. **Review** (15 min): Write from memory — what makes a stack "monotonic"? (Elements are kept in strictly increasing or decreasing order from bottom to top)
2. **Read** (25 min): `18_monotonic_stack.md` — two types table (decreasing vs increasing) + NGE pattern.
3. **Trace NGE** (35 min): `arr = [2, 1, 2, 4, 3]`, find Next Greater Element for each:
   - Write columns: `i | arr[i] | stack (indices) | Action | NGE assigned`
   - Push index to stack. If `arr[i] > arr[stack.top()]`, pop and assign NGE = `arr[i]`
   - Walk through all 5 elements
4. **Understand** (15 min): What does it mean for an element to be "still in the stack" at the end?

---

### Session B — Tue: Code + LC (90 min)
1. **Review** (15 min): Write the monotonic stack NGE template from memory — stack stores indices, pop while `arr[i] > arr[st.top()]`.
2. **Code from scratch** (35 min):
   - Next Greater Element (output NGE for each position)
   - Daily Temperatures (same pattern, result = distance to next warmer day)
3. **LeetCode** (40 min):
   - LC 739 — Daily Temperatures (Medium, 20 min)
   - LC 901 — Online Stock Span (Medium, 20 min) — decreasing stack, count span

---

### Session C — Wed: Largest Rectangle + LC (90 min)
1. **Review** (15 min): Write the stack-of-indices template. Stack stores indices. Pop when current bar is shorter.
2. **Read + Trace Largest Rectangle** (30 min): `heights = [2, 1, 5, 6, 2, 3]`:
   - Use sentinel (push -1, append 0 to heights)
   - Walk through — when you pop, calculate width using `i - stack.top() - 1`
   - Trace on paper which rectangles are computed at each pop
3. **Code Largest Rectangle from scratch** (25 min)
4. **LeetCode** (20 min): LC 84 — Largest Rectangle in Histogram (Hard, 20 min — you traced it)

**Key insight**: Stack stores INDICES, not values. Elements remaining in the stack at the end have no greater element to their right — their NGE = -1 (or infinity, depending on problem).

**Self-check**: Can you explain in one sentence when to use a decreasing stack vs increasing stack?

---

## Pattern 19 — Tries
**File**: `19_tries.md` | **Week 12 (Thu + Fri) + Week 13 (Mon)**

### Session A — Week 12 Thu: Read + Draw (90 min)
1. **Review** (15 min): Write from memory — what is a Trie node? (array of children + `is_end` boolean)
2. **Read** (25 min): `19_tries.md` — TrieNode structure, Trie class, insert/search/startsWith.
3. **Draw on paper** (35 min): Build a Trie for words: `"cat"`, `"car"`, `"card"`, `"care"`, `"bat"`:
   - Draw each node as a circle with its character
   - Mark `is_end = true` nodes with a star
   - Which node is shared between "car", "card", and "care"?
4. **Understand the key distinction** (15 min): Write it:
   - `search("car")` → must check `is_end` at last node
   - `startsWith("car")` → only checks if path exists, NOT `is_end`

---

### Session B — Week 12 Fri: Code from Scratch (90 min)
1. **Review** (15 min): Write the TrieNode struct from memory:
   ```cpp
   struct TrieNode {
     TrieNode* children[26] = {};
     bool is_end = false;
   };
   ```
2. **Code from scratch** (50 min):
   - `insert(word)` — walk and create nodes
   - `search(word)` — walk and check `is_end` at last character
   - `startsWith(prefix)` — walk only, no `is_end` check
   - ALL three without looking
3. **LeetCode** (25 min): LC 208 — Implement Trie (Medium, 25 min)

---

### Session C — Week 13 Mon: Trie LC (90 min)
1. **Review** (15 min): Write all 3 Trie methods from memory. Can you do it faster than last time?
2. **LeetCode** (75 min):
   - LC 211 — Add and Search Word (Medium, 35 min) — `'.'` matches any character, use DFS in Trie
   - LC 212 — Word Search II (Hard, 40 min) — Trie + grid DFS (prune by prefix)

**Key insight**: A Trie's power is prefix sharing. If 1000 words start with "pre", they share the same 3 nodes. `search` vs `startsWith` differ by ONE line — the `is_end` check.

**Self-check**: Without looking — can you code `insert` in under 5 minutes? Can you explain what `children[26]` means vs a `map<char, TrieNode*>`?

---

## End-of-Phase Review Sessions

### After Phase 1 (Week 6 Fri + Sun)
**Fri — Flag Weak Patterns (90 min)**:
- Go through patterns 1–10 in `pattern_cheatsheet.md`
- For each: write the template from memory (5 min max per pattern)
- Any pattern where you needed >2 minutes → mark as weak
- Set aside 1 extra LC problem for each weak pattern next week

**Sun — Final Phase 1 Review (45 min)**:
- 10 min: Keyword drill from `pattern_cheatsheet.md`
- 20 min: Re-take Active Recall quiz in `01_pattern_overview.md` (patterns 1–10 only)
- 15 min: Re-solve one problem from Week 4 that you struggled on

---

### After Phase 2 (Week 9 Fri + Sun)
**Fri — Review Pattern Templates (90 min)**:
- Open a blank file. Write a one-sentence "when to use" and a template skeleton for the patterns studied so far
- Time yourself: target < 5 min per pattern
- Which ones took longest? → Extra review next week

**Sun (45 min)**:
- Full Active Recall quiz in `01_pattern_overview.md`
- Note which answers were uncertain and add a related problem for review

---

### After Phase 3 (Week 13 Sun)
**Final Review (45 min)**:
- Write "when to use" for the 18 pattern chapters from memory — no files
- For each of the 3 new patterns (Graphs, Monotonic Stack, Tries): can you explain the core data structure in 2 sentences?
- Identify your 3 weakest patterns by name — those get 2 extra LC problems before interviews

---

## Quick Reference: Session Count Per Pattern

| Pattern | Sessions | Weeks |
|---------|----------|-------|
| Overview & Setup | 1 | W1 Mon |
| Two Pointers | 2 | W1 Tue–Wed |
| Sliding Window | 4 | W1 Thu–Fri, W2 Mon–Tue |
| Fast & Slow Pointers | 2 | W2 Wed–Thu |
| Binary Search | 3 | W3 Mon–Wed |
| Merge Intervals | 2 | W3 Thu–Fri |
| BFS Tree | 2 | W4 Mon–Tue |
| DFS Tree | 3 | W4 Wed–Fri |
| Top K Elements | 2 | W5 Mon–Tue |
| Backtracking | 3 | W5 Wed–Fri |
| DP 1D | 3 | W6 Mon–Wed |
| Cyclic Sort | 2 | W7 Mon–Tue |
| In-place Reversal | 2 | W7 Wed–Thu |
| K-way Merge | 1 | W7 Fri |
| Modified Binary Search | 3 | W8 Mon–Wed |
| Greedy | 2 | W8 Thu–Fri |
| Advanced DP 2D | 3 | W9 Mon–Wed |
| Graphs | 10 | W10–W11 |
| Monotonic Stack | 3 | W12 Mon–Wed |
| Tries | 3 | W12 Thu–Fri, W13 Mon |

**Total learning sessions**: 56 weekday sessions + 13 Sunday reviews = 13 weeks at 1.5 hrs/day
