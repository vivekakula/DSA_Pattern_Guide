# Practice Problem Set 🎯

A comprehensive collection of 40+ problems covering all 16 DSA patterns. Each problem includes:
- ✅ LeetCode link for online practice
- 💡 3-tier hints system
- 💻 C++ solutions with detailed explanations
- ⚡ Time & space complexity analysis

**How to use:**
1. Read the problem statement
2. Try for 10-15 minutes (use hints if stuck)
3. Identify the pattern
4. Implement your solution
5. Compare with provided solutions

**Progress Tracking:** Check off problems as you complete them!

---

## 📚 Table of Contents

**Level 1: Foundation (Easy)**
- Two Pointers (Problems 1, 5, 9)
- Sliding Window (Problems 2, 6, 10)
- Fast & Slow Pointers (Problems 3, 11)

**Level 2: Intermediate (Medium)**
- Two Pointers (Problem 4)
- Sliding Window (Problem 7, 8)
- Merge Intervals (Problems 12, 13, 14)
- Cyclic Sort (Problems 15, 16, 17)
- In-place Reversal (Problems 18, 19)
- Binary Search (Problems 20, 21, 22)

**Level 3: Advanced (Medium-Hard)**
- BFS Tree (Problems 23, 24)
- DFS Tree (Problems 25, 26, 27)
- Top K Elements (Problems 28, 29, 30)
- K-way Merge (Problems 31, 32)
- Backtracking (Problems 33, 34, 35)

**Level 4: Expert (Hard)**
- Dynamic Programming (Problems 36, 37, 38)
- Greedy (Problems 39, 40)
- Modified Binary Search (Problem 41)

---

## Level 1: Foundation Problems (Easy)

### Problem 1: Pair with Target Sum ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#167 - Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

Given a **sorted** array, find two numbers that add up to a target value. Return their indices.

```
Input: arr = [1, 2, 3, 4, 6], target = 6
Output: [1, 3] (indices of 2 and 4)

Input: arr = [2, 5, 9, 11], target = 11
Output: [0, 2] (indices of 2 and 9)
```

**Your task**: 
- What pattern should you use?
- What's the time complexity?
- Write the solution

<details>
<summary>💡 Hint 1 (Click to expand)</summary>

The array is **sorted**. Can you use pointers at both ends?
</details>

<details>
<summary>💡 Hint 2</summary>

Start with one pointer at the beginning and one at the end. If the sum is too small, which pointer should you move?
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Two Pointers
- Start with left=0, right=n-1
- If sum < target: move left++ (need bigger sum)
- If sum > target: move right-- (need smaller sum)
- If sum == target: found!
</details>

---

### Problem 2: Maximum Sum Subarray ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: Related to [#643 - Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/)

Find the maximum sum of any contiguous subarray of size k.

```
Input: arr = [2, 1, 5, 1, 3, 2], k = 3
Output: 9 (subarray [5, 1, 3])

Input: arr = [2, 3, 4, 1, 5], k = 2
Output: 7 (subarray [3, 4])
```

**Your task**:
- What pattern should you use?
- How do you avoid recalculating sum each time?
- Write the solution

<details>
<summary>💡 Hint 1</summary>

The subarray has a **fixed size k**. Think of it as a window moving through the array.
</details>

<details>
<summary>💡 Hint 2</summary>

Instead of recalculating the sum each time, can you remove the leftmost element and add the new rightmost element?
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Sliding Window (Fixed Size)
- Calculate sum of first k elements
- Slide: subtract arr[i-k], add arr[i]
- Track maximum as you go
- Time: O(n), Space: O(1)
</details>

---

### Problem 3: Middle of Linked List ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#876 - Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

Find the middle node of a linked list. If there are two middle nodes, return the second one.

```
Input: 1 -> 2 -> 3 -> 4 -> 5
Output: 3

Input: 1 -> 2 -> 3 -> 4 -> 5 -> 6
Output: 4
```

**Your task**:
- What pattern should you use?
- Can you do it in one pass?
- Write the solution

<details>
<summary>💡 Hint 1</summary>

Can you use two pointers that move at different speeds?
</details>

<details>
<summary>💡 Hint 2</summary>

What if one pointer moves twice as fast as the other? Where will the slow pointer be when the fast one reaches the end?
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Fast & Slow Pointers
- slow moves 1 step, fast moves 2 steps
- When fast reaches end, slow is at middle
- Time: O(n), Space: O(1)
</details>

---

## Level 2: Intermediate Problems (Medium)

### Problem 4: Longest Substring with K Distinct Characters ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#340 - Longest Substring with At Most K Distinct Characters](https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/) (Premium)

Find the length of the longest substring with at most k distinct characters.

```
Input: s = "araaci", k = 2
Output: 4 (substring "araa")

Input: s = "araaci", k = 1
Output: 2 (substring "aa")

Input: s = "cbbebi", k = 3
Output: 5 (substring "cbbeb")
```

**Your task**:
- Identify the pattern
- What data structure helps track distinct characters?
- When should you shrink the window?

<details>
<summary>💡 Hint 1</summary>

This is about finding the **longest** substring with a constraint. Think expandable window.
</details>

<details>
<summary>💡 Hint 2</summary>

Use a HashMap to count character frequencies. Shrink the window when you have more than k distinct characters.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Sliding Window (Dynamic)
- Expand window by adding right character
- Track frequency in HashMap
- Shrink from left while distinct > k
- Time: O(n), Space: O(k)
</details>

---

### Problem 5: Squares of Sorted Array ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#977 - Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)

Given a sorted array (can have negative numbers), return sorted array of squares.

```
Input: [-4, -1, 0, 3, 10]
Output: [0, 1, 9, 16, 100]

Input: [-7, -3, 2, 3, 11]
Output: [4, 9, 9, 49, 121]
```

**Your task**:
- Why is this not straightforward?
- Which pattern helps avoid sorting after squaring?
- Write an O(n) solution

<details>
<summary>💡 Hint 1</summary>

The largest squares come from the extreme values (most negative or most positive). Where are they located?
</details>

<details>
<summary>💡 Hint 2</summary>

Compare squares at both ends and place the larger one at the end of the result array.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Two Pointers
- Pointers at both ends
- Compare squares, place larger at end of result
- Fill result array from right to left
- Time: O(n), Space: O(n)
</details>

---

### Problem 6: Find All Anagrams ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#438 - Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)

Find all start indices of anagrams of pattern in string.

```
Input: s = "cbaebabacd", p = "abc"
Output: [0, 6]
Explanation: 
  "cba" at index 0 is an anagram of "abc"
  "bac" at index 6 is an anagram of "abc"

Input: s = "abab", p = "ab"
Output: [0, 1, 2]
```

**Your task**:
- What pattern fits this problem?
- How do you check if window is an anagram?
- What's the time complexity?

<details>
<summary>💡 Hint 1</summary>

An anagram has the same character frequencies. Use a **fixed-size window** equal to pattern length.
</details>

<details>
<summary>💡 Hint 2</summary>

Maintain character frequencies for the window and compare with pattern frequencies.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Sliding Window (Fixed Size)
- Window size = pattern length
- Track char frequencies in HashMap
- When frequencies match, record index
- Time: O(n), Space: O(1) - at most 26 chars
</details>

---

### Problem 7: Linked List Cycle ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#141 - Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

Determine if a linked list has a cycle.

```
Input: 3 -> 2 -> 0 -> -4 -> (back to 2)
Output: True

Input: 1 -> 2 -> NULL
Output: False
```

**Your task**:
- What pattern detects cycles efficiently?
- Can you do it with O(1) space?
- What happens when they meet?

<details>
<summary>💡 Hint 1</summary>

If there's a cycle, will two pointers moving at different speeds ever meet?
</details>

<details>
<summary>💡 Hint 2</summary>

Use slow (1 step) and fast (2 steps) pointers. In a cycle, the fast pointer will eventually catch the slow one.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Fast & Slow Pointers
- Fast moves 2x speed of slow
- If they meet, there's a cycle
- If fast reaches null, no cycle
- Time: O(n), Space: O(1)
</details>

---

## Level 3: Advanced Problems (Medium-Hard)

### Problem 8: Minimum Window Substring ⭐⭐⭐
**Difficulty**: Hard  
**Pattern**: ?  
**LeetCode**: [#76 - Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/)

Find the minimum window in string s that contains all characters of string t.

```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"

Input: s = "a", t = "a"
Output: "a"

Input: s = "a", t = "aa"
Output: "" (not possible)
```

**Your task**:
- Which pattern works for "minimum window" problems?
- How do you track if all characters are matched?
- When do you try to shrink?

<details>
<summary>💡 Hint 1</summary>

For "minimum" problems, expand window until valid, then shrink to minimize.
</details>

<details>
<summary>💡 Hint 2</summary>

Track required character counts. When all requirements are met, try shrinking from the left.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Sliding Window (Dynamic - Minimize)
- Expand until window contains all chars
- Shrink while valid, track minimum
- Use HashMap for char frequencies
- Time: O(n+m), Space: O(m)
</details>

---

### Problem 9: Three Sum ⭐⭐⭐
**Difficulty**: Medium-Hard  
**Pattern**: ?  
**LeetCode**: [#15 - 3Sum](https://leetcode.com/problems/3sum/)

Find all unique triplets that sum to zero.

```
Input: [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]

Input: [0, 0, 0]
Output: [[0, 0, 0]]
```

**Your task**:
- How do you avoid O(n³) brute force?
- How do you handle duplicates?
- Combine which patterns?

<details>
<summary>💡 Hint 1</summary>

Sort the array first. Fix one element and find two others that complete the sum.
</details>

<details>
<summary>💡 Hint 2</summary>

After fixing one element, use two pointers to find the other two in O(n) time.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Two Pointers (with iteration)
- Sort array: O(n log n)
- For each element, use two pointers for remaining
- Skip duplicates carefully
- Time: O(n²), Space: O(1)
</details>

---

### Problem 10: Fruits Into Baskets ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#904 - Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/)

Pick maximum consecutive fruits with at most 2 types.

```
Input: fruits = [1, 2, 1]
Output: 3

Input: fruits = [0, 1, 2, 2]
Output: 3 (pick [1, 2, 2])

Input: fruits = [1, 2, 3, 2, 2]
Output: 4 (pick [2, 3, 2, 2])
```

**Your task**:
- This is "longest subarray with at most 2 distinct elements"
- Which pattern handles this?
- How do you track fruit types?

<details>
<summary>💡 Hint 1</summary>

This is disguised as "longest substring with at most 2 distinct characters."
</details>

<details>
<summary>💡 Hint 2</summary>

Use a HashMap to track fruit types. Shrink when you have more than 2 types.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Sliding Window (Dynamic)
- Expand window, track fruit frequencies
- Shrink when distinct types > 2
- Track maximum length
- Time: O(n), Space: O(1)
</details>

---

### Problem 11: Happy Number ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#202 - Happy Number](https://leetcode.com/problems/happy-number/)

A happy number is defined by: starting with any positive integer, replace the number by the sum of the squares of its digits. Repeat until the number equals 1 (happy), or it loops endlessly in a cycle (not happy).

```
Input: n = 19
Output: true
Explanation: 
1² + 9² = 82
8² + 2² = 68
6² + 8² = 100
1² + 0² + 0² = 1

Input: n = 2
Output: false (enters a cycle)
```

**Your task**:
- How do you detect if you're in a cycle?
- Can you do it without a HashSet?

<details>
<summary>💡 Hint 1</summary>

This is a cycle detection problem in disguise!
</details>

<details>
<summary>💡 Hint 2</summary>

Use fast and slow pointers. If they meet and it's not 1, there's a cycle.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Fast & Slow Pointers
- Slow computes next once, fast computes twice
- If slow reaches 1: happy number
- If slow == fast and != 1: cycle detected
- Time: O(log n), Space: O(1)
</details>

---

### Problem 12: Merge Intervals ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#56 - Merge Intervals](https://leetcode.com/problems/merge-intervals/)

Given a collection of intervals, merge all overlapping intervals.

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: [1,3] and [2,6] overlap

Input: [[1,4],[4,5]]
Output: [[1,5]]
```

**Your task**:
- How should you process the intervals?
- When do two intervals overlap?
- What's the time complexity?

<details>
<summary>💡 Hint 1</summary>

Sort the intervals by start time first.
</details>

<details>
<summary>💡 Hint 2</summary>

After sorting, you only need to compare each interval with the last merged interval.
</details>

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Merge Intervals
- Sort by start time: O(n log n)
- Compare current.start with last.end
- If overlap: merge by taking max(end)
- Time: O(n log n), Space: O(n)
</details>

---

### Problem 13: Insert Interval ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#57 - Insert Interval](https://leetcode.com/problems/insert-interval/)

Insert a new interval into a sorted list of non-overlapping intervals and merge if necessary.

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]

Input: intervals = [[1,2],[3,5],[6,7],[8,10]], newInterval = [4,8]
Output: [[1,2],[3,10]]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Merge Intervals
- Add all intervals before newInterval
- Merge all overlapping intervals
- Add all intervals after
- Time: O(n), Space: O(n)
</details>

---

### Problem 14: Meeting Rooms II ⭐⭐⭐
**Difficulty**: Medium-Hard  
**Pattern**: ?  
**LeetCode**: [#253 - Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) (Premium)

Find minimum number of meeting rooms required.

```
Input: [[0,30],[5,10],[15,20]]
Output: 2
Explanation: Need 2 rooms: one for [0,30], one for [5,10] and [15,20]

Input: [[7,10],[2,4]]
Output: 1
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Merge Intervals (with Min Heap)
- Sort by start time
- Use min-heap to track room end times
- Time: O(n log n), Space: O(n)
</details>

---

### Problem 15: Find Missing Number ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#268 - Missing Number](https://leetcode.com/problems/missing-number/)

Given array containing n distinct numbers in range [0, n], find the missing number.

```
Input: [3, 0, 1]
Output: 2

Input: [0, 1]
Output: 2

Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Cyclic Sort (or Math)
- Place each number at its index
- The index without correct number is the answer
- Time: O(n), Space: O(1)
</details>

---

### Problem 16: Find All Duplicates ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#442 - Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/)

Given array of integers where 1 ≤ a[i] ≤ n, some elements appear twice and others once. Find all elements that appear twice.

```
Input: [4,3,2,7,8,2,3,1]
Output: [2,3]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Cyclic Sort
- Place each at its correct position
- Numbers not in correct position are duplicates
- Time: O(n), Space: O(1)
</details>

---

### Problem 17: First Missing Positive ⭐⭐⭐
**Difficulty**: Hard  
**Pattern**: ?  
**LeetCode**: [#41 - First Missing Positive](https://leetcode.com/problems/first-missing-positive/)

Find the smallest missing positive integer.

```
Input: [1,2,0]
Output: 3

Input: [3,4,-1,1]
Output: 2

Input: [7,8,9,11,12]
Output: 1
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Cyclic Sort
- Place positive numbers at their index
- First index without correct number + 1 is answer
- Time: O(n), Space: O(1)
</details>

---

### Problem 18: Reverse Linked List ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#206 - Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)

Reverse a singly linked list.

```
Input: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
Output: 5 -> 4 -> 3 -> 2 -> 1 -> NULL
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: In-place Reversal
- Use three pointers: prev, current, next
- Reverse links one by one
- Time: O(n), Space: O(1)
</details>

---

### Problem 19: Reverse Sublist ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#92 - Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/)

Reverse a linked list from position m to n.

```
Input: 1 -> 2 -> 3 -> 4 -> 5, m = 2, n = 4
Output: 1 -> 4 -> 3 -> 2 -> 5
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: In-place Reversal
- Navigate to m-1
- Reverse m to n
- Reconnect the parts
- Time: O(n), Space: O(1)
</details>

---

### Problem 20: Binary Search ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#704 - Binary Search](https://leetcode.com/problems/binary-search/)

Implement binary search on a sorted array.

```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4

Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Binary Search
- left = 0, right = n-1
- mid = left + (right-left)//2
- Eliminate half each iteration
- Time: O(log n), Space: O(1)
</details>

---

### Problem 21: Search in Rotated Array ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#33 - Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

Search target in a rotated sorted array.

```
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Modified Binary Search
- Find which half is sorted
- Check if target is in sorted half
- Time: O(log n), Space: O(1)
</details>

---

### Problem 22: Find Peak Element ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#162 - Find Peak Element](https://leetcode.com/problems/find-peak-element/)

Find a peak element (greater than neighbors).

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak

Input: nums = [1,2,1,3,5,6,4]
Output: 5
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Binary Search
- Compare mid with mid+1
- Move toward the ascending side
- Time: O(log n), Space: O(1)
</details>

---

## Level 4: Expert Problems (Hard)

### Problem 23: Binary Tree Level Order ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#102 - Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/)

Return level order traversal of a binary tree.

```
Input:     3
          / \
         9  20
           /  \
          15   7
Output: [[3],[9,20],[15,7]]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: BFS (Tree)
- Use queue, process level by level
- Track level size before processing
- Time: O(n), Space: O(n)
</details>

---

### Problem 24: Zigzag Level Order ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#103 - Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

Traverse tree in zigzag pattern.

```
Input:     3
          / \
         9  20
           /  \
          15   7
Output: [[3],[20,9],[15,7]]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: BFS (Tree)
- Use BFS with level tracking
- Reverse alternate levels
- Time: O(n), Space: O(n)
</details>

---

### Problem 25: Path Sum ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#112 - Path Sum](https://leetcode.com/problems/path-sum/)

Determine if tree has root-to-leaf path with target sum.

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,null,1], target = 22
Output: true
Explanation: Path 5->4->11->2 = 22
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: DFS (Tree)
- Recursively check left and right
- Subtract current value from sum
- Time: O(n), Space: O(h)
</details>

---

### Problem 26: All Paths for Sum ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#113 - Path Sum II](https://leetcode.com/problems/path-sum-ii/)

Find all root-to-leaf paths with target sum.

```
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], target = 22
Output: [[5,4,11,2],[5,8,4,5]]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: DFS (Tree)
- DFS with path tracking
- Copy path when leaf reached
- Time: O(n²), Space: O(n)
</details>

---

### Problem 27: Diameter of Binary Tree ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#543 - Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/)

Find diameter (longest path between any two nodes).

```
Input:    1
         / \
        2   3
       / \     
      4   5    
Output: 3
Explanation: Path is [4,2,1,3] or [5,2,1,3]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: DFS (Tree)
- Calculate height of each subtree
- Diameter at node = left_height + right_height
- Time: O(n), Space: O(h)
</details>

---

### Problem 28: Kth Largest Element ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#215 - Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/)

Find the kth largest element in an array.

```
Input: [3,2,1,5,6,4], k = 2
Output: 5

Input: [3,2,3,1,2,4,5,5,6], k = 4
Output: 4
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Top K Elements (Min Heap)
- Use min-heap of size k
- Keep k largest elements in heap
- Time: O(n log k), Space: O(k)
</details>

---

### Problem 29: Top K Frequent Elements ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#347 - Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)

Return k most frequent elements.

```
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Input: nums = [1], k = 1
Output: [1]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Top K Elements (Heap)
- Count frequencies in HashMap
- Use min-heap to keep top k
- Time: O(n log k), Space: O(n)
</details>

---

### Problem 30: K Closest Points ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#973 - K Closest Points to Origin](https://leetcode.com/problems/k-closest-points-to-origin/)

Find k closest points to origin.

```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation: Distance: sqrt(5) < sqrt(10)
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Top K Elements (Max Heap)
- Use max-heap of size k
- Store (distance, point)
- Time: O(n log k), Space: O(k)
</details>

---

### Problem 31: Merge K Sorted Lists ⭐⭐⭐
**Difficulty**: Hard  
**Pattern**: ?  
**LeetCode**: [#23 - Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/)

Merge k sorted linked lists.

```
Input: [
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: K-way Merge (Min Heap)
- Put first element of each list in min-heap
- Extract min, add next from that list
- Time: O(n log k), Space: O(k)
</details>

---

### Problem 32: Smallest Range Covering K Lists ⭐⭐⭐
**Difficulty**: Hard  
**Pattern**: ?  
**LeetCode**: [#632 - Smallest Range Covering Elements from K Lists](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists/)

Find smallest range that includes at least one number from each list.

```
Input: [[4,10,15,24,26],[0,9,12,20],[5,18,22,30]]
Output: [20,24]
Explanation: Contains 20 from list 2, 24 from list 1, and 22 from list 3
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: K-way Merge (Min Heap)
- Track min (from heap) and max
- Range = max - min
- Time: O(n log k), Space: O(k)
</details>

---

### Problem 33: Subsets ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#78 - Subsets](https://leetcode.com/problems/subsets/)

Find all possible subsets (power set).

```
Input: [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Backtracking
- For each element: include or exclude
- Build subsets recursively
- Time: O(2ⁿ), Space: O(n)
</details>

---

### Problem 34: Permutations ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#46 - Permutations](https://leetcode.com/problems/permutations/)

Find all possible permutations.

```
Input: [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Backtracking
- Swap elements recursively
- Backtrack after each recursive call
- Time: O(n!), Space: O(n)
</details>

---

### Problem 35: N-Queens ⭐⭐⭐
**Difficulty**: Hard  
**Pattern**: ?  
**LeetCode**: [#51 - N-Queens](https://leetcode.com/problems/n-queens/)

Place n queens on n×n board so none attack each other.

```
Input: n = 4
Output: [
 [".Q..",
  "...Q",
  "Q...",
  "..Q."],
  
 ["..Q.",
  "Q...",
  "...Q",
  ".Q.."]
]
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Backtracking
- Try placing queen in each column
- Check diagonals and columns
- Backtrack if invalid
- Time: O(n!), Space: O(n²)
</details>

---

### Problem 36: Climbing Stairs ⭐
**Difficulty**: Easy  
**Pattern**: ?  
**LeetCode**: [#70 - Climbing Stairs](https://leetcode.com/problems/climbing-stairs/)

How many ways to climb n stairs if you can take 1 or 2 steps?

```
Input: n = 3
Output: 3
Explanation: 1+1+1, 1+2, 2+1

Input: n = 5
Output: 8
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Dynamic Programming
- dp[i] = dp[i-1] + dp[i-2]
- Base: dp[0]=1, dp[1]=1
- Time: O(n), Space: O(1)
</details>

---

### Problem 37: Longest Common Subsequence ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#1143 - Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/)

Find length of longest common subsequence.

```
Input: text1 = "abcde", text2 = "ace" 
Output: 3
Explanation: LCS is "ace"

Input: text1 = "abc", text2 = "def"
Output: 0
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Dynamic Programming
- dp[i][j] = LCS of text1[0..i] and text2[0..j]
- If match: dp[i][j] = dp[i-1][j-1] + 1
- Else: max(dp[i-1][j], dp[i][j-1])
- Time: O(m×n), Space: O(m×n)
</details>

---

### Problem 38: Coin Change ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#322 - Coin Change](https://leetcode.com/problems/coin-change/)

Find minimum coins to make amount.

```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1

Input: coins = [2], amount = 3
Output: -1
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Dynamic Programming
- dp[i] = min coins for amount i
- dp[i] = min(dp[i-coin] + 1) for all coins
- Time: O(amount × coins), Space: O(amount)
</details>

---

### Problem 39: Jump Game II ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#45 - Jump Game II](https://leetcode.com/problems/jump-game-ii/)

Find minimum jumps to reach last index.

```
Input: [2,3,1,1,4]
Output: 2
Explanation: Jump 1 step from index 0 to 1, then 3 steps to last
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Greedy
- Track current jump range and farthest reachable
- Jump when reaching end of current range
- Time: O(n), Space: O(1)
</details>

---

### Problem 40: Task Scheduler ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#621 - Task Scheduler](https://leetcode.com/problems/task-scheduler/)

Minimum intervals to execute tasks with cooling time.

```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Greedy (with Heap)
- Count frequencies, schedule most frequent first
- Calculate idle slots needed
- Time: O(n), Space: O(1)
</details>

---

### Problem 41: Search in 2D Matrix II ⭐⭐
**Difficulty**: Medium  
**Pattern**: ?  
**LeetCode**: [#240 - Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

Search in matrix where rows and columns are sorted.

```
Input: matrix = [
  [1,4,7,11,15],
  [2,5,8,12,19],
  [3,6,9,16,22]
], target = 5
Output: true
```

<details>
<summary>💡 Hint 3 (Approach)</summary>

**Pattern**: Modified Binary Search
- Start at top-right corner
- If target < current: move left
- If target > current: move down
- Time: O(m+n), Space: O(1)
</details>

---

## Quick Self-Check

Before checking solutions, identify the pattern for each:

**Level 1 (Easy):**
1. Problem 1: _______ | 2. Problem 2: _______ | 3. Problem 3: _______

**Level 2 (Medium):**
4. Problem 4: _______ | 5. Problem 5: _______ | 6. Problem 6: _______
7. Problem 7: _______ | 8. Problem 8: _______ | 9. Problem 9: _______
10. Problem 10: _______ | 11. Problem 11: _______ | 12. Problem 12: _______

**Level 3 (Advanced):**
13-27: Identify patterns for Merge Intervals, Cyclic Sort, In-place Reversal, Binary Search, BFS, DFS, Top K

**Level 4 (Expert):**
28-41: Identify patterns for K-way Merge, Backtracking, DP, Greedy

---

---

## 💡 Solutions

Scroll down for detailed solutions...

<br><br><br><br><br><br><br><br><br><br>

---

## Solution 1: Pair with Target Sum

**Pattern**: Two Pointers  
**Time**: O(n) | **Space**: O(1)

**Why this pattern?**
- Sorted array ✓
- Finding pairs ✓
- Can work from both ends ✓
```cpp
#include <vector>
using namespace std;

vector<int> twoSumSorted(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    
    while (left < right) {
        int current_sum = arr[left] + arr[right];
        
        if (current_sum == target) {
            return {left, right};
        } else if (current_sum < target) {
            left++;  // Need bigger sum
        } else {
            right--;  // Need smaller sum
        }
    }
    
    return {-1, -1};
}

// Test
int main() {
    vector<int> arr1 = {1, 2, 3, 4, 6};
    vector<int> result1 = twoSumSorted(arr1, 6);  // [1, 3]
    
    vector<int> arr2 = {2, 5, 9, 11};
    vector<int> result2 = twoSumSorted(arr2, 11);  // [0, 2]
    
    return 0;
}
```

**Key insight**: Move left when sum is small, move right when sum is large.

---

## Solution 2: Maximum Sum Subarray

**Pattern**: Sliding Window (Fixed Size)  
**Time**: O(n) | **Space**: O(1)

**Why this pattern?**
- Contiguous subarray ✓
- Fixed size (k) ✓
- Can slide window instead of recalculating ✓
```cpp
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

int maxSumSubarray(vector<int>& arr, int k) {
    int max_sum = INT_MIN;
    int window_sum = 0;
    int window_start = 0;
    
    for (int window_end = 0; window_end < arr.size(); window_end++) {
        window_sum += arr[window_end];  // Add next element
        
        // When window hits size k
        if (window_end >= k - 1) {
            max_sum = max(max_sum, window_sum);
            window_sum -= arr[window_start];  // Remove first element
            window_start++;
        }
    }
    
    return max_sum;
}

// Test
int main() {
    vector<int> arr1 = {2, 1, 5, 1, 3, 2};
    cout << maxSumSubarray(arr1, 3);  // Output: 9
    
    vector<int> arr2 = {2, 3, 4, 1, 5};
    cout << maxSumSubarray(arr2, 2);  // Output: 7
    
    return 0;
}
```

**Key insight**: Add new element, remove old element - don't recalculate entire sum.

---

## Solution 3: Middle of Linked List

**Pattern**: Fast & Slow Pointers  
**Time**: O(n) | **Space**: O(1)

**Why this pattern?**
- Linked list ✓
- Need middle element ✓
- One pass solution ✓
```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* findMiddle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;        // Move 1 step
        fast = fast->next->next;  // Move 2 steps
    }
    
    return slow;  // Slow is at middle
}

// Test
int main() {
    // Create list: 1 -> 2 -> 3 -> 4 -> 5
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);
    
    ListNode* middle = findMiddle(head);
    cout << middle->val;  // Output: 3
    
    return 0;
}
```

**Key insight**: When fast reaches end, slow is at middle (fast moves 2x speed).

---

 Solution 4: Longest Substring with K Distinct

**Pattern**: Sliding Window (Dynamic)  
**Time**: O(n) | **Space**: O(k)

**Why this pattern?**
- Substring (contiguous) ✓
- "Longest" with constraint ✓
- Need to expand/shrink window ✓

```cpp
include <string>
include <unordered_map>
include <algorithm>
using namespace std;

int longestSubstringKDistinct(string s, int k) {
    unordered_map<char, int> char_frequency;
    int window_start = 0;
    int max_length = 0;
    
    for (int window_end = 0; window_end < s.length(); window_end++) {
        char right_char = s[window_end];
        char_frequency[right_char]++;
        
        // Shrink window until k distinct
        while (char_frequency.size() > k) {
            char left_char = s[window_start];
            char_frequency[left_char]--;
            if (char_frequency[left_char] == 0) {
                char_frequency.erase(left_char);
            }
            window_start++;
        }
        
        max_length = max(max_length, window_end - window_start + 1);
    }
    
    return max_length;
}

// Test
int main() {
    cout << longestSubstringKDistinct("araaci", 2);  // Output: 4
    cout << longestSubstringKDistinct("araaci", 1);  // Output: 2
    cout << longestSubstringKDistinct("cbbebi", 3);  // Output: 5
    
    return 0;
}
```

**Key insight**: Use HashMap to track character counts, shrink when > k distinct.

---

 Solution 5: Squares of Sorted Array

**Pattern**: Two Pointers  
**Time**: O(n) | **Space**: O(n)

**Why this pattern?**
- Sorted array ✓
- But squares of negatives become large ✓
- Largest squares are at ends ✓

```cpp
include <vector>
include <cmath>
using namespace std;

vector<int> sortedSquares(vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n);
    int left = 0, right = n - 1;
    int position = n - 1;  // Fill from end
    
    while (left <= right) {
        int left_square = arr[left] * arr[left];
        int right_square = arr[right] * arr[right];
        
        if (left_square > right_square) {
            result[position] = left_square;
            left++;
        } else {
            result[position] = right_square;
            right--;
        }
        
        position--;
    }
    
    return result;
}

// Test
int main() {
    vector<int> arr1 = {-4, -1, 0, 3, 10};
    vector<int> result1 = sortedSquares(arr1);  // [0, 1, 9, 16, 100]
    
    vector<int> arr2 = {-7, -3, 2, 3, 11};
    vector<int> result2 = sortedSquares(arr2);  // [4, 9, 9, 49, 121]
    
    return 0;
}
```

**Key insight**: Compare squares from both ends, place larger one at end of result.

---

 Solution 6: Find All Anagrams

**Pattern**: Sliding Window (Fixed Size)  
**Time**: O(n) | **Space**: O(1) - at most 26 characters

**Why this pattern?**
- Substring search ✓
- Fixed pattern length ✓
- Need all occurrences ✓

```cpp
include <string>
include <vector>
include <unordered_map>
using namespace std;

vector<int> findAnagrams(string s, string p) {
    vector<int> result;
    unordered_map<char, int> pattern_count;
    unordered_map<char, int> window_count;
    
    // Count pattern characters
    for (char c : p) {
        pattern_count[c]++;
    }
    
    int window_start = 0;
    int matched = 0;
    
    for (int window_end = 0; window_end < s.length(); window_end++) {
        char right_char = s[window_end];
        
        if (pattern_count.count(right_char)) {
            window_count[right_char]++;
            if (window_count[right_char] == pattern_count[right_char]) {
                matched++;
            }
        }
        
        // When window size equals pattern
        if (window_end >= p.length() - 1) {
            if (matched == pattern_count.size()) {
                result.push_back(window_start);
            }
            
            // Shrink window
            char left_char = s[window_start];
            if (pattern_count.count(left_char)) {
                if (window_count[left_char] == pattern_count[left_char]) {
                    matched--;
                }
                window_count[left_char]--;
            }
            window_start++;
        }
    }
    
    return result;
}

// Test
int main() {
    vector<int> result1 = findAnagrams("cbaebabacd", "abc");  // [0, 6]
    vector<int> result2 = findAnagrams("abab", "ab");         // [0, 1, 2]
    
    return 0;
}
```

**Key insight**: Track character frequencies, check if window matches pattern.

---

 Solution 7: Linked List Cycle

**Pattern**: Fast & Slow Pointers  
**Time**: O(n) | **Space**: O(1)

**Why this pattern?**
- Linked list cycle ✓
- Need O(1) space ✓
- Can't use HashSet ✓

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

bool hasCycle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        
        if (slow == fast) {
            return true;  // They met - cycle exists!
        }
    }
    
    return false;  // Fast reached end - no cycle
}

// Test would require creating cycle manually
int main() {
    // Create cycle: 1 -> 2 -> 3 -> 4 -> (back to 2)
    ListNode* head = new ListNode(1);
    ListNode* node2 = new ListNode(2);
    ListNode* node3 = new ListNode(3);
    ListNode* node4 = new ListNode(4);
    
    head->next = node2;
    node2->next = node3;
    node3->next = node4;
    node4->next = node2;  // Create cycle
    
    cout << hasCycle(head);  // Output: 1 (true)
    
    return 0;
}
```

**Key insight**: If there's a cycle, fast will eventually catch up to slow.

---

 Solution 8: Minimum Window Substring

**Pattern**: Sliding Window (Dynamic - Minimize)  
**Time**: O(n + m) | **Space**: O(m)

**Why this pattern?**
- Substring problem ✓
- "Minimum" window ✓
- Need to shrink when valid ✓

```cpp
include <string>
include <unordered_map>
include <climits>
using namespace std;

string minWindow(string s, string t) {
    if (s.empty() || t.empty()) {
        return "";
    }
    
    // Count characters in t
    unordered_map<char, int> need;
    for (char c : t) {
        need[c]++;
    }
    
    unordered_map<char, int> window_counts;
    int have = 0;
    int required = need.size();
    
    int left = 0;
    int min_len = INT_MAX;
    int min_start = 0;
    
    for (int right = 0; right < s.length(); right++) {
        char c = s[right];
        window_counts[c]++;
        
        if (need.count(c) && window_counts[c] == need[c]) {
            have++;
        }
        
        // Shrink while valid
        while (have == required) {
            // Update result
            if (right - left + 1 < min_len) {
                min_len = right - left + 1;
                min_start = left;
            }
            
            // Remove left character
            char left_char = s[left];
            window_counts[left_char]--;
            if (need.count(left_char) && window_counts[left_char] < need[left_char]) {
                have--;
            }
            left++;
        }
    }
    
    return min_len == INT_MAX ? "" : s.substr(min_start, min_len);
}

// Test
int main() {
    cout << minWindow("ADOBECODEBANC", "ABC");  // Output: "BANC"
    cout << minWindow("a", "a");                // Output: "a"
    cout << minWindow("a", "aa");               // Output: ""
    
    return 0;
}
```

**Key insight**: Expand until valid, then shrink to find minimum while maintaining validity.

---

 Solution 9: Three Sum

**Pattern**: Two Pointers (with iteration)  
**Time**: O(n²) | **Space**: O(1) excluding output

**Why this pattern?**
- Need triplets ✓
- Can sort array ✓
- Fix one, use two pointers for rest ✓

```cpp
include <vector>
include <algorithm>
using namespace std;

vector<vector<int>> threeSum(vector<int>& arr) {
    sort(arr.begin(), arr.end());
    vector<vector<int>> result;
    
    for (int i = 0; i < arr.size() - 2; i++) {
        // Skip duplicates for first number
        if (i > 0 && arr[i] == arr[i - 1]) {
            continue;
        }
        
        // Two pointers for remaining two numbers
        int left = i + 1, right = arr.size() - 1;
        int target = -arr[i];
        
        while (left < right) {
            int current_sum = arr[left] + arr[right];
            
            if (current_sum == target) {
                result.push_back({arr[i], arr[left], arr[right]});
                
                // Skip duplicates
                while (left < right && arr[left] == arr[left + 1]) {
                    left++;
                }
                while (left < right && arr[right] == arr[right - 1]) {
                    right--;
                }
                
                left++;
                right--;
            } else if (current_sum < target) {
                left++;
            } else {
                right--;
            }
        }
    }
    
    return result;
}

// Test
int main() {
    vector<int> arr1 = {-1, 0, 1, 2, -1, -4};
    vector<vector<int>> result1 = threeSum(arr1);  // [[-1, -1, 2], [-1, 0, 1]]
    
    vector<int> arr2 = {0, 0, 0};
    vector<vector<int>> result2 = threeSum(arr2);  // [[0, 0, 0]]
    
    return 0;
}
```

**Key insight**: Sort, fix first number, use two pointers for the other two.

---

 Solution 10: Fruits Into Baskets

**Pattern**: Sliding Window (Dynamic)  
**Time**: O(n) | **Space**: O(1) - at most 2 fruit types

**Why this pattern?**
- Contiguous elements ✓
- "Maximum" with constraint ✓
- At most 2 distinct types ✓

```cpp
include <vector>
include <unordered_map>
include <algorithm>
using namespace std;

int totalFruits(vector<int>& fruits) {
    unordered_map<int, int> fruit_count;
    int window_start = 0;
    int max_fruits = 0;
    
    for (int window_end = 0; window_end < fruits.size(); window_end++) {
        int right_fruit = fruits[window_end];
        fruit_count[right_fruit]++;
        
        // Shrink if more than 2 types
        while (fruit_count.size() > 2) {
            int left_fruit = fruits[window_start];
            fruit_count[left_fruit]--;
            if (fruit_count[left_fruit] == 0) {
                fruit_count.erase(left_fruit);
            }
            window_start++;
        }
        
        max_fruits = max(max_fruits, window_end - window_start + 1);
    }
    
    return max_fruits;
}

// Test
int main() {
    vector<int> fruits1 = {1, 2, 1};
    cout << totalFruits(fruits1);  // Output: 3
    
    vector<int> fruits2 = {0, 1, 2, 2};
    cout << totalFruits(fruits2);  // Output: 3
    
    vector<int> fruits3 = {1, 2, 3, 2, 2};
    cout << totalFruits(fruits3);  // Output: 4
    
    return 0;
}
```

**Key insight**: This is "longest subarray with at most 2 distinct elements".

---

 Pattern Summary

| Problem | Pattern | Key Technique |
|---------|---------|---------------|
| 1. Pair Sum | Two Pointers | Move based on sum comparison |
| 2. Max Sum Subarray | Sliding Window | Add new, remove old |
| 3. Middle of List | Fast & Slow | 2x speed difference |
| 4. K Distinct Chars | Sliding Window | HashMap tracking |
| 5. Sorted Squares | Two Pointers | Compare from ends |
| 6. Find Anagrams | Sliding Window | Frequency matching |
| 7. Cycle Detection | Fast & Slow | Will meet if cycle |
| 8. Min Window | Sliding Window | Shrink when valid |
| 9. Three Sum | Two Pointers | Fix one + two pointers |
| 10. Fruits Baskets | Sliding Window | At most 2 distinct |

---

 What You Learned

✅ **Pattern Recognition**: Keywords → Pattern mapping  
✅ **Template Application**: Using the right template  
✅ **Problem Solving**: Breaking down complex problems  
✅ **Optimization**: Reducing time complexity  
✅ **C++ STL**: Using vectors, maps, sets efficiently

---

 C++ Key Takeaways

**Common Headers**:
```cpp
include <vector>           // Dynamic arrays
include <unordered_map>    // Hash maps
include <unordered_set>    // Hash sets
include <algorithm>        // sort, max, min
include <climits>          // INT_MAX, INT_MIN
include <queue>            // BFS, heaps
```

**Common Patterns**:
```cpp
// Vector initialization
vector<int> arr = {1, 2, 3};
vector<int> result(n, 0);  // n zeros

// HashMap operations
unordered_map<char, int> freq;
freq[key]++;
if (freq.count(key)) { }
freq.erase(key);

// Two pointers
int left = 0, right = arr.size() - 1;

// Range-based for loop
for (int num : arr) { }
for (auto& pair : map) { }
```

---

 Next Steps

1. **Solve these again** without looking at solutions
2. **Time yourself** - aim for 15-20 minutes each
3. **Add edge case tests** - empty input, single element, duplicates
4. **Move to LeetCode** - Practice with similar patterns:
   - Easy: 2-3 problems per pattern
   - Medium: 5-7 problems per pattern
   - Hard: 2-3 problems per pattern

5. **Mix patterns together** for complex problems

---

 Bonus: Quick Testing Template

```cpp
include <iostream>
include <vector>
include <cassert>
using namespace std;

// Your solution function here

void test() {
    // Test case 1
    vector<int> input1 = {1, 2, 3};
    int expected1 = 6;
    assert(yourFunction(input1) == expected1);
    cout << "Test 1 passed!" << endl;
    
    // Add more test cases
}

int main() {
    test();
    cout << "All tests passed!" << endl;
    return 0;
}
```

Keep practicing! 🚀
