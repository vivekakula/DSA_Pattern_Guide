# Cyclic Sort Pattern 🔄

## The Big Idea
When array contains numbers in range [1, n], we can place each number at its **correct index** by swapping. This achieves O(n) time with O(1) space!

**Why it works**: Each number knows where it should go: number 1 goes to index 0, number 2 to index 1, etc.

---

 When to Use
- Array contains numbers in a **specific range** (usually [1, n] or [0, n-1])
- Find **missing** or **duplicate** numbers
- Problems mention "containing integers from 1 to n"

**Keywords to spot**:
- "Find missing number"
- "Find duplicate"
- "Array contains numbers from 1 to n"
- "Find all duplicates"
- "First missing positive"

---

 The Template

```cpp
void cyclic_sort(vector<int>& nums) {
    int i = 0;
    
    while (i < nums.size()) {
        int correct_index = nums[i] - 1;  // Where this number should be
        
        if (nums[i] != nums[correct_index]) {
            // Number is not at correct position, swap it
            swap(nums[i], nums[correct_index]);
        } else {
            // Number is at correct position, move to next
            i++;
        }
    }
}
```

---

 Example 1: Sort Array [1 to n]
**Problem**: Sort an array containing numbers from 1 to n.

```cpp
void cyclic_sort(vector<int>& nums) {
    int i = 0;
    
    while (i < nums.size()) {
        int correct_index = nums[i] - 1;
        
        if (nums[i] != nums[correct_index]) {
            swap(nums[i], nums[correct_index]);
        } else {
            i++;
        }
    }
}

// Example
vector<int> arr = {3, 1, 5, 4, 2};
cyclic_sort(arr);
// Output: [1, 2, 3, 4, 5]
```

**Visual walkthrough**:
```
[3, 1, 5, 4, 2]
 i

nums[0] = 3, should be at index 2
Swap arr[0] with arr[2]:
[5, 1, 3, 4, 2]
 i

nums[0] = 5, should be at index 4
Swap arr[0] with arr[4]:
[2, 1, 3, 4, 5]
 i

nums[0] = 2, should be at index 1
Swap arr[0] with arr[1]:
[1, 2, 3, 4, 5]
 i

nums[0] = 1, already at correct position
Move i forward...

Result: [1, 2, 3, 4, 5]
```

---

 Example 2: Find Missing Number
**Problem**: Array contains numbers from 0 to n, one number is missing. Find it.

```cpp
int find_missing_number(vector<int>& nums) {
    int i = 0;
    int n = nums.size();
    
    // Cyclic sort
    while (i < n) {
        int correct_index = nums[i];
        
        if (nums[i] < n && nums[i] != nums[correct_index]) {
            swap(nums[i], nums[correct_index]);
        } else {
            i++;
        }
    }
    
    // Find missing number
    for (int i = 0; i < n; i++) {
        if (nums[i] != i) {
            return i;
        }
    }
    
    return n;  // If all present, n is missing
}

// Example
vector<int> arr = {4, 0, 3, 1};
// Output: 2 (missing number)
```

**Why it works**: 
- After sorting, each number should equal its index
- First index where `nums[i] != i` is the missing number

---

 Example 3: Find All Duplicates
**Problem**: Array of size n contains numbers from 1 to n, some appear twice. Find all duplicates.

```cpp
vector<int> find_all_duplicates(vector<int>& nums) {
    vector<int> duplicates;
    int i = 0;
    
    // Cyclic sort
    while (i < nums.size()) {
        int correct_index = nums[i] - 1;
        
        if (nums[i] != nums[correct_index]) {
            swap(nums[i], nums[correct_index]);
        } else {
            i++;
        }
    }
    
    // Find duplicates
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != i + 1) {
            duplicates.push_back(nums[i]);
        }
    }
    
    return duplicates;
}

// Example
vector<int> arr = {4, 3, 2, 7, 8, 2, 3, 1};
// Output: [2, 3]
```

---

 Example 4: Find the Duplicate Number
**Problem**: Array contains n+1 integers, each between 1 and n. Find the one duplicate.

```cpp
int find_duplicate(vector<int>& nums) {
    int i = 0;
    
    while (i < nums.size()) {
        if (nums[i] != i + 1) {
            int correct_index = nums[i] - 1;
            
            if (nums[i] != nums[correct_index]) {
                swap(nums[i], nums[correct_index]);
            } else {
                // Found duplicate!
                return nums[i];
            }
        } else {
            i++;
        }
    }
    
    return -1;
}

// Example
vector<int> arr = {1, 3, 4, 2, 2};
// Output: 2
```

---

 Example 5: Find All Missing Numbers
**Problem**: Array of size n contains numbers from 1 to n, some numbers appear twice. Find all missing.

```cpp
vector<int> find_missing_numbers(vector<int>& nums) {
    vector<int> missing;
    int i = 0;
    
    // Cyclic sort
    while (i < nums.size()) {
        int correct_index = nums[i] - 1;
        
        if (nums[i] != nums[correct_index]) {
            swap(nums[i], nums[correct_index]);
        } else {
            i++;
        }
    }
    
    // Find missing numbers
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != i + 1) {
            missing.push_back(i + 1);
        }
    }
    
    return missing;
}

// Example
vector<int> arr = {2, 3, 1, 8, 2, 3, 5, 1};
// Output: [4, 6, 7]
```

---

 Example 6: First Missing Positive
**Problem**: Find the smallest missing positive integer.

```cpp
int first_missing_positive(vector<int>& nums) {
    int i = 0;
    int n = nums.size();
    
    // Cyclic sort (only for positive numbers in range)
    while (i < n) {
        int correct_index = nums[i] - 1;
        
        if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[correct_index]) {
            swap(nums[i], nums[correct_index]);
        } else {
            i++;
        }
    }
    
    // Find first missing positive
    for (int i = 0; i < n; i++) {
        if (nums[i] != i + 1) {
            return i + 1;
        }
    }
    
    return n + 1;  // All present, so n+1 is missing
}

// Example
vector<int> arr = {3, 4, -1, 1};
// Output: 2
```

**Visual**:
```
[3, 4, -1, 1]

Cyclic sort (ignore negative and > n):
[1, -1, 3, 4]

Check: nums[1] != 2
Return 2
```

---

 Example 7: Find Corrupt Pair
**Problem**: One number got duplicated (another got lost). Find [duplicate, missing].

```cpp
vector<int> find_corrupt_numbers(vector<int>& nums) {
    int i = 0;
    
    // Cyclic sort
    while (i < nums.size()) {
        int correct_index = nums[i] - 1;
        
        if (nums[i] != nums[correct_index]) {
            swap(nums[i], nums[correct_index]);
        } else {
            i++;
        }
    }
    
    // Find duplicate and missing
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != i + 1) {
            return {nums[i], i + 1};  // [duplicate, missing]
        }
    }
    
    return {-1, -1};
}

// Example
vector<int> arr = {3, 1, 2, 5, 2};
// Output: [2, 4] (2 is duplicate, 4 is missing)
```

---

 Time & Space Complexity
- **Time**: O(n) - each number swapped at most once
- **Space**: O(1) - in-place sorting

This is better than:
- Sorting: O(n log n)
- Hash set: O(n) space

---

 Key Insights

 Why O(n) time?
Each number is swapped at most once to its correct position. Once in place, we never touch it again.

 Why this works?
When numbers are in range [1, n], there's a **one-to-one mapping** between values and indices:
- Value 1 → Index 0
- Value 2 → Index 1
- Value k → Index k-1

 When it doesn't work?
- Numbers outside range [1, n]
- No specific range mentioned
- Need to preserve order

---

 Common Variations

 For range [0, n-1]:
```cpp
int correct_index = nums[i];  // Not nums[i] - 1
```

 For range [1, n]:
```cpp
int correct_index = nums[i] - 1;
```

 Skip out-of-range values:
```cpp
if (nums[i] > 0 && nums[i] <= n && nums[i] != nums[correct_index]) {
    swap(nums[i], nums[correct_index]);
}
```

---

 Tips & Tricks

1. **Check range first**: Works only when numbers in specific range
2. **Calculate correct index**: For [1,n], use `nums[i] - 1`
3. **Don't increment i** after swap - check the swapped value again
4. **Check condition**: `nums[i] != nums[correct_index]` prevents infinite loop
5. **Second pass**: After sorting, iterate to find missing/duplicate

---

 Practice Problems

1. **Easy**: Missing Number (LeetCode 268)
2. **Easy**: Find All Numbers Disappeared in an Array (LeetCode 448)
3. **Medium**: Find All Duplicates in an Array (LeetCode 442)
4. **Medium**: Find the Duplicate Number (LeetCode 287)
5. **Hard**: First Missing Positive (LeetCode 41)
6. **Medium**: Set Mismatch (LeetCode 645)
7. **Easy**: Find Missing Number (Educational - multiple variations)

---

 Key Takeaways
- ✅ Only works when numbers in range [1, n] or [0, n-1]
- ✅ Place each number at correct index by swapping
- ✅ O(n) time, O(1) space - very efficient
- ✅ Don't increment i after swap - check swapped value
- ✅ Second pass to find missing/duplicate
- ✅ Check `nums[i] != nums[correct_index]` to avoid infinite loop
