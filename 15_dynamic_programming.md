# Dynamic Programming Pattern 💰

## The Big Idea
Break problem into **overlapping subproblems**, solve each once, and **store results** to avoid recomputation.

**Formula**: DP = Recursion + Memoization

**Why it works**: Many problems have optimal substructure (optimal solution contains optimal solutions to subproblems) and overlapping subproblems (same subproblems computed multiple times).

---

 When to Use
- **Optimization** problems (max/min, count ways)
- **Overlapping subproblems**
- **Optimal substructure**
- Can write **recurrence relation**

**Keywords to spot**:
- "Maximum/minimum"
- "Count number of ways"
- "Longest/shortest"
- "Can you reach..."
- "Optimize", "best way"

---

 The Template

 Top-Down (Memoization)
```cpp
unordered_map<string, int> memo;

int dp(/* state parameters */) {
    // Base case
    if (base_condition) {
        return base_value;
    }
    
    // Check memo
    string key = create_key(state);
    if (memo.count(key)) {
        return memo[key];
    }
    
    // Compute and store
    int result = /* recurrence relation */;
    memo[key] = result;
    return result;
}
```

 Bottom-Up (Tabulation)
```cpp
int dp(/* parameters */) {
    vector<int> dp(n + 1);
    
    // Base case
    dp[0] = base_value;
    
    // Fill table
    for (int i = 1; i <= n; i++) {
        dp[i] = /* recurrence relation using dp[j] where j < i */;
    }
    
    return dp[n];
}
```

---

 Example 1: Fibonacci
**Problem**: Calculate nth Fibonacci number.

```cpp
// Top-Down
unordered_map<int, int> memo;

int fib(int n) {
    if (n <= 1) return n;
    
    if (memo.count(n)) {
        return memo[n];
    }
    
    memo[n] = fib(n - 1) + fib(n - 2);
    return memo[n];
}

// Bottom-Up
int fib(int n) {
    if (n <= 1) return n;
    
    vector<int> dp(n + 1);
    dp[0] = 0;
    dp[1] = 1;
    
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    
    return dp[n];
}

// Space Optimized
int fib(int n) {
    if (n <= 1) return n;
    
    int prev2 = 0, prev1 = 1;
    
    for (int i = 2; i <= n; i++) {
        int current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }
    
    return prev1;
}
```

---

 Example 2: Climbing Stairs
**Problem**: How many ways to climb n stairs (can take 1 or 2 steps)?

```cpp
int climb_stairs(int n) {
    if (n <= 2) return n;
    
    vector<int> dp(n + 1);
    dp[1] = 1;  // 1 way to reach step 1
    dp[2] = 2;  // 2 ways to reach step 2
    
    for (int i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    
    return dp[n];
}

// Example: n = 5
// Ways: [1,1,1,1,1], [1,1,1,2], [1,1,2,1], [1,2,1,1], [2,1,1,1], 
//       [1,2,2], [2,1,2], [2,2,1]
// Output: 8
```

---

 Example 3: House Robber
**Problem**: Rob houses to maximize money (can't rob adjacent houses).

```cpp
int rob(vector<int>& nums) {
    int n = nums.size();
    if (n == 0) return 0;
    if (n == 1) return nums[0];
    
    vector<int> dp(n);
    dp[0] = nums[0];
    dp[1] = max(nums[0], nums[1]);
    
    for (int i = 2; i < n; i++) {
        dp[i] = max(dp[i - 1],              // Don't rob house i
                    dp[i - 2] + nums[i]);   // Rob house i
    }
    
    return dp[n - 1];
}

// Example
vector<int> nums = {2, 7, 9, 3, 1};
// Rob houses 0, 2, 4: 2 + 9 + 1 = 12
```

---

 Example 4: Coin Change
**Problem**: Find minimum coins needed to make amount.

```cpp
int coin_change(vector<int>& coins, int amount) {
    vector<int> dp(amount + 1, INT_MAX);
    dp[0] = 0;  // 0 coins for amount 0
    
    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (i >= coin && dp[i - coin] != INT_MAX) {
                dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
    }
    
    return dp[amount] == INT_MAX ? -1 : dp[amount];
}

// Example
vector<int> coins = {1, 2, 5};
int amount = 11;
// Output: 3 (5 + 5 + 1)
```

---

 Example 5: Longest Increasing Subsequence
**Problem**: Find length of longest increasing subsequence.

```cpp
int longest_increasing_subsequence(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, 1);  // Each element is subsequence of length 1
    
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }
    
    return *max_element(dp.begin(), dp.end());
}

// Example
vector<int> nums = {10, 9, 2, 5, 3, 7, 101, 18};
// LIS: [2, 3, 7, 101] or [2, 5, 7, 101]
// Output: 4
```

---

 Example 6: 0/1 Knapsack
**Problem**: Maximize value with weight constraint (each item used 0 or 1 times).

```cpp
int knapsack(vector<int>& weights, vector<int>& values, int capacity) {
    int n = weights.size();
    vector<vector<int>> dp(n + 1, vector<int>(capacity + 1, 0));
    
    for (int i = 1; i <= n; i++) {
        for (int w = 0; w <= capacity; w++) {
            if (weights[i - 1] <= w) {
                // Can include item i
                dp[i][w] = max(dp[i - 1][w],  // Don't include
                              dp[i - 1][w - weights[i - 1]] + values[i - 1]);  // Include
            } else {
                // Can't include item i
                dp[i][w] = dp[i - 1][w];
            }
        }
    }
    
    return dp[n][capacity];
}

// Example
vector<int> weights = {1, 3, 4, 5};
vector<int> values = {1, 4, 5, 7};
int capacity = 7;
// Take items with weights 3 and 4: value = 4 + 5 = 9
```

---

 Example 7: Longest Common Subsequence
**Problem**: Find length of longest common subsequence.

```cpp
int longest_common_subsequence(string text1, string text2) {
    int m = text1.size(), n = text2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1[i - 1] == text2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1] + 1;
            } else {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }
    
    return dp[m][n];
}

// Example
string text1 = "abcde";
string text2 = "ace";
// LCS: "ace"
// Output: 3
```

---

 Example 8: Edit Distance
**Problem**: Minimum operations to convert one string to another.

```cpp
int min_distance(string word1, string word2) {
    int m = word1.size(), n = word2.size();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1));
    
    // Base cases
    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;
    
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (word1[i - 1] == word2[j - 1]) {
                dp[i][j] = dp[i - 1][j - 1];  // No operation needed
            } else {
                dp[i][j] = 1 + min({
                    dp[i - 1][j],      // Delete
                    dp[i][j - 1],      // Insert
                    dp[i - 1][j - 1]   // Replace
                });
            }
        }
    }
    
    return dp[m][n];
}

// Example
string word1 = "horse";
string word2 = "ros";
// Output: 3 (horse -> rorse -> rose -> ros)
```

---

 Example 9: Partition Equal Subset Sum
**Problem**: Can array be partitioned into two subsets with equal sum?

```cpp
bool can_partition(vector<int>& nums) {
    int total_sum = accumulate(nums.begin(), nums.end(), 0);
    
    if (total_sum % 2 != 0) return false;
    
    int target = total_sum / 2;
    vector<bool> dp(target + 1, false);
    dp[0] = true;
    
    for (int num : nums) {
        for (int j = target; j >= num; j--) {
            dp[j] = dp[j] || dp[j - num];
        }
    }
    
    return dp[target];
}

// Example
vector<int> nums = {1, 5, 11, 5};
// Can partition to [1, 5, 5] and [11]
// Output: true
```

---

 Example 10: Maximum Product Subarray
**Problem**: Find contiguous subarray with largest product.

```cpp
int max_product(vector<int>& nums) {
    int max_so_far = nums[0];
    int max_ending_here = nums[0];
    int min_ending_here = nums[0];
    
    for (int i = 1; i < nums.size(); i++) {
        if (nums[i] < 0) {
            swap(max_ending_here, min_ending_here);
        }
        
        max_ending_here = max(nums[i], max_ending_here * nums[i]);
        min_ending_here = min(nums[i], min_ending_here * nums[i]);
        
        max_so_far = max(max_so_far, max_ending_here);
    }
    
    return max_so_far;
}

// Example
vector<int> nums = {2, 3, -2, 4};
// Subarray [2, 3] has product 6
// Output: 6
```

---

 Time & Space Complexity

| Pattern | Time | Space |
|---------|------|-------|
| 1D DP | O(n) | O(n) → O(1) |
| 2D DP | O(n²) | O(n²) → O(n) |
| Knapsack | O(n × W) | O(n × W) → O(W) |

---

 DP Categories

 1. Linear DP (1D)
- Climbing Stairs
- House Robber
- Decode Ways

 2. 2D DP (Grid/String)
- Longest Common Subsequence
- Edit Distance
- Unique Paths

 3. Knapsack
- 0/1 Knapsack
- Subset Sum
- Partition Equal Subset

 4. Interval DP
- Palindrome Partitioning
- Burst Balloons
- Matrix Chain Multiplication

---

 Steps to Solve DP

1. **Identify** if it's DP (optimization, overlapping subproblems)
2. **Define state**: What parameters uniquely identify subproblem?
3. **Write recurrence**: How to compute state from smaller states?
4. **Base cases**: What are trivial cases?
5. **Memoization or Tabulation**: Choose approach
6. **Space optimization**: Can you reduce space?

---

 Top-Down vs Bottom-Up

| Top-Down (Memoization) | Bottom-Up (Tabulation) |
|------------------------|------------------------|
| Recursion + Memo | Iterative |
| Only computes needed | Computes all |
| Stack overhead | No recursion |
| Easier to write | More efficient |

---

 Tips & Tricks

1. **Draw decision tree**: Visualize recursive calls
2. **Identify state**: What changes in recursion?
3. **Memo key**: Convert state to string/tuple
4. **Space optimization**: Often need only last 1-2 rows
5. **Edge cases**: Empty input, single element
6. **Direction**: Iterate in correct order for dependencies

---

 Practice Problems

 Easy
1. Climbing Stairs (LeetCode 70)
2. Min Cost Climbing Stairs (LeetCode 746)
3. House Robber (LeetCode 198)

 Medium
4. Coin Change (LeetCode 322)
5. Longest Increasing Subsequence (LeetCode 300)
6. Longest Common Subsequence (LeetCode 1143)
7. Partition Equal Subset Sum (LeetCode 416)
8. Maximum Product Subarray (LeetCode 152)
9. Decode Ways (LeetCode 91)
10. Unique Paths (LeetCode 62)

 Hard
11. Edit Distance (LeetCode 72)
12. Regular Expression Matching (LeetCode 10)
13. Burst Balloons (LeetCode 312)
14. Palindrome Partitioning II (LeetCode 132)

---

 Key Takeaways
- ✅ Optimal substructure + overlapping subproblems
- ✅ Recursion + Memoization = DP
- ✅ Define state clearly
- ✅ Write recurrence relation
- ✅ Bottom-up usually more efficient
- ✅ Space can often be optimized
- ✅ Practice identifying DP patterns
