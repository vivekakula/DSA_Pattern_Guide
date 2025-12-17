# Two Pointers Pattern 👉👈

## The Big Idea
Instead of using nested loops (checking every pair), use two pointers moving smartly through the array.

**Why it works**: By moving pointers based on conditions, we avoid unnecessary comparisons.

---

 When to Use
- Array or string is **sorted** (or can be sorted)
- Need to find **pairs, triplets** that satisfy a condition
- Need to **compare elements** from both ends
- **Remove duplicates** or partition

**Keywords to spot**: 
- "Find pair that sums to..."
- "Remove duplicates"
- "Is palindrome?"
- "Triplet sum"
- "Container with most water"

---

 The Template

```cpp
vector<int> two_pointers(vector<int>& arr) {
    int left = 0;
    int right = arr.size() - 1;
    
    while (left < right) {
        // Calculate something with arr[left] and arr[right]
        
        if (condition_met) {
            // Found answer or record it
            return result;
        } else if (need_larger_value) {
            left++;  // Move left pointer right
        } else {
            right--;  // Move right pointer left
        }
    }
    
    return result;
}
```

---

 Example 1: Two Sum (Sorted Array)
**Problem**: Find two numbers that add up to target.

```cpp
vector<int> two_sum_sorted(vector<int>& arr, int target) {
    int left = 0, right = arr.size() - 1;
    
    while (left < right) {
        int current_sum = arr[left] + arr[right];
        
        if (current_sum == target) {
            return {left, right};  // Found it!
        } else if (current_sum < target) {
            left++;  // Need bigger sum, move left up
        } else {
            right--;  // Sum too big, move right down
        }
    }
    
    return {-1, -1};  // Not found
}

// Example
vector<int> arr = {1, 2, 3, 4, 6};
int target = 6;
vector<int> result = two_sum_sorted(arr, target);  // Output: [1, 3] (2+4=6)
```

**Why it works**: 
- If sum is too small, left pointer moves right (gets bigger numbers)
- If sum is too large, right pointer moves left (gets smaller numbers)
- Each step eliminates possibilities efficiently

---

 Example 2: Remove Duplicates
**Problem**: Remove duplicates from sorted array in-place.

```cpp
int remove_duplicates(vector<int>& arr) {
    if (arr.empty()) {
        return 0;
    }
    
    // Two pointers: 'left' for unique position, 'right' for exploring
    int left = 0;
    
    for (int right = 1; right < arr.size(); right++) {
        if (arr[right] != arr[left]) {
            left++;
            arr[left] = arr[right];
        }
    }
    
    return left + 1;  // Length of unique elements
}

// Example
vector<int> arr = {1, 1, 2, 2, 3, 4, 4};
int length = remove_duplicates(arr);
// First 'length' elements: [1, 2, 3, 4]
```

**Visual walkthrough**:
```
[1, 1, 2, 2, 3, 4, 4]
 L  R                    arr[L] == arr[R], skip
 
[1, 1, 2, 2, 3, 4, 4]
 L     R                 arr[L] != arr[R], move L, copy
 
[1, 2, 2, 2, 3, 4, 4]
    L     R              arr[L] != arr[R], move L, copy
```

---

 Example 3: Valid Palindrome
**Problem**: Check if string is palindrome (ignoring spaces and case).

```cpp
bool is_palindrome(string s) {
    int left = 0, right = s.length() - 1;
    
    while (left < right) {
        // Skip non-alphanumeric
        while (left < right && !isalnum(s[left])) {
            left++;
        }
        while (left < right && !isalnum(s[right])) {
            right--;
        }
        
        // Compare characters
        if (tolower(s[left]) != tolower(s[right])) {
            return false;
        }
        
        left++;
        right--;
    }
    
    return true;
}

// Example
cout << is_palindrome("A man, a plan, a canal: Panama");  // 1 (true)
cout << is_palindrome("race a car");  // 0 (false)
```

---

 Example 4: Three Sum
**Problem**: Find all unique triplets that sum to zero.

```cpp
vector<vector<int>> three_sum(vector<int>& arr) {
    sort(arr.begin(), arr.end());  // Must sort first!
    vector<vector<int>> result;
    
    for (int i = 0; i < arr.size() - 2; i++) {
        // Skip duplicates for first number
        if (i > 0 && arr[i] == arr[i-1]) {
            continue;
        }
        
        // Two pointers for remaining two numbers
        int left = i + 1, right = arr.size() - 1;
        int target = -arr[i];  // We want arr[left] + arr[right] = target
        
        while (left < right) {
            int current_sum = arr[left] + arr[right];
            
            if (current_sum == target) {
                result.push_back({arr[i], arr[left], arr[right]});
                
                // Skip duplicates
                while (left < right && arr[left] == arr[left+1]) {
                    left++;
                }
                while (left < right && arr[right] == arr[right-1]) {
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

// Example
vector<int> arr = {-1, 0, 1, 2, -1, -4};
vector<vector<int>> result = three_sum(arr);  // [[-1, -1, 2], [-1, 0, 1]]
```

**Pattern**: Fix one element, use two pointers for the rest!

---

 Key Insights

 ✅ Advantages
- **Time**: Reduces O(n²) to O(n) for many problems
- **Space**: O(1) - only two variables
- **Simple**: Easy to understand and implement

 🎯 When to Choose This Pattern
1. Array/string is sorted or can be sorted
2. Looking for pairs/triplets with a condition
3. Need to process from both ends
4. Comparing or removing duplicates

 ⚠️ Common Mistakes
1. Forgetting to sort when needed
2. Not handling duplicates properly
3. Wrong pointer movement logic
4. Off-by-one errors with indices

---

 Practice Problems (Easy → Hard)

 Easy
1. **Valid Palindrome** - Check if string is palindrome
2. **Remove Duplicates** - From sorted array
3. **Squares of Sorted Array** - Merge squares from both ends

 Medium
4. **Two Sum II** - In sorted array
5. **3Sum** - Find all triplets summing to zero
6. **Container With Most Water** - Maximize water between lines
7. **Sort Colors** - Dutch flag problem

 Hard
8. **4Sum** - Find all quadruplets
9. **Trapping Rain Water** - Calculate trapped water

---

 Quick Template Reference

```cpp
// Standard two pointers (opposite ends)
int left = 0, right = arr.size() - 1;
while (left < right) {
    if (condition) {
        // process
        left++;
        right--;
    }
}

// Fast-slow pointers (same direction)
int slow = 0;
for (int fast = 0; fast < arr.size(); fast++) {
    if (condition) {
        slow++;
    }
}

// Three pointers (for 3Sum pattern)
for (int i = 0; i < arr.size(); i++) {
    int left = i + 1, right = arr.size() - 1;
    while (left < right) {
        // process triplet
    }
}
```

---

**Next**: Learn `03_sliding_window.md` - Similar but for contiguous subarrays!
