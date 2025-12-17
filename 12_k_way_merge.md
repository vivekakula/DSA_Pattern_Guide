# K-way Merge Pattern 🔀

## The Big Idea
Merge K sorted arrays/lists efficiently using a **min heap**. The heap always gives us the next smallest element across all arrays.

**Why it works**: Min heap of size K tracks smallest unprocessed element from each array. Extract min, add next from same array.

---

 When to Use
- Merge **K sorted** arrays/lists
- Find **smallest range** covering elements from K lists
- **Kth smallest** in multiple sorted arrays

**Keywords to spot**:
- "Merge K sorted lists"
- "K sorted arrays"
- "Smallest range"
- "Kth smallest in sorted matrix"

---

 The Template

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* merge_k_lists(vector<ListNode*>& lists) {
    // Min heap with custom comparator
    auto cmp = [](ListNode* a, ListNode* b) {
        return a->val > b->val;
    };
    priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> min_heap(cmp);
    
    // Add first node of each list
    for (auto list : lists) {
        if (list) {
            min_heap.push(list);
        }
    }
    
    ListNode* dummy = new ListNode(0);
    ListNode* tail = dummy;
    
    while (!min_heap.empty()) {
        ListNode* node = min_heap.top();
        min_heap.pop();
        
        tail->next = node;
        tail = tail->next;
        
        if (node->next) {
            min_heap.push(node->next);
        }
    }
    
    return dummy->next;
}
```

---

 Example 1: Merge K Sorted Lists
**Problem**: Merge K sorted linked lists into one sorted list.

```cpp
ListNode* merge_k_lists(vector<ListNode*>& lists) {
    auto cmp = [](ListNode* a, ListNode* b) {
        return a->val > b->val;
    };
    priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> min_heap(cmp);
    
    // Add first node from each list
    for (auto list : lists) {
        if (list) {
            min_heap.push(list);
        }
    }
    
    ListNode* dummy = new ListNode(0);
    ListNode* tail = dummy;
    
    while (!min_heap.empty()) {
        ListNode* smallest = min_heap.top();
        min_heap.pop();
        
        tail->next = smallest;
        tail = tail->next;
        
        if (smallest->next) {
            min_heap.push(smallest->next);
        }
    }
    
    return dummy->next;
}

// Example
// Input: [[1,4,5], [1,3,4], [2,6]]
// Output: [1,1,2,3,4,4,5,6]
```

**Visual**:
```
Lists: 1→4→5
       1→3→4
       2→6

Heap: [1, 1, 2]  → Take 1 (from list 1)
Heap: [1, 2, 4]  → Take 1 (from list 2)
Heap: [2, 3, 4]  → Take 2
Heap: [3, 4, 6]  → Take 3
...
```

---

 Example 2: Merge K Sorted Arrays
**Problem**: Merge K sorted arrays into one sorted array.

```cpp
vector<int> merge_k_arrays(vector<vector<int>>& arrays) {
    // Min heap: {value, array_index, element_index}
    auto cmp = [](vector<int>& a, vector<int>& b) {
        return a[0] > b[0];
    };
    priority_queue<vector<int>, vector<vector<int>>, decltype(cmp)> min_heap(cmp);
    
    // Add first element from each array
    for (int i = 0; i < arrays.size(); i++) {
        if (!arrays[i].empty()) {
            min_heap.push({arrays[i][0], i, 0});
        }
    }
    
    vector<int> result;
    
    while (!min_heap.empty()) {
        auto top = min_heap.top();
        min_heap.pop();
        
        int value = top[0];
        int array_idx = top[1];
        int elem_idx = top[2];
        
        result.push_back(value);
        
        // Add next element from same array
        if (elem_idx + 1 < arrays[array_idx].size()) {
            min_heap.push({
                arrays[array_idx][elem_idx + 1],
                array_idx,
                elem_idx + 1
            });
        }
    }
    
    return result;
}

// Example
vector<vector<int>> arrays = {{1, 4, 7}, {2, 5, 8}, {3, 6, 9}};
// Output: [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

---

 Example 3: Kth Smallest in M Sorted Arrays
**Problem**: Find Kth smallest element across M sorted arrays.

```cpp
int kth_smallest_in_m_arrays(vector<vector<int>>& arrays, int k) {
    // Min heap: {value, array_index, element_index}
    auto cmp = [](vector<int>& a, vector<int>& b) {
        return a[0] > b[0];
    };
    priority_queue<vector<int>, vector<vector<int>>, decltype(cmp)> min_heap(cmp);
    
    // Add first element from each array
    for (int i = 0; i < arrays.size(); i++) {
        if (!arrays[i].empty()) {
            min_heap.push({arrays[i][0], i, 0});
        }
    }
    
    int count = 0;
    int result = 0;
    
    while (!min_heap.empty()) {
        auto top = min_heap.top();
        min_heap.pop();
        
        result = top[0];
        count++;
        
        if (count == k) {
            return result;
        }
        
        int array_idx = top[1];
        int elem_idx = top[2];
        
        if (elem_idx + 1 < arrays[array_idx].size()) {
            min_heap.push({
                arrays[array_idx][elem_idx + 1],
                array_idx,
                elem_idx + 1
            });
        }
    }
    
    return result;
}

// Example
vector<vector<int>> arrays = {{2, 6, 8}, {3, 6, 7}, {1, 3, 4}};
// K = 5, Output: 4
```

---

 Example 4: Smallest Range Covering K Lists
**Problem**: Find smallest range that includes at least one number from each K list.

```cpp
vector<int> smallest_range(vector<vector<int>>& nums) {
    // Min heap: {value, list_index, element_index}
    auto cmp = [](vector<int>& a, vector<int>& b) {
        return a[0] > b[0];
    };
    priority_queue<vector<int>, vector<vector<int>>, decltype(cmp)> min_heap(cmp);
    
    int current_max = INT_MIN;
    
    // Add first element from each list
    for (int i = 0; i < nums.size(); i++) {
        min_heap.push({nums[i][0], i, 0});
        current_max = max(current_max, nums[i][0]);
    }
    
    int range_start = 0, range_end = INT_MAX;
    
    while (min_heap.size() == nums.size()) {
        auto top = min_heap.top();
        min_heap.pop();
        
        int min_val = top[0];
        int list_idx = top[1];
        int elem_idx = top[2];
        
        // Update range if smaller
        if (range_end - range_start > current_max - min_val) {
            range_start = min_val;
            range_end = current_max;
        }
        
        // Add next element from same list
        if (elem_idx + 1 < nums[list_idx].size()) {
            int next_val = nums[list_idx][elem_idx + 1];
            min_heap.push({next_val, list_idx, elem_idx + 1});
            current_max = max(current_max, next_val);
        }
    }
    
    return {range_start, range_end};
}

// Example
vector<vector<int>> nums = {{4,10,15,24,26}, {0,9,12,20}, {5,18,22,30}};
// Output: [20, 24] (contains 20 from list 2, 22 from list 3, 24 from list 1)
```

---

 Example 5: Kth Smallest in Sorted Matrix
**Problem**: Find Kth smallest element in row and column sorted matrix.

```cpp
int kth_smallest(vector<vector<int>>& matrix, int k) {
    int n = matrix.size();
    
    // Min heap: {value, row, col}
    auto cmp = [](vector<int>& a, vector<int>& b) {
        return a[0] > b[0];
    };
    priority_queue<vector<int>, vector<vector<int>>, decltype(cmp)> min_heap(cmp);
    
    // Add first element of each row
    for (int i = 0; i < min(n, k); i++) {
        min_heap.push({matrix[i][0], i, 0});
    }
    
    int result = 0;
    
    while (k-- > 0) {
        auto top = min_heap.top();
        min_heap.pop();
        
        result = top[0];
        int row = top[1];
        int col = top[2];
        
        if (col + 1 < n) {
            min_heap.push({matrix[row][col + 1], row, col + 1});
        }
    }
    
    return result;
}

// Example
// [[1,  5,  9],
//  [10, 11, 13],
//  [12, 13, 15]]
// K = 8, Output: 13
```

---

 Example 6: Median of Two Sorted Arrays
**Problem**: Find median of two sorted arrays (can be solved with K-way merge concept).

```cpp
double find_median_sorted_arrays(vector<int>& nums1, vector<int>& nums2) {
    int total = nums1.size() + nums2.size();
    
    if (total % 2 == 1) {
        return find_kth_element(nums1, nums2, total / 2);
    } else {
        return (find_kth_element(nums1, nums2, total / 2 - 1) +
                find_kth_element(nums1, nums2, total / 2)) / 2.0;
    }
}

double find_kth_element(vector<int>& nums1, vector<int>& nums2, int k) {
    int i = 0, j = 0;
    
    while (k > 0) {
        if (i >= nums1.size()) return nums2[j + k];
        if (j >= nums2.size()) return nums1[i + k];
        
        if (nums1[i] < nums2[j]) {
            if (k == 0) return nums1[i];
            i++;
        } else {
            if (k == 0) return nums2[j];
            j++;
        }
        k--;
    }
    
    return i < nums1.size() ? nums1[i] : nums2[j];
}
```

---

 Time & Space Complexity
- **Time**: O(N log K)
  - N = total elements across all arrays
  - K = number of arrays
  - Each of N operations involves heap operation (log K)
  
- **Space**: O(K) - heap size

Comparison:
- Naive merge: O(N * K)
- K-way merge: O(N log K)

---

 Pattern Recognition

Use K-way merge when:
1. Multiple **sorted** sequences
2. Need to **merge** or find **smallest/largest**
3. Can't sort everything together (too large or streaming)

---

 Common Variations

 Track indices
```cpp
// {value, source_array_idx, element_idx}
min_heap.push({arr[i][j], i, j});
```

 Track max for range
```cpp
int current_max = INT_MIN;
// Update max when adding to heap
current_max = max(current_max, new_value);
```

 Stop early for Kth element
```cpp
while (k-- > 0) {
    // ... process
}
return result;
```

---

 Tips & Tricks

1. **Min heap**: Always use min heap for K-way merge
2. **Track indices**: Store {value, array_idx, element_idx}
3. **Initialize**: Add first element from each array
4. **Update**: Add next element from same array after popping
5. **Check bounds**: Verify next element exists before adding

---

 Heap Element Structure

```cpp
// For arrays:
struct Element {
    int value;
    int array_index;
    int element_index;
};

// For linked lists:
struct ListNode {
    int val;
    ListNode* next;
};
// Heap stores ListNode*
```

---

 Practice Problems

1. **Hard**: Merge k Sorted Lists (LeetCode 23)
2. **Hard**: Find K Pairs with Smallest Sums (LeetCode 373)
3. **Hard**: Smallest Range Covering Elements from K Lists (LeetCode 632)
4. **Medium**: Kth Smallest Element in Sorted Matrix (LeetCode 378)
5. **Hard**: Median of Two Sorted Arrays (LeetCode 4)
6. **Medium**: Merge Sorted Array (LeetCode 88)
7. **Hard**: Merge K Sorted Arrays (Educational)

---

 Key Takeaways
- ✅ Use min heap of size K
- ✅ Store {value, array_idx, element_idx} in heap
- ✅ Add first element from each array initially
- ✅ After popping, add next from same array
- ✅ O(N log K) time complexity
- ✅ Perfect for merging multiple sorted sources
