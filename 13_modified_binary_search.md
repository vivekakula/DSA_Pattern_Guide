# Modified Binary Search Pattern 🎯

## The Big Idea
Apply **binary search** to problems that don't look like traditional search, but have a **monotonic property** (if condition is true at X, it's true for all values > X or < X).

**Why it works**: Binary search doesn't need a sorted array - it needs a search space where you can eliminate half based on a condition.

---

 When to Use
- **Search space** has monotonic property
- **Minimize/maximize** something
- Find **boundary** or **threshold**
- Problem says "at least", "at most"

**Keywords to spot**:
- "Minimize the maximum"
- "Maximize the minimum"
- "At least X"
- "Can we do it with K?"
- "Split array", "allocate resources"

---

 The Template

```cpp
int binary_search_on_answer(vector<int>& arr, int target) {
    int left = min_possible_answer;
    int right = max_possible_answer;
    int result = -1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (is_feasible(arr, mid, target)) {
            result = mid;
            // Minimize: search left
            // Maximize: search right
            right = mid - 1;  // or left = mid + 1
        } else {
            left = mid + 1;   // or right = mid - 1
        }
    }
    
    return result;
}
```

---

 Example 1: Find in Rotated Sorted Array
**Problem**: Search in rotated sorted array.

```cpp
int search(vector<int>& nums, int target) {
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
vector<int> nums = {4,5,6,7,0,1,2};
search(nums, 0);  // Output: 4
```

---

 Example 2: Capacity To Ship Packages
**Problem**: Find minimum capacity to ship all packages within D days.

```cpp
bool can_ship(vector<int>& weights, int capacity, int days) {
    int days_needed = 1;
    int current_load = 0;
    
    for (int weight : weights) {
        if (current_load + weight > capacity) {
            days_needed++;
            current_load = weight;
        } else {
            current_load += weight;
        }
    }
    
    return days_needed <= days;
}

int ship_within_days(vector<int>& weights, int days) {
    int left = *max_element(weights.begin(), weights.end());  // Min capacity
    int right = accumulate(weights.begin(), weights.end(), 0);  // Max capacity
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        if (can_ship(weights, mid, days)) {
            right = mid;  // Try smaller capacity
        } else {
            left = mid + 1;
        }
    }
    
    return left;
}

// Example
vector<int> weights = {1,2,3,4,5,6,7,8,9,10};
int days = 5;
// Output: 15
```

---

 Example 3: Split Array Largest Sum
**Problem**: Split array into M subarrays to minimize the largest sum.

```cpp
bool can_split(vector<int>& nums, int m, int max_sum) {
    int subarrays = 1;
    int current_sum = 0;
    
    for (int num : nums) {
        if (current_sum + num > max_sum) {
            subarrays++;
            current_sum = num;
            
            if (subarrays > m) {
                return false;
            }
        } else {
            current_sum += num;
        }
    }
    
    return true;
}

int split_array(vector<int>& nums, int m) {
    int left = *max_element(nums.begin(), nums.end());
    int right = accumulate(nums.begin(), nums.end(), 0);
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        if (can_split(nums, m, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    
    return left;
}

// Example
vector<int> nums = {7,2,5,10,8};
int m = 2;
// Output: 18 (split: [7,2,5] and [10,8])
```

---

 Example 4: Koko Eating Bananas
**Problem**: Find minimum eating speed to finish all bananas within H hours.

```cpp
bool can_finish(vector<int>& piles, int speed, int h) {
    int hours = 0;
    
    for (int pile : piles) {
        hours += (pile + speed - 1) / speed;  // Ceiling division
        if (hours > h) {
            return false;
        }
    }
    
    return true;
}

int min_eating_speed(vector<int>& piles, int h) {
    int left = 1;
    int right = *max_element(piles.begin(), piles.end());
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        if (can_finish(piles, mid, h)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    
    return left;
}

// Example
vector<int> piles = {3,6,7,11};
int h = 8;
// Output: 4
```

---

 Example 5: Minimum Time to Complete Trips
**Problem**: Find minimum time for buses to complete given number of trips.

```cpp
bool can_complete(vector<int>& time, int total_trips, long long given_time) {
    long long trips = 0;
    
    for (int t : time) {
        trips += given_time / t;
        if (trips >= total_trips) {
            return true;
        }
    }
    
    return false;
}

long long minimum_time(vector<int>& time, int total_trips) {
    long long left = 1;
    long long right = (long long)*min_element(time.begin(), time.end()) * total_trips;
    
    while (left < right) {
        long long mid = left + (right - left) / 2;
        
        if (can_complete(time, total_trips, mid)) {
            right = mid;
        } else {
            left = mid + 1;
        }
    }
    
    return left;
}

// Example
vector<int> time = {1,2,3};
int total_trips = 5;
// Output: 3
```

---

 Example 6: Magnetic Force Between Balls
**Problem**: Place M balls in N positions to maximize minimum magnetic force.

```cpp
bool can_place(vector<int>& position, int m, int min_force) {
    int count = 1;
    int last_pos = position[0];
    
    for (int i = 1; i < position.size(); i++) {
        if (position[i] - last_pos >= min_force) {
            count++;
            last_pos = position[i];
            
            if (count == m) {
                return true;
            }
        }
    }
    
    return false;
}

int max_distance(vector<int>& position, int m) {
    sort(position.begin(), position.end());
    
    int left = 1;
    int right = position.back() - position[0];
    int result = 0;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (can_place(position, m, mid)) {
            result = mid;
            left = mid + 1;  // Try larger distance
        } else {
            right = mid - 1;
        }
    }
    
    return result;
}

// Example
vector<int> position = {1,2,3,4,7};
int m = 3;
// Output: 3 (place at positions 1, 4, 7)
```

---

 Example 7: Minimum in Rotated Sorted Array
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
vector<int> nums = {4,5,6,7,0,1,2};
// Output: 0
```

---

 Example 8: Find Peak Element
**Problem**: Find a peak element (greater than neighbors).

```cpp
int find_peak_element(vector<int>& nums) {
    int left = 0, right = nums.size() - 1;
    
    while (left < right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] > nums[mid + 1]) {
            // Peak is on left or mid is peak
            right = mid;
        } else {
            // Peak is on right
            left = mid + 1;
        }
    }
    
    return left;
}

// Example
vector<int> nums = {1,2,3,1};
// Output: 2 (index of peak element 3)
```

---

 Time & Space Complexity
- **Time**: O(n log(max - min))
  - n for feasibility check
  - log(max - min) for binary search iterations
  
- **Space**: O(1)

---

 Pattern Recognition

Use modified binary search when:
1. **Minimize maximum** or **maximize minimum**
2. Answer has **monotonic** property
3. Can write `is_feasible(answer)` function
4. Search space is **numeric range** (not necessarily array)

---

 Common Problem Types

 1. Resource Allocation
- Ship packages
- Split array
- Allocate books

 2. Time Optimization
- Minimum time
- Eating speed
- Complete trips

 3. Distance/Force
- Magnetic force
- Aggressive cows
- Place items

---

 Tips & Tricks

1. **Define search space**: Find min and max possible answers
2. **Feasibility function**: Can we achieve this answer?
3. **Monotonic property**: If feasible at X, is it feasible at X+1?
4. **Minimize vs Maximize**:
   - Minimize: search left when feasible
   - Maximize: search right when feasible
5. **Edge cases**: Single element, all same values

---

 Template Variations

 Minimize Maximum
```cpp
while (left < right) {
    int mid = left + (right - left) / 2;
    if (is_feasible(mid)) {
        right = mid;  // Try smaller
    } else {
        left = mid + 1;
    }
}
```

 Maximize Minimum
```cpp
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (is_feasible(mid)) {
        result = mid;
        left = mid + 1;  // Try larger
    } else {
        right = mid - 1;
    }
}
```

---

 Practice Problems

1. **Medium**: Capacity To Ship Packages Within D Days (LeetCode 1011)
2. **Hard**: Split Array Largest Sum (LeetCode 410)
3. **Medium**: Koko Eating Bananas (LeetCode 875)
4. **Medium**: Minimum Time to Complete Trips (LeetCode 2187)
5. **Hard**: Magnetic Force Between Two Balls (LeetCode 1552)
6. **Medium**: Find Minimum in Rotated Sorted Array (LeetCode 153)
7. **Medium**: Find Peak Element (LeetCode 162)
8. **Hard**: Median of Two Sorted Arrays (LeetCode 4)
9. **Medium**: Search in Rotated Sorted Array (LeetCode 33)

---

 Key Takeaways
- ✅ Binary search on **answer space**, not array
- ✅ Need **monotonic** property
- ✅ Write `is_feasible(answer)` function
- ✅ Minimize: search left when feasible
- ✅ Maximize: search right when feasible
- ✅ O(n log(range)) complexity
