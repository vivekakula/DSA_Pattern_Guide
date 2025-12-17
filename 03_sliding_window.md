# Sliding Window Pattern 🪟

## The Big Idea
Instead of recalculating from scratch for each subarray, **slide a window** and update incrementally.

Think of it like a window sliding across your array - you remove what's leaving and add what's entering.

---

 When to Use
- Problems about **contiguous** subarrays or substrings
- Need to track something in a **range** that changes

**Keywords to spot**:
- "Maximum/minimum sum of subarray of size k"
- "Longest substring with..."
- "Find all anagrams"
- "Smallest subarray with sum ≥ target"
- "Contiguous", "consecutive", "substring", "subarray"

---

 Two Types of Sliding Window

 Type 1: Fixed Window Size
Window size is constant (given as k)

 Type 2: Dynamic Window Size
Window grows/shrinks based on condition

---

 Template 1: Fixed Window

```cpp
int fixed_window(vector<int>& arr, int k) {
    int window_sum = 0;
    int result = 0;
    
    // Build first window
    for (int i = 0; i < k; i++) {
        window_sum += arr[i];
    }
    
    result = window_sum;
    
    // Slide the window
    for (int i = k; i < arr.size(); i++) {
        window_sum += arr[i];      // Add new element
        window_sum -= arr[i - k];  // Remove old element
        result = max(result, window_sum);
    }
    
    return result;
}
```

---

 Example 1: Maximum Sum Subarray of Size K
**Problem**: Find maximum sum of any subarray of size k.

```cpp
int max_sum_subarray(vector<int>& arr, int k) {
    int max_sum = INT_MIN;
    int window_sum = 0;
    
    for (int i = 0; i < arr.size(); i++) {
        window_sum += arr[i];  // Add next element
        
        // When window hits size k
        if (i >= k - 1) {
            max_sum = max(max_sum, window_sum);
            window_sum -= arr[i - k + 1];  // Remove leftmost
        }
    }
    
    return max_sum;
}

// Example
vector<int> arr = {2, 1, 5, 1, 3, 2};
int k = 3;
cout << max_sum_subarray(arr, k);  // Output: 9 (5+1+3)
```

**Visual**:
```
[2, 1, 5, 1, 3, 2]  k=3
 [2,1,5] = 8
    [1,5,1] = 7
       [5,1,3] = 9  ← Maximum
          [1,3,2] = 6
```

---

 Template 2: Dynamic Window

```cpp
int dynamic_window(vector<int>& arr) {
    int left = 0;
    int result = 0;
    
    for (int right = 0; right < arr.size(); right++) {
        // Add arr[right] to window
        
        // Shrink window while condition violated
        while (condition_violated) {
            // Remove arr[left] from window
            left++;
        }
        
        // Update result with current window
        result = max(result, right - left + 1);
    }
    
    return result;
}
```

---

 Example 2: Longest Substring Without Repeating Characters
**Problem**: Find length of longest substring with all unique characters.

```cpp
int longest_substring_unique(string s) {
    unordered_set<char> char_set;
    int left = 0;
    int max_length = 0;
    
    for (int right = 0; right < s.length(); right++) {
        // Shrink window until no duplicates
        while (char_set.count(s[right])) {
            char_set.erase(s[left]);
            left++;
        }
        
        // Add current character
        char_set.insert(s[right]);
        max_length = max(max_length, right - left + 1);
    }
    
    return max_length;
}

// Example
cout << longest_substring_unique("abcabcbb");  // Output: 3 ("abc")
cout << longest_substring_unique("bbbbb");     // Output: 1 ("b")
cout << longest_substring_unique("pwwkew");    // Output: 3 ("wke")
```

**Visual for "abcabcbb"**:
```
"abcabcbb"
 abc       length=3 ✓
  bca      length=3 ✓
   cab     length=3 ✓
    abc    duplicates! shrink...
```

---

 Example 3: Minimum Window Substring
**Problem**: Find smallest substring containing all characters of target.

```cpp
string min_window(string s, string t) {
    if (s.empty() || t.empty()) {
        return "";
    }
    
    // Count characters needed
    unordered_map<char, int> need;
    for (char c : t) {
        need[c]++;
    }
    
    int left = 0;
    int min_len = INT_MAX;
    int min_start = 0;
    int required = need.size();  // Unique chars needed
    int formed = 0;  // Unique chars matched
    unordered_map<char, int> window_counts;
    
    for (int right = 0; right < s.length(); right++) {
        char c = s[right];
        window_counts[c]++;
        
        // Check if we matched this character's requirement
        if (need.count(c) && window_counts[c] == need[c]) {
            formed++;
        }
        
        // Try to shrink window
        while (formed == required && left <= right) {
            // Update result if smaller
            if (right - left + 1 < min_len) {
                min_len = right - left + 1;
                min_start = left;
            }
            
            // Remove leftmost character
            char leftChar = s[left];
            window_counts[leftChar]--;
            if (need.count(leftChar) && window_counts[leftChar] < need[leftChar]) {
                formed--;
            }
            left++;
        }
    }
    
    return min_len == INT_MAX ? "" : s.substr(min_start, min_len);
}

// Example
cout << min_window("ADOBECODEBANC", "ABC");  // Output: "BANC"
```

---

 Example 4: Fruits Into Baskets (Max 2 Types)
**Problem**: Pick maximum fruits with at most 2 types.

```cpp
int max_fruits(vector<int>& fruits) {
    unordered_map<int, int> fruit_count;
    int left = 0;
    int max_fruits_count = 0;
    
    for (int right = 0; right < fruits.size(); right++) {
        // Add fruit to basket
        fruit_count[fruits[right]]++;
        
        // Shrink if more than 2 types
        while (fruit_count.size() > 2) {
            fruit_count[fruits[left]]--;
            if (fruit_count[fruits[left]] == 0) {
                fruit_count.erase(fruits[left]);
            }
            left++;
        }
        
        max_fruits_count = max(max_fruits_count, right - left + 1);
    }
    
    return max_fruits_count;
}

// Example
vector<int> fruits = {1, 2, 1, 2, 3, 1, 1};
cout << max_fruits(fruits);  // Output: 5 ([2,3,1,1,1])
```

---

 Example 5: Subarray Sum Equals K (with negatives)
**Problem**: Count subarrays with sum equal to k.

```cpp
int subarray_sum_k(vector<int>& arr, int k) {
    // Use prefix sum + hashmap
    int prefix_sum = 0;
    unordered_map<int, int> sum_count;
    sum_count[0] = 1;  // Empty subarray
    int result = 0;
    
    for (int num : arr) {
        prefix_sum += num;
        
        // Check if (prefix_sum - k) exists
        if (sum_count.count(prefix_sum - k)) {
            result += sum_count[prefix_sum - k];
        }
        
        // Add current prefix sum to map
        sum_count[prefix_sum]++;
    }
    
    return result;
}

// Example
vector<int> arr = {1, 2, 3, -3, 1, 1, 1, 4, 2, -3};
int k = 3;
cout << subarray_sum_k(arr, k);  // Output: 8
```

---

 Pattern Variations

 1. Fixed Size Window
```python
 Expand to size k, then slide
for i in range(len(arr)):
    add(arr[i])
    if i >= k - 1:
        compute_result()
        remove(arr[i - k + 1])
```

 2. Dynamic Size (Find Maximum)
```python
 Expand right, shrink left when condition breaks
left = 0
for right in range(len(arr)):
    add(arr[right])
    while invalid:
        remove(arr[left])
        left += 1
    max_result = max(max_result, right - left + 1)
```

 3. Dynamic Size (Find Minimum)
```python
 Expand until valid, then shrink to find minimum
left = 0
for right in range(len(arr)):
    add(arr[right])
    while valid:
        min_result = min(min_result, right - left + 1)
        remove(arr[left])
        left += 1
```

---

 Key Insights

 ✅ When to Use
1. **Contiguous** subarray/substring
2. Keywords: "consecutive", "window", "subarray of size k"
3. Need to optimize from O(n²) to O(n)

 🎯 How to Recognize
- Ask: "Do I need to track something in a contiguous range?"
- If yes → Sliding Window

 💡 Common Tools
- **HashMap/Set**: Track character frequencies
- **Variables**: Track sum, count, etc.
- **Two pointers**: left and right

 ⚠️ Common Mistakes
1. Forgetting to shrink window
2. Not updating window state correctly
3. Off-by-one errors in window size
4. Using when elements can be non-contiguous (use other patterns)

---

 Practice Problems

 Easy
1. **Maximum Sum Subarray of Size K**
2. **Average of Subarrays of Size K**

 Medium
3. **Longest Substring Without Repeating Characters**
4. **Fruits Into Baskets** (max 2 types)
5. **Longest Substring with K Distinct Characters**
6. **Permutation in String** (substring anagram)

 Hard
7. **Minimum Window Substring**
8. **Substring with Concatenation of All Words**
9. **Longest Substring with At Most K Distinct Characters**

---

 Cheat Sheet

```python
 Fixed window template
window = initial_state
for i in range(len(arr)):
    window.add(arr[i])
    if i >= k - 1:
        result = compute(window)
        window.remove(arr[i - k + 1])

 Dynamic window (maximize)
left = 0
for right in range(len(arr)):
    add_to_window(arr[right])
    while invalid:
        remove_from_window(arr[left])
        left += 1
    max_len = max(max_len, right - left + 1)

 Dynamic window (minimize)
left = 0
for right in range(len(arr)):
    add_to_window(arr[right])
    while valid:
        min_len = min(min_len, right - left + 1)
        remove_from_window(arr[left])
        left += 1
```

---

**Next**: Learn `04_fast_slow_pointers.md` for linked list problems!
