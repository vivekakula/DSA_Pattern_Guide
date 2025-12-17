# Top K Elements Pattern 🏆

## The Big Idea
Find top K largest/smallest elements efficiently using a **heap** (priority queue) of size K.

**Why it works**: Heap maintains K elements and removes worst element when size exceeds K. This gives O(n log k) instead of O(n log n).

---

 When to Use
- Find **K largest** or **K smallest** elements
- Find **K most frequent** elements
- Find **K closest** points
- Need **partial sorting** (not full sort)

**Keywords to spot**:
- "K largest/smallest"
- "K most frequent"
- "K closest"
- "Top K"
- "Kth largest"

---

 The Template

```cpp
include <queue>

vector<int> top_k_elements(vector<int>& nums, int k) {
    // Min heap for K largest (keeps smallest of top K at top)
    priority_queue<int, vector<int>, greater<int>> min_heap;
    
    for (int num : nums) {
        min_heap.push(num);
        
        if (min_heap.size() > k) {
            min_heap.pop();  // Remove smallest
        }
    }
    
    vector<int> result;
    while (!min_heap.empty()) {
        result.push_back(min_heap.top());
        min_heap.pop();
    }
    
    return result;
}
```

---

 Heap Basics

 Min Heap (Smallest on top)
```cpp
priority_queue<int, vector<int>, greater<int>> min_heap;
min_heap.push(5);
int min = min_heap.top();  // Smallest element
```

 Max Heap (Largest on top)
```cpp
priority_queue<int> max_heap;  // Default is max heap
max_heap.push(5);
int max = max_heap.top();  // Largest element
```

---

 Example 1: Kth Largest Element
**Problem**: Find Kth largest element in array.

```cpp
int find_kth_largest(vector<int>& nums, int k) {
    // Min heap of size k
    priority_queue<int, vector<int>, greater<int>> min_heap;
    
    for (int num : nums) {
        min_heap.push(num);
        
        if (min_heap.size() > k) {
            min_heap.pop();
        }
    }
    
    return min_heap.top();
}

// Example
vector<int> nums = {3, 2, 1, 5, 6, 4};
find_kth_largest(nums, 2);  // Output: 5
```

**Why min heap for K largest?**
- Keep K largest elements
- Remove smallest when size > k
- Top of min heap is Kth largest!

---

 Example 2: K Largest Elements
**Problem**: Find K largest elements.

```cpp
vector<int> find_k_largest(vector<int>& nums, int k) {
    priority_queue<int, vector<int>, greater<int>> min_heap;
    
    for (int num : nums) {
        min_heap.push(num);
        if (min_heap.size() > k) {
            min_heap.pop();
        }
    }
    
    vector<int> result;
    while (!min_heap.empty()) {
        result.push_back(min_heap.top());
        min_heap.pop();
    }
    
    return result;
}

// Example
vector<int> nums = {1, 5, 12, 2, 11, 5};
// K = 3, Output: [5, 11, 12] (or [12, 11, 5])
```

---

 Example 3: K Most Frequent Elements
**Problem**: Find K most frequent elements.

```cpp
vector<int> top_k_frequent(vector<int>& nums, int k) {
    // Count frequencies
    unordered_map<int, int> freq;
    for (int num : nums) {
        freq[num]++;
    }
    
    // Min heap based on frequency
    auto cmp = [](pair<int, int>& a, pair<int, int>& b) {
        return a.second > b.second;  // Min heap by frequency
    };
    priority_queue<pair<int, int>, vector<pair<int, int>>, decltype(cmp)> min_heap(cmp);
    
    for (auto& [num, count] : freq) {
        min_heap.push({num, count});
        if (min_heap.size() > k) {
            min_heap.pop();
        }
    }
    
    vector<int> result;
    while (!min_heap.empty()) {
        result.push_back(min_heap.top().first);
        min_heap.pop();
    }
    
    return result;
}

// Example
vector<int> nums = {1, 1, 1, 2, 2, 3};
// K = 2, Output: [1, 2]
```

---

 Example 4: K Closest Points to Origin
**Problem**: Find K closest points to (0, 0).

```cpp
vector<vector<int>> k_closest(vector<vector<int>>& points, int k) {
    // Max heap (by distance)
    auto cmp = [](vector<int>& a, vector<int>& b) {
        return a[0]*a[0] + a[1]*a[1] < b[0]*b[0] + b[1]*b[1];
    };
    priority_queue<vector<int>, vector<vector<int>>, decltype(cmp)> max_heap(cmp);
    
    for (auto& point : points) {
        max_heap.push(point);
        if (max_heap.size() > k) {
            max_heap.pop();
        }
    }
    
    vector<vector<int>> result;
    while (!max_heap.empty()) {
        result.push_back(max_heap.top());
        max_heap.pop();
    }
    
    return result;
}

// Example
vector<vector<int>> points = {{1,3}, {-2,2}, {5,8}, {0,1}};
// K = 2, Output: [[0,1], [-2,2]]
```

---

 Example 5: Connect Ropes with Minimum Cost
**Problem**: Connect N ropes with minimum cost (cost = sum of lengths).

```cpp
int minimum_cost_to_connect_ropes(vector<int>& ropes) {
    // Min heap
    priority_queue<int, vector<int>, greater<int>> min_heap(ropes.begin(), ropes.end());
    
    int total_cost = 0;
    
    while (min_heap.size() > 1) {
        int first = min_heap.top();
        min_heap.pop();
        int second = min_heap.top();
        min_heap.pop();
        
        int cost = first + second;
        total_cost += cost;
        min_heap.push(cost);
    }
    
    return total_cost;
}

// Example
vector<int> ropes = {1, 3, 11, 5};
// Output: 33
// Connect 1+3=4, cost=4
// Connect 4+5=9, cost=9
// Connect 9+11=20, cost=20
// Total = 4+9+20 = 33
```

---

 Example 6: K Pairs with Smallest Sums
**Problem**: Find K pairs with smallest sums from two sorted arrays.

```cpp
vector<vector<int>> k_smallest_pairs(vector<int>& nums1, vector<int>& nums2, int k) {
    vector<vector<int>> result;
    if (nums1.empty() || nums2.empty()) return result;
    
    // Min heap: {sum, i, j}
    auto cmp = [&](vector<int>& a, vector<int>& b) {
        return a[0] > b[0];
    };
    priority_queue<vector<int>, vector<vector<int>>, decltype(cmp)> min_heap(cmp);
    
    // Start with pairs from nums1[i] and nums2[0]
    for (int i = 0; i < min(k, (int)nums1.size()); i++) {
        min_heap.push({nums1[i] + nums2[0], i, 0});
    }
    
    while (k-- > 0 && !min_heap.empty()) {
        auto top = min_heap.top();
        min_heap.pop();
        
        int i = top[1], j = top[2];
        result.push_back({nums1[i], nums2[j]});
        
        if (j + 1 < nums2.size()) {
            min_heap.push({nums1[i] + nums2[j+1], i, j+1});
        }
    }
    
    return result;
}
```

---

 Example 7: Frequency Sort
**Problem**: Sort string characters by frequency.

```cpp
string frequency_sort(string s) {
    // Count frequencies
    unordered_map<char, int> freq;
    for (char c : s) {
        freq[c]++;
    }
    
    // Max heap by frequency
    auto cmp = [](pair<char, int>& a, pair<char, int>& b) {
        return a.second < b.second;
    };
    priority_queue<pair<char, int>, vector<pair<char, int>>, decltype(cmp)> max_heap(cmp);
    
    for (auto& p : freq) {
        max_heap.push(p);
    }
    
    string result;
    while (!max_heap.empty()) {
        auto [ch, count] = max_heap.top();
        max_heap.pop();
        result.append(count, ch);
    }
    
    return result;
}

// Example
frequency_sort("tree");  // Output: "eert" or "eetr"
```

---

 Example 8: Kth Smallest in Sorted Matrix
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
        int row = top[1], col = top[2];
        
        if (col + 1 < n) {
            min_heap.push({matrix[row][col+1], row, col+1});
        }
    }
    
    return result;
}
```

---

 Time & Space Complexity
- **Time**: O(n log k) - n elements, heap size k
- **Space**: O(k) - heap size

Comparison:
- Sorting: O(n log n)
- Heap: O(n log k) - better when k << n

---

 Min Heap vs Max Heap

| Problem | Use |
|---------|-----|
| K largest | Min heap |
| K smallest | Max heap |
| K most frequent | Min heap (by frequency) |
| K closest | Max heap (by distance) |

**Rule of thumb**: Use opposite heap to keep K elements!

---

 Custom Comparators

 Lambda Function
```cpp
auto cmp = [](int a, int b) { return a > b; };
priority_queue<int, vector<int>, decltype(cmp)> pq(cmp);
```

 Struct
```cpp
struct Compare {
    bool operator()(int a, int b) {
        return a > b;
    }
};
priority_queue<int, vector<int>, Compare> pq;
```

---

 Tips & Tricks

1. **Opposite heap**: K largest → min heap, K smallest → max heap
2. **Custom comparator**: For complex types (pairs, custom objects)
3. **Heap size**: Maintain size K, remove worst element
4. **Frequency**: Use hash map first, then heap
5. **Multiple arrays**: Process arrays intelligently (don't create all pairs)

---

 Practice Problems

1. **Medium**: Kth Largest Element in Array (LeetCode 215)
2. **Medium**: K Closest Points to Origin (LeetCode 973)
3. **Medium**: Top K Frequent Elements (LeetCode 347)
4. **Easy**: Kth Largest Element in Stream (LeetCode 703)
5. **Medium**: Sort Characters By Frequency (LeetCode 451)
6. **Hard**: Find Median from Data Stream (LeetCode 295)
7. **Medium**: K Closest Points (LeetCode 973)
8. **Hard**: Kth Smallest Element in Sorted Matrix (LeetCode 378)
9. **Easy**: Last Stone Weight (LeetCode 1046)
10. **Medium**: Reorganize String (LeetCode 767)

---

 Key Takeaways
- ✅ Use heap for partial sorting
- ✅ K largest → min heap, K smallest → max heap
- ✅ O(n log k) better than O(n log n) when k << n
- ✅ Maintain heap size of K
- ✅ Custom comparators for complex types
- ✅ Count frequencies first if needed
