# Greedy Pattern 🤑

## The Big Idea
Make **locally optimal choice** at each step, hoping to find global optimum. Choose what looks best right now.

**When it works**: When local optimal leads to global optimal (needs proof!)

**Why it's fast**: Makes one pass, no backtracking. O(n) or O(n log n).

---

 When to Use
- **Optimization** problem (max/min)
- **Greedy choice property**: Local optimal → global optimal
- Can **prove** greedy works
- Problem has **optimal substructure**

**Keywords to spot**:
- "Minimum/maximum"
- "Optimize"
- "Activity selection"
- "Interval scheduling"
- "Jump game"

---

 The Template

```cpp
int greedy_solution(vector<int>& input) {
    // Step 1: Sort (if needed)
    sort(input.begin(), input.end());
    
    int result = 0;
    
    // Step 2: Make greedy choice at each step
    for (int i = 0; i < input.size(); i++) {
        if (greedy_condition) {
            // Make choice
            result += input[i];
            // Update state
        }
    }
    
    return result;
}
```

---

 Example 1: Activity Selection
**Problem**: Maximum number of non-overlapping activities.

```cpp
int max_activities(vector<vector<int>>& activities) {
    // Sort by end time
    sort(activities.begin(), activities.end(), 
         [](vector<int>& a, vector<int>& b) {
             return a[1] < b[1];
         });
    
    int count = 1;
    int last_end = activities[0][1];
    
    for (int i = 1; i < activities.size(); i++) {
        if (activities[i][0] >= last_end) {
            count++;
            last_end = activities[i][1];
        }
    }
    
    return count;
}

// Example
vector<vector<int>> activities = {{1,3}, {2,4}, {3,5}, {0,6}, {5,7}};
// Select: {1,3}, {3,5}, {5,7}
// Output: 3
```

**Why greedy works**: Choosing earliest ending activity leaves maximum time for others.

---

 Example 2: Jump Game
**Problem**: Can you reach last index? Each element is max jump length.

```cpp
bool can_jump(vector<int>& nums) {
    int max_reach = 0;
    
    for (int i = 0; i < nums.size(); i++) {
        if (i > max_reach) {
            return false;  // Can't reach this position
        }
        
        max_reach = max(max_reach, i + nums[i]);
        
        if (max_reach >= nums.size() - 1) {
            return true;
        }
    }
    
    return false;
}

// Example
vector<int> nums = {2, 3, 1, 1, 4};
// Jump path: 0 -> 1 -> 4
// Output: true
```

---

 Example 3: Minimum Jumps
**Problem**: Minimum jumps to reach last index.

```cpp
int min_jumps(vector<int>& nums) {
    int jumps = 0;
    int current_end = 0;
    int farthest = 0;
    
    for (int i = 0; i < nums.size() - 1; i++) {
        farthest = max(farthest, i + nums[i]);
        
        if (i == current_end) {
            jumps++;
            current_end = farthest;
            
            if (current_end >= nums.size() - 1) {
                break;
            }
        }
    }
    
    return jumps;
}

// Example
vector<int> nums = {2, 3, 1, 1, 4};
// Output: 2 (0 -> 1 -> 4)
```

---

 Example 4: Gas Station
**Problem**: Find starting gas station to complete circular route.

```cpp
int can_complete_circuit(vector<int>& gas, vector<int>& cost) {
    int total_tank = 0;
    int current_tank = 0;
    int start = 0;
    
    for (int i = 0; i < gas.size(); i++) {
        total_tank += gas[i] - cost[i];
        current_tank += gas[i] - cost[i];
        
        if (current_tank < 0) {
            // Can't start from any station before i
            start = i + 1;
            current_tank = 0;
        }
    }
    
    return total_tank >= 0 ? start : -1;
}

// Example
vector<int> gas = {1, 2, 3, 4, 5};
vector<int> cost = {3, 4, 5, 1, 2};
// Start at index 3
// Output: 3
```

**Why greedy works**: If we can't reach station j from i, we can't reach j from any station between i and j.

---

 Example 5: Assign Cookies
**Problem**: Maximize satisfied children with cookies.

```cpp
int find_content_children(vector<int>& children, vector<int>& cookies) {
    sort(children.begin(), children.end());
    sort(cookies.begin(), cookies.end());
    
    int child = 0, cookie = 0;
    
    while (child < children.size() && cookie < cookies.size()) {
        if (cookies[cookie] >= children[child]) {
            child++;  // Satisfied
        }
        cookie++;
    }
    
    return child;
}

// Example
vector<int> children = {1, 2, 3};
vector<int> cookies = {1, 1};
// Give cookie to children with greed 1 and 2
// Output: 2
```

---

 Example 6: Partition Labels
**Problem**: Partition string into maximum parts where each letter appears in at most one part.

```cpp
vector<int> partition_labels(string s) {
    // Find last occurrence of each character
    vector<int> last(26);
    for (int i = 0; i < s.size(); i++) {
        last[s[i] - 'a'] = i;
    }
    
    vector<int> result;
    int start = 0, end = 0;
    
    for (int i = 0; i < s.size(); i++) {
        end = max(end, last[s[i] - 'a']);
        
        if (i == end) {
            result.push_back(end - start + 1);
            start = i + 1;
        }
    }
    
    return result;
}

// Example
string s = "ababcbacadefegdehijhklij";
// Output: [9, 7, 8]
// Partitions: "ababcbaca", "defegde", "hijhklij"
```

---

 Example 7: Two City Scheduling
**Problem**: Send N people to two cities minimizing total cost.

```cpp
int two_city_scheduling(vector<vector<int>>& costs) {
    // Sort by difference (cost[A] - cost[B])
    sort(costs.begin(), costs.end(), 
         [](vector<int>& a, vector<int>& b) {
             return (a[0] - a[1]) < (b[0] - b[1]);
         });
    
    int total_cost = 0;
    int n = costs.size() / 2;
    
    // Send first n to city A, rest to city B
    for (int i = 0; i < n; i++) {
        total_cost += costs[i][0];
    }
    for (int i = n; i < 2 * n; i++) {
        total_cost += costs[i][1];
    }
    
    return total_cost;
}

// Example
vector<vector<int>> costs = {{10,20}, {30,200}, {400,50}, {30,20}};
// Output: 110
```

---

 Example 8: Remove K Digits
**Problem**: Remove k digits to make smallest number.

```cpp
string remove_k_digits(string num, int k) {
    string result;
    
    for (char digit : num) {
        while (!result.empty() && k > 0 && result.back() > digit) {
            result.pop_back();
            k--;
        }
        result.push_back(digit);
    }
    
    // Remove remaining k digits from end
    result.resize(result.size() - k);
    
    // Remove leading zeros
    int start = 0;
    while (start < result.size() && result[start] == '0') {
        start++;
    }
    
    result = result.substr(start);
    return result.empty() ? "0" : result;
}

// Example
string num = "1432219";
int k = 3;
// Remove 4, 3, 2 to get "1219"
// Output: "1219"
```

---

 Example 9: Minimum Number of Arrows
**Problem**: Minimum arrows to burst all balloons.

```cpp
int find_min_arrow_shots(vector<vector<int>>& points) {
    if (points.empty()) return 0;
    
    // Sort by end position
    sort(points.begin(), points.end(), 
         [](vector<int>& a, vector<int>& b) {
             return a[1] < b[1];
         });
    
    int arrows = 1;
    int arrow_pos = points[0][1];
    
    for (int i = 1; i < points.size(); i++) {
        if (points[i][0] > arrow_pos) {
            // Need new arrow
            arrows++;
            arrow_pos = points[i][1];
        }
    }
    
    return arrows;
}

// Example
vector<vector<int>> points = {{10,16}, {2,8}, {1,6}, {7,12}};
// Output: 2 (shoot at 6 and 11)
```

---

 Example 10: Task Scheduler
**Problem**: Minimum time to complete tasks with cooling interval.

```cpp
int least_interval(vector<char>& tasks, int n) {
    vector<int> freq(26, 0);
    int max_freq = 0;
    
    // Count frequencies
    for (char task : tasks) {
        freq[task - 'A']++;
        max_freq = max(max_freq, freq[task - 'A']);
    }
    
    // Count tasks with max frequency
    int max_count = 0;
    for (int f : freq) {
        if (f == max_freq) {
            max_count++;
        }
    }
    
    // Calculate minimum time
    int intervals = (max_freq - 1) * (n + 1) + max_count;
    
    return max(intervals, (int)tasks.size());
}

// Example
vector<char> tasks = {'A','A','A','B','B','B'};
int n = 2;
// Schedule: A -> B -> idle -> A -> B -> idle -> A -> B
// Output: 8
```

---

 Time & Space Complexity
- **Time**: O(n) or O(n log n) with sorting
- **Space**: O(1) typically

Much faster than:
- DP: O(n²) or O(2^n)
- Backtracking: O(2^n) or O(n!)

---

 Greedy vs DP

| Greedy | DP |
|--------|-----|
| Makes choice now | Considers all options |
| No backtracking | Can reconsider |
| Not always optimal | Always optimal (if applicable) |
| Faster | Slower |

**When greedy works, use it!** But you must prove correctness.

---

 How to Prove Greedy Works

1. **Exchange argument**: Show greedy solution can be transformed to any optimal without making it worse
2. **Greedy stays ahead**: Show greedy maintains better state than any other approach
3. **Structural induction**: Prove inductively

---

 Common Greedy Patterns

 1. Activity/Interval Selection
- Sort by end time
- Pick earliest ending

 2. Fractional Knapsack
- Sort by value/weight ratio
- Pick highest ratio first

 3. Scheduling
- Sort by some criteria
- Make greedy choice

 4. Minimum Spanning Tree
- Kruskal's, Prim's algorithms

---

 Tips & Tricks

1. **Sort first**: Often need sorted data
2. **Prove correctness**: Don't assume greedy works
3. **Counter-example**: Try to find case where greedy fails
4. **Local vs global**: Verify local optimal leads to global
5. **Edge cases**: Empty input, single element

---

 When Greedy Fails

```cpp
// Coin change with coins = {1, 3, 4}
// Target = 6
// Greedy: 4 + 1 + 1 = 3 coins ❌
// Optimal: 3 + 3 = 2 coins ✅

// Use DP, not greedy!
```

---

 Practice Problems

 Easy
1. Assign Cookies (LeetCode 455)
2. Lemonade Change (LeetCode 860)
3. Best Time to Buy and Sell Stock II (LeetCode 122)

 Medium
4. Jump Game (LeetCode 55)
5. Jump Game II (LeetCode 45)
6. Gas Station (LeetCode 134)
7. Partition Labels (LeetCode 763)
8. Two City Scheduling (LeetCode 1029)
9. Remove K Digits (LeetCode 402)
10. Minimum Number of Arrows (LeetCode 452)

 Hard
11. Task Scheduler (LeetCode 621)
12. Candy (LeetCode 135)
13. Create Maximum Number (LeetCode 321)

---

 Key Takeaways
- ✅ Make locally optimal choice
- ✅ Must **prove** greedy works
- ✅ Usually involves **sorting**
- ✅ O(n) or O(n log n) time
- ✅ No backtracking (unlike DP)
- ✅ When works, much faster than DP
- ✅ Not always applicable - verify first!
