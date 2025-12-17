# Merge Intervals Pattern 📊

## The Big Idea
When dealing with overlapping ranges or intervals, **sort them first** by start time, then merge overlapping ones.

**Why it works**: Sorting by start time puts overlapping intervals next to each other, making them easy to merge in one pass.

---

 When to Use
- Problems involving **overlapping ranges**
- **Time intervals**, **meeting rooms**, **scheduling**
- **Insert/merge intervals**
- Finding **conflicts** or **gaps**

**Keywords to spot**:
- "Merge overlapping intervals"
- "Insert interval"
- "Meeting rooms"
- "Conflicting appointments"
- "Free time slots"

---

 The Template

```cpp
struct Interval {
    int start;
    int end;
    Interval(int s, int e) : start(s), end(e) {}
};

vector<Interval> merge_intervals(vector<Interval>& intervals) {
    if (intervals.empty()) {
        return {};
    }
    
    // Step 1: Sort by start time
    sort(intervals.begin(), intervals.end(), 
         [](const Interval& a, const Interval& b) {
             return a.start < b.start;
         });
    
    vector<Interval> merged;
    merged.push_back(intervals[0]);
    
    // Step 2: Merge overlapping intervals
    for (int i = 1; i < intervals.size(); i++) {
        Interval& last = merged.back();
        Interval& current = intervals[i];
        
        if (current.start <= last.end) {
            // Overlapping - merge
            last.end = max(last.end, current.end);
        } else {
            // Not overlapping - add as new interval
            merged.push_back(current);
        }
    }
    
    return merged;
}
```

---

 Example 1: Merge Overlapping Intervals
**Problem**: Given intervals, merge all overlapping ones.

```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    if (intervals.empty()) {
        return {};
    }
    
    // Sort by start time
    sort(intervals.begin(), intervals.end());
    
    vector<vector<int>> merged;
    merged.push_back(intervals[0]);
    
    for (int i = 1; i < intervals.size(); i++) {
        vector<int>& last = merged.back();
        vector<int>& current = intervals[i];
        
        if (current[0] <= last[1]) {
            // Overlapping - extend the end
            last[1] = max(last[1], current[1]);
        } else {
            // Not overlapping
            merged.push_back(current);
        }
    }
    
    return merged;
}

// Example
vector<vector<int>> intervals = {{1,3}, {2,6}, {8,10}, {15,18}};
// Output: {{1,6}, {8,10}, {15,18}}
```

**Visual**:
```
Input:
[1,3]   [2,6]      [8,10]    [15,18]
|---|    |---|      |---|      |---|
  |-------|

After sort: [1,3], [2,6], [8,10], [15,18]

Merge [1,3] and [2,6] -> [1,6]
[8,10] doesn't overlap -> keep separate
[15,18] doesn't overlap -> keep separate

Output: [1,6], [8,10], [15,18]
```

---

 Example 2: Insert Interval
**Problem**: Insert a new interval into a sorted list of intervals and merge if needed.

```cpp
vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
    vector<vector<int>> result;
    int i = 0;
    int n = intervals.size();
    
    // Step 1: Add all intervals that come before newInterval
    while (i < n && intervals[i][1] < newInterval[0]) {
        result.push_back(intervals[i]);
        i++;
    }
    
    // Step 2: Merge overlapping intervals
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = min(newInterval[0], intervals[i][0]);
        newInterval[1] = max(newInterval[1], intervals[i][1]);
        i++;
    }
    result.push_back(newInterval);
    
    // Step 3: Add remaining intervals
    while (i < n) {
        result.push_back(intervals[i]);
        i++;
    }
    
    return result;
}

// Example
vector<vector<int>> intervals = {{1,3}, {6,9}};
vector<int> newInterval = {2,5};
// Output: {{1,5}, {6,9}}
```

**Visual**:
```
Existing: [1,3]     [6,9]
New:          [2,5]

[1,3] overlaps with [2,5] -> merge to [1,5]
[6,9] doesn't overlap -> keep separate

Result: [1,5], [6,9]
```

---

 Example 3: Meeting Rooms (Can Attend All?)
**Problem**: Check if a person can attend all meetings.

```cpp
bool can_attend_meetings(vector<vector<int>>& intervals) {
    if (intervals.empty()) {
        return true;
    }
    
    // Sort by start time
    sort(intervals.begin(), intervals.end());
    
    // Check for any overlap
    for (int i = 1; i < intervals.size(); i++) {
        if (intervals[i][0] < intervals[i-1][1]) {
            return false;  // Overlap found!
        }
    }
    
    return true;
}

// Example
vector<vector<int>> meetings1 = {{0,30}, {5,10}, {15,20}};
// Output: false (0-30 overlaps with 5-10)

vector<vector<int>> meetings2 = {{7,10}, {2,4}};
// Output: true (no overlap)
```

---

 Example 4: Meeting Rooms II (Minimum Rooms Needed)
**Problem**: Find minimum number of conference rooms required.

```cpp
int min_meeting_rooms(vector<vector<int>>& intervals) {
    vector<int> start_times;
    vector<int> end_times;
    
    // Separate start and end times
    for (auto& interval : intervals) {
        start_times.push_back(interval[0]);
        end_times.push_back(interval[1]);
    }
    
    // Sort both
    sort(start_times.begin(), start_times.end());
    sort(end_times.begin(), end_times.end());
    
    int rooms_needed = 0;
    int rooms_available = 0;
    int start_ptr = 0, end_ptr = 0;
    
    while (start_ptr < start_times.size()) {
        if (start_times[start_ptr] < end_times[end_ptr]) {
            // Meeting starting, need a room
            rooms_needed++;
            start_ptr++;
        } else {
            // Meeting ending, room becomes available
            rooms_needed--;
            end_ptr++;
        }
        
        rooms_available = max(rooms_available, rooms_needed);
    }
    
    return rooms_available;
}

// Example
vector<vector<int>> meetings = {{0,30}, {5,10}, {15,20}};
// Output: 2 (at time 5, both [0,30] and [5,10] are running)
```

**Visual**:
```
Timeline:
0    5    10   15   20   30
|-----------|
     |---|
          |---|

At time 5: 2 rooms needed
At time 15: 2 rooms needed (one from [0,30])
Maximum: 2 rooms
```

---

 Example 5: Intervals Intersection
**Problem**: Find intersection of two interval lists.

```cpp
vector<vector<int>> interval_intersection(vector<vector<int>>& A, vector<vector<int>>& B) {
    vector<vector<int>> result;
    int i = 0, j = 0;
    
    while (i < A.size() && j < B.size()) {
        // Find intersection
        int start = max(A[i][0], B[j][0]);
        int end = min(A[i][1], B[j][1]);
        
        if (start <= end) {
            result.push_back({start, end});
        }
        
        // Move pointer of interval that ends first
        if (A[i][1] < B[j][1]) {
            i++;
        } else {
            j++;
        }
    }
    
    return result;
}

// Example
vector<vector<int>> A = {{0,2}, {5,10}, {13,23}, {24,25}};
vector<vector<int>> B = {{1,5}, {8,12}, {15,24}, {25,26}};
// Output: {{1,2}, {5,5}, {8,10}, {15,23}, {24,24}, {25,25}}
```

---

 Example 6: Employee Free Time
**Problem**: Find common free time for all employees.

```cpp
struct Interval {
    int start, end;
    Interval(int s, int e) : start(s), end(e) {}
};

vector<Interval> employee_free_time(vector<vector<Interval>>& schedule) {
    vector<Interval> all_intervals;
    
    // Flatten all schedules
    for (auto& emp_schedule : schedule) {
        for (auto& interval : emp_schedule) {
            all_intervals.push_back(interval);
        }
    }
    
    // Sort by start time
    sort(all_intervals.begin(), all_intervals.end(),
         [](const Interval& a, const Interval& b) {
             return a.start < b.start;
         });
    
    // Merge intervals to find busy times
    vector<Interval> busy;
    busy.push_back(all_intervals[0]);
    
    for (int i = 1; i < all_intervals.size(); i++) {
        Interval& last = busy.back();
        Interval& current = all_intervals[i];
        
        if (current.start <= last.end) {
            last.end = max(last.end, current.end);
        } else {
            busy.push_back(current);
        }
    }
    
    // Find gaps between busy times (= free time)
    vector<Interval> free_time;
    for (int i = 1; i < busy.size(); i++) {
        free_time.push_back(Interval(busy[i-1].end, busy[i].start));
    }
    
    return free_time;
}
```

---

 Time & Space Complexity
- **Time**: O(n log n) - sorting dominates
- **Space**: O(n) - for output array

---

 Common Patterns

 1. Check Overlap
```cpp
bool is_overlapping(Interval a, Interval b) {
    return a.start <= b.end && b.start <= a.end;
}
```

 2. Merge Two Intervals
```cpp
Interval merge_two(Interval a, Interval b) {
    return Interval(min(a.start, b.start), max(a.end, b.end));
}
```

 3. Sort Intervals
```cpp
sort(intervals.begin(), intervals.end(),
     [](const Interval& a, const Interval& b) {
         return a.start < b.start;
     });
```

---

 Tips & Tricks

1. **Always sort first** by start time
2. **Check overlap**: `current.start <= last.end`
3. **Merge**: `last.end = max(last.end, current.end)`
4. **Use two pointers** for intersection problems
5. **Separate arrays** for start/end times when counting overlaps

---

 Practice Problems

1. **Medium**: Merge Intervals (LeetCode 56)
2. **Medium**: Insert Interval (LeetCode 57)
3. **Easy**: Meeting Rooms (LeetCode 252)
4. **Medium**: Meeting Rooms II (LeetCode 253)
5. **Medium**: Interval List Intersections (LeetCode 986)
6. **Hard**: Employee Free Time (LeetCode 759)
7. **Medium**: Non-overlapping Intervals (LeetCode 435)
8. **Medium**: Minimum Number of Arrows (LeetCode 452)

---

 Key Takeaways
- ✅ Sort intervals by start time first
- ✅ Merge when `current.start <= last.end`
- ✅ Update end with `max(last.end, current.end)`
- ✅ Use two pointers for intersection
- ✅ Separate start/end arrays for room counting
