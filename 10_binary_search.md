# Binary Search Pattern 🔍

## The Big Idea
Search in **sorted** space by repeatedly dividing search range in half. Eliminates half of possibilities each step.

**Why it works**: When data is sorted, comparing with middle tells us which half contains the answer.

---

 When to Use
- Array is **sorted** (or rotated sorted)
- Search in **sorted space** (even if implicit)
- Find **first/last** occurrence
- **Minimize/maximize** something with monotonic property

**Keywords to spot**:
- "Sorted array"
- "Find element in O(log n)"
- "First/last occurrence"
- "Search in rotated array"
- "Find peak element"

---

 The Template

```cpp
int binary_search(vector<int>& arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;  // Avoid overflow
        
        if (arr[mid] == target) {
            return mid;  // Found!
        } else if (arr[mid] < target) {
            left = mid + 1;  // Search right half
        } else {
            right = mid - 1;  // Search left half
        }
    }
    
    return -1;  // Not found
}
```

---

 Example 1: Basic Binary Search
**Problem**: Find target in sorted array.

```cpp
int search(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return -1;
}

// Example
vector<int> arr = {1, 3, 5, 7, 9, 11};
search(arr, 7);  // Output: 3
```

**Visual**:
```
[1, 3, 5, 7, 9, 11]  target = 7
 L        M        R
 
Compare mid (5) < 7, search right:
[1, 3, 5, 7, 9, 11]
          L  M   R
          
Compare mid (7) == 7, found!
```

---

 Example 2: First Occurrence
**Problem**: Find first occurrence of target (array may have duplicates).

```cpp
int find_first(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    int result = -1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            result = mid;
            right = mid - 1;  // Continue searching left
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return result;
}

// Example
vector<int> arr = {1, 2, 2, 2, 3, 4};
find_first(arr, 2);  // Output: 1
```

---

 Example 3: Last Occurrence
**Problem**: Find last occurrence of target.

```cpp
int find_last(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    int result = -1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            result = mid;
            left = mid + 1;  // Continue searching right
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return result;
}

// Example
vector<int> arr = {1, 2, 2, 2, 3, 4};
find_last(arr, 2);  // Output: 3
```

---

 Example 4: Search in Rotated Sorted Array
**Problem**: Array was sorted then rotated. Find target.

```cpp
int search_rotated(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] == target) {
            return mid;
        }
        
        // Check which half is sorted
        if (nums[left] <= nums[mid]) {
            // Left half is sorted
            if (target >= nums[left] && target < nums[mid]) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        } else {
            // Right half is sorted
            if (target > nums[mid] && target <= nums[right]) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
    }
    
    return -1;
}

// Example
vector<int> arr = {4, 5, 6, 7, 0, 1, 2};
search_rotated(arr, 0);  // Output: 4
```

---

 Example 5: Find Peak Element
**Problem**: Find any peak element (element greater than neighbors).

```cpp
int find_peak_element(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] > nums[mid + 1]) {
            // Peak is on left side (or mid is peak)
            right = mid;
        } else {
            // Peak is on right side
            left = mid + 1;
        }
    }
    
    return left;
}

// Example
vector<int> arr = {1, 2, 3, 1};
// Output: 2 (element 3 is peak)
```

---

 Example 6: Square Root
**Problem**: Find integer square root (without using sqrt function).

```cpp
int my_sqrt(int x) {
    if (x < 2) return x;
    
    int left = 1, right = x / 2;
    
    while (left <= right) {
        long mid = left + (right - left) / 2;
        long square = mid * mid;
        
        if (square == x) {
            return mid;
        } else if (square < x) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return right;  // Floor value
}

// Example
my_sqrt(8);  // Output: 2 (sqrt(8) ≈ 2.82)
```

---

 Example 7: Search in 2D Matrix
**Problem**: Search in matrix where each row is sorted.

```cpp
bool search_matrix(vector<vector<int>>& matrix, int target) {
    if (matrix.empty()) return false;
    
    int rows = matrix.size();
    int cols = matrix[0].size();
    int left = 0, right = rows * cols - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        int mid_value = matrix[mid / cols][mid % cols];
        
        if (mid_value == target) {
            return true;
        } else if (mid_value < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return false;
}

// Example
// [[1,  3,  5,  7],
//  [10, 11, 16, 20],
//  [23, 30, 34, 60]]
// target = 3, Output: true
```

---

 Example 8: Find Smallest Letter Greater Than Target
**Problem**: Find smallest character that is lexicographically greater than target.

```cpp
char next_greatest_letter(vector<char>& letters, char target) {
    int left = 0, right = letters.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (letters[mid] <= target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return letters[left % letters.size()];  // Wrap around
}

// Example
vector<char> letters = {'c', 'f', 'j'};
next_greatest_letter(letters, 'a');  // Output: 'c'
next_greatest_letter(letters, 'c');  // Output: 'f'
```

---

 Example 9: Find Minimum in Rotated Sorted Array
**Problem**: Find minimum element in rotated sorted array.

```cpp
int find_min(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] > nums[right]) {
            // Minimum is in right half
            left = mid + 1;
        } else {
            // Minimum is in left half or mid
            right = mid;
        }
    }
    
    return nums[left];
}

// Example
vector<int> arr = {4, 5, 6, 7, 0, 1, 2};
// Output: 0
```

---

 Time & Space Complexity
- **Time**: O(log n) - halve search space each iteration
- **Space**: O(1) - only using pointers

Comparison:
- Linear search: O(n)
- Binary search: O(log n)

---

 Common Pitfalls

 1. Infinite Loop
```cpp
// Wrong: Can cause infinite loop
while (left < right) {
    int mid = (left + right) / 2;
    if (condition) {
        left = mid;  // ❌ left never increases when left == mid
    }
}

// Correct:
left = mid + 1;  // ✅
```

 2. Integer Overflow
```cpp
int mid = (left + right) / 2;  // ❌ Can overflow

int mid = left + (right - left) / 2;  // ✅
```

 3. Loop Condition
```cpp
while (left < right)   // Use when you want left == right at end
while (left <= right)  // Use for exact search
```

---

 Binary Search Variants

 Template 1: Exact Match
```cpp
while (left <= right) {
    // ... check arr[mid] == target
    left = mid + 1;
    right = mid - 1;
}
```

 Template 2: Find Boundary
```cpp
while (left < right) {
    // ... move left or right
    // Don't use mid + 1 or mid - 1 on one side
}
```

 Template 3: Find Range
```cpp
// Use Template 1 twice (first and last occurrence)
```

---

 Tips & Tricks

1. **Avoid overflow**: Use `left + (right - left) / 2`
2. **Loop condition**: `left <= right` for exact, `left < right` for boundary
3. **Update pointers**: Always move by at least 1
4. **Sorted check**: Verify array is sorted (or can be treated as sorted)
5. **Edge cases**: Empty array, single element, target not in array

---

 When NOT to Use Binary Search
- Array is **not sorted**
- Need to check **all elements**
- O(n) is acceptable (small input)

---

 Practice Problems

1. **Easy**: Binary Search (LeetCode 704)
2. **Medium**: Find First and Last Position (LeetCode 34)
3. **Medium**: Search in Rotated Sorted Array (LeetCode 33)
4. **Medium**: Find Peak Element (LeetCode 162)
5. **Easy**: Sqrt(x) (LeetCode 69)
6. **Medium**: Search a 2D Matrix (LeetCode 74)
7. **Easy**: Find Smallest Letter Greater Than Target (LeetCode 744)
8. **Medium**: Find Minimum in Rotated Sorted Array (LeetCode 153)
9. **Easy**: Valid Perfect Square (LeetCode 367)
10. **Hard**: Median of Two Sorted Arrays (LeetCode 4)

---

 Key Takeaways
- ✅ Only works on sorted data
- ✅ O(log n) time complexity
- ✅ Avoid overflow: `left + (right - left) / 2`
- ✅ Choose right loop condition
- ✅ Update pointers correctly (avoid infinite loops)
- ✅ Can search in "search space" (not just arrays)
