# DSA Pattern Cheatsheet 📋

Quick reference guide for identifying and applying patterns.

---

 Pattern Recognition Guide

| Keywords in Problem | Pattern to Use |
|---------------------|----------------|
| "pair/triplet sum", "palindrome", sorted array | **Two Pointers** |
| "subarray", "substring", "consecutive", "window" | **Sliding Window** |
| "cycle detection", "middle of list", "happy number" | **Fast & Slow Pointers** |
| "overlapping intervals", "merge", "insert interval" | **Merge Intervals** |
| "missing number", array with 1 to n | **Cyclic Sort** |
| "reverse linked list", "reverse in groups" | **In-place Reversal** |
| "level order", "minimum depth", tree by level | **BFS** |
| "all paths", "path sum", tree traversal | **DFS** |
| "sorted array", "search", "find peak" | **Binary Search** |
| "k largest", "k smallest", "k frequent" | **Top K (Heap)** |
| "merge k sorted", "smallest range" | **K-way Merge** |
| "all combinations", "all subsets", "permutations" | **Backtracking** |
| "maximum/minimum", "count ways", "longest/shortest" | **Dynamic Programming** |
| "minimum coins", "jump game", scheduling | **Greedy** |

---

 Time Complexity Quick Reference

| Pattern | Typical Time | Typical Space |
|---------|--------------|---------------|
| Two Pointers | O(n) | O(1) |
| Sliding Window | O(n) | O(k) |
| Fast & Slow | O(n) | O(1) |
| Merge Intervals | O(n log n) | O(n) |
| Cyclic Sort | O(n) | O(1) |
| BFS | O(n) | O(n) |
| DFS | O(n) | O(h) |
| Binary Search | O(log n) | O(1) |
| Heap (Top K) | O(n log k) | O(k) |
| K-way Merge | O(n log k) | O(k) |
| Backtracking | O(2ⁿ) or O(n!) | O(n) |
| DP | O(n²) typical | O(n) or O(n²) |

---

 Code Templates

 Two Pointers
```cpp
int left = 0, right = arr.size() - 1;
while (left < right) {
    if (condition) {
        return result;
    } else if (need_increase) {
        left++;
    } else {
        right--;
    }
}
```

 Sliding Window (Dynamic)
```cpp
int left = 0;
for (int right = 0; right < arr.size(); right++) {
    // Expand window
    add(arr[right]);
    
    // Shrink window
    while (invalid) {
        remove(arr[left]);
        left++;
    }
    
    // Update result
    result = max(result, right - left + 1);
}
```

 Fast & Slow Pointers
```cpp
ListNode* slow = head;
ListNode* fast = head;
while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
    if (slow == fast) {
        return true;  // Cycle detected
    }
}
return false;
```

 Binary Search
```cpp
int left = 0, right = arr.size() - 1;
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) {
        return mid;
    } else if (arr[mid] < target) {
        left = mid + 1;
    } else {
        right = mid - 1;
    }
}
```

 DFS (Recursion)
```cpp
int dfs(TreeNode* node) {
    if (!node) {
        return 0;
    }
    
    // Process current node
    int result = process(node);
    
    // Recurse on children
    int left_result = dfs(node->left);
    int right_result = dfs(node->right);
    
    return combine(result, left_result, right_result);
}
```

 BFS (Level Order)
```cpp
include <queue>

queue<TreeNode*> q;
q.push(root);
while (!q.empty()) {
    int level_size = q.size();
    for (int i = 0; i < level_size; i++) {
        TreeNode* node = q.front();
        q.pop();
        process(node);
        if (node->left) q.push(node->left);
        if (node->right) q.push(node->right);
    }
}
```

 Backtracking
```cpp
void backtrack(vector<int>& path, vector<int>& choices) {
    if (is_solution(path)) {
        result.push_back(path);
        return;
    }
    
    for (int choice : choices) {
        // Choose
        path.push_back(choice);
        
        // Explore
        backtrack(path, next_choices);
        
        // Unchoose
        path.pop_back();
    }
}
```

 Top K Elements (Heap)
```cpp
include <queue>

priority_queue<int, vector<int>, greater<int>> minHeap;  // Min heap
for (int num : arr) {
    minHeap.push(num);
    if (minHeap.size() > k) {
        minHeap.pop();
    }
}
// minHeap contains k largest elements
```

---

 Decision Tree

```
START: Read the problem

├─ Array/String problem?
│  ├─ Sorted or can sort?
│  │  ├─ Find pairs/triplets → TWO POINTERS
│  │  ├─ Search element → BINARY SEARCH
│  │  └─ Numbers 1 to n → CYCLIC SORT
│  │
│  ├─ Contiguous subarray?
│  │  └─ YES → SLIDING WINDOW
│  │
│  └─ All combinations?
│      └─ YES → BACKTRACKING

├─ Linked List problem?
│  ├─ Cycle detection → FAST & SLOW
│  └─ Reverse → IN-PLACE REVERSAL

├─ Tree/Graph problem?
│  ├─ Level by level → BFS
│  ├─ All paths/depth → DFS
│  └─ Search → DFS/BFS

├─ Interval problem?
│  └─ Overlapping ranges → MERGE INTERVALS

├─ Top K problem?
│  └─ K largest/smallest → HEAP

├─ Multiple sorted arrays?
│  └─ Merge them → K-WAY MERGE

├─ Optimization problem?
│  ├─ Overlapping subproblems → DP
│  └─ Greedy choice property → GREEDY

└─ Can't identify?
   └─ Try simpler approach or ask for hints
```

---

 Common Problem Patterns

 Array Problems
- **Two Sum** → Two Pointers or HashMap
- **Max Subarray Sum** → Sliding Window or Kadane's
- **Missing Number** → Cyclic Sort or XOR
- **Find Duplicate** → Cyclic Sort or Floyd's

 String Problems
- **Anagram** → HashMap or Sliding Window
- **Palindrome** → Two Pointers
- **Substring Search** → Sliding Window
- **Permutations** → Backtracking

 Linked List Problems
- **Cycle** → Fast & Slow
- **Middle** → Fast & Slow
- **Reverse** → In-place Reversal
- **Merge** → Two Pointers

 Tree Problems
- **Level Order** → BFS
- **Path Sum** → DFS
- **Diameter** → DFS
- **LCA** → DFS

 Graph Problems
- **Shortest Path** → BFS
- **Connected Components** → DFS/BFS
- **Cycle Detection** → DFS with colors
- **Topological Sort** → DFS or Kahn's

---

 Problem-Solving Checklist

1. ✅ **Understand the problem**
   - What is input/output?
   - Any constraints?
   - Edge cases?

2. ✅ **Identify the pattern**
   - Check keywords
   - Check data structure
   - Check constraints

3. ✅ **Choose approach**
   - Brute force first
   - Optimize with pattern
   - Consider trade-offs

4. ✅ **Write pseudocode**
   - Outline logic
   - Check edge cases

5. ✅ **Implement**
   - Use template
   - Keep it clean

6. ✅ **Test**
   - Normal cases
   - Edge cases
   - Large inputs

---

 Time-Saving Tips

1. **Sort first?** Many patterns work better on sorted data
2. **Can you use HashMap?** O(1) lookup is powerful
3. **Can you use two passes?** Sometimes easier than one pass
4. **Work backwards?** Some DP problems are easier this way
5. **Can you binary search?** If you can check validity in O(n)

---

 Red Flags (What NOT to do)

❌ Using nested loops without thinking (probably O(n²))
❌ Not considering edge cases (empty, single element, duplicates)
❌ Ignoring constraints (they hint at the solution!)
❌ Premature optimization (get it working first)
❌ Not testing with examples

---

 Quick Reference Card

**Most Common Optimizations:**
- O(n²) → O(n): Two Pointers, Sliding Window
- O(n²) → O(n log n): Sorting + Two Pointers
- O(n) → O(log n): Binary Search
- O(2ⁿ) → O(n²): Dynamic Programming
- O(n) space → O(1): In-place algorithms

**Most Used Data Structures:**
1. HashMap (frequency, lookup)
2. Heap (top k, min/max)
3. Queue (BFS, sliding window)
4. Stack (DFS, monotonic problems)
5. Set (uniqueness, deduplication)

---

Keep this cheatsheet handy while solving problems! 🚀
