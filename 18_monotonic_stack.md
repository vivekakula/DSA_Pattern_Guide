# Monotonic Stack Pattern 📉

## In One Sentence
Keep unresolved items in a stack; when a new item answers their question, pop them and record the answer.

For a next-greater-element problem, each index waits in the stack until a larger value appears to its right. Each index is pushed and popped at most once, so this can be faster than searching separately for every item.

---

## When to Use
- Find **Next Greater Element** to the right or left
- Find **Next Smaller Element**
- Problems about **spans**, **visibility**, **boundaries**
- **Largest rectangle** or **area** problems

**Keywords to spot**:
- "Next greater element"
- "Next smaller element"
- "Daily temperatures"
- "Stock span"
- "Largest rectangle in histogram"
- "Trapping rain water"
- "Visible buildings/people"

---

 Two Types

| Type | Stack Order | Use For |
|------|------------|---------|
| **Monotonic Decreasing** | Top is smallest | Find Next Greater Element |
| **Monotonic Increasing** | Top is largest | Find Next Smaller Element |

---

 The Template: Next Greater Element

```cpp
vector<int> nextGreater(vector<int>& arr) {
    int n = arr.size();
    vector<int> result(n, -1);  // Default: no greater element found
    stack<int> st;              // Stack stores INDICES (not values!)

    for (int i = 0; i < n; i++) {
        // Pop while current element is greater than stack top
        while (!st.empty() && arr[i] > arr[st.top()]) {
            int idx = st.top();
            st.pop();
            result[idx] = arr[i];  // arr[i] is the next greater for idx
        }
        st.push(i);
    }

    return result;
    // Elements still in stack have no next greater element (result stays -1)
}
```

---

 Example 1: Next Greater Element
**Problem**: For each element, find the next greater element to its right (LeetCode 496).

```cpp
vector<int> nextGreaterElement(vector<int>& nums) {
    int n = nums.size();
    vector<int> result(n, -1);
    stack<int> st;  // Monotonic decreasing stack (stores indices)

    for (int i = 0; i < n; i++) {
        while (!st.empty() && nums[i] > nums[st.top()]) {
            result[st.top()] = nums[i];
            st.pop();
        }
        st.push(i);
    }

    return result;
}

// Example: nums = [2, 1, 2, 4, 3]
// Output:         [4, 2, 4,-1,-1]
```

**Step-by-step trace** for `nums = [2, 1, 2, 4, 3]`:

| i | nums[i] | Stack (indices) | Action | result[] |
|---|---------|-----------------|--------|----------|
| 0 | 2 | [] | push 0 | [-1,-1,-1,-1,-1] |
| 1 | 1 | [0] | 1<2, push 1 | [-1,-1,-1,-1,-1] |
| 2 | 2 | [0,1] | 2>1: pop 1, result[1]=2; 2=2: stop, push 2 | [-1,2,-1,-1,-1] |
| 3 | 4 | [0,2] | 4>2: pop 2, result[2]=4; 4>2: pop 0, result[0]=4; push 3 | [4,2,4,-1,-1] |
| 4 | 3 | [3] | 3<4: push 4 | [4,2,4,-1,-1] |
| End | — | [3,4] | Still in stack → result stays -1 | [4,2,4,-1,-1] ✅ |

**Key insight**: Elements still in the stack at the end never found a greater element to their right — they stay -1.

> **Try it yourself**: Change the input to `[4, 3, 2, 1]`. Trace the table. What does this tell you about a fully decreasing array?

---

 Example 2: Daily Temperatures
**Problem**: For each day, how many days until a warmer temperature? (LeetCode 739)

```cpp
vector<int> dailyTemperatures(vector<int>& temperatures) {
    int n = temperatures.size();
    vector<int> result(n, 0);
    stack<int> st;  // Stores indices

    for (int i = 0; i < n; i++) {
        while (!st.empty() && temperatures[i] > temperatures[st.top()]) {
            int idx = st.top();
            st.pop();
            result[idx] = i - idx;  // Distance between current and popped index
        }
        st.push(i);
    }

    return result;
}

// Example: temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
// Output:                  [ 1,  1,  4,  2,  1,  1,  0,  0]
// Day 0 (73°): 1 day wait (day 1 is 74°)
// Day 2 (75°): 4 days wait (day 6 is 76°)
```

**Why `i - idx`?** Index `i` is the warmer day, `idx` is the day that was waiting. The difference is the number of days waited.

---

 Example 3: Largest Rectangle in Histogram ⭐
**Problem**: Find the largest rectangle in a histogram (LeetCode 84). Classic hard problem.

```cpp
int largestRectangleArea(vector<int>& heights) {
    int n = heights.size();
    int max_area = 0;
    stack<int> st;  // Monotonic increasing stack

    for (int i = 0; i <= n; i++) {
        int curr_height = (i == n) ? 0 : heights[i];

        while (!st.empty() && curr_height < heights[st.top()]) {
            int height = heights[st.top()];
            st.pop();
            int width = st.empty() ? i : i - st.top() - 1;
            max_area = max(max_area, height * width);
        }

        st.push(i);
    }

    return max_area;
}

// Example: heights = [2, 1, 5, 6, 2, 3]
// Output: 10  (rectangle of height 5, width 2: bars at index 2 and 3)
```

**Visual**:
```
Heights: [2, 1, 5, 6, 2, 3]

  6
  5 6
  5 6
2 5 6 2 3
2 1 5 6 2 3
─────────────
0 1 2 3 4 5

Largest rectangle: height=5, spans index 2-3, area=10
```

**Why process at `i == n`?** Adding a sentinel height=0 at the end forces ALL remaining elements in the stack to be popped and processed.

---

 Example 4: Trapping Rain Water
**Problem**: How much water can be trapped between bars? (LeetCode 42)

```cpp
int trap(vector<int>& height) {
    int n = height.size();
    int water = 0;
    stack<int> st;

    for (int i = 0; i < n; i++) {
        while (!st.empty() && height[i] > height[st.top()]) {
            int bottom = st.top(); st.pop();
            if (st.empty()) break;

            int left_wall = st.top();
            int width = i - left_wall - 1;
            int bounded_height = min(height[left_wall], height[i]) - height[bottom];
            water += width * bounded_height;
        }
        st.push(i);
    }

    return water;
}

// Example: height = [0,1,0,2,1,0,1,3,2,1,2,1]
// Output: 6
```

**Mental model**: The stack holds "left walls." When a right wall is encountered, the "valley" between left wall and right wall is filled with water.

---

 After Solving, Ask Yourself

For every monotonic stack problem:

1. **Am I looking for next GREATER or next SMALLER?**
   - Greater → decreasing stack (pop when new element is bigger)
   - Smaller → increasing stack (pop when new element is smaller)

2. **Should I store indices or values in the stack?**
   - Almost always **indices** — you need both position AND value.

3. **Does the problem have a "circular" variation?** (e.g., Next Greater in circular array)
   - Solution: traverse the array TWICE (or use modulo).

> **Tutor's rule**: Every monotonic stack problem is a Next Greater/Smaller variant in disguise. Once you can trace Example 1 from memory, every other problem here becomes a modification of that same code.

---

 Practice Problems

 Must-Solve
1. **Easy**: Next Greater Element I (LeetCode 496)
2. **Medium**: Daily Temperatures (LeetCode 739)
3. **Medium**: Online Stock Span (LeetCode 901)
4. **Hard**: Largest Rectangle in Histogram (LeetCode 84)
5. **Hard**: Trapping Rain Water (LeetCode 42)

 Good to Know
6. Next Greater Element II — circular array (LeetCode 503)
7. Sum of Subarray Minimums (LeetCode 907)
8. Remove K Digits (LeetCode 402)

---

 Key Takeaways
- ✅ Stack stores **indices**, not values
- ✅ Pop while the **order is broken** — this is the core operation
- ✅ Elements remaining in stack at end = no answer found for them
- ✅ Decreasing stack → finds Next Greater; Increasing stack → finds Next Smaller
- ⚠️ The "index difference trick" gives distances/widths — commit this to memory
