# Backtracking Pattern ⬅️➡️

## The Big Idea
Explore **all possibilities** by making choices, exploring consequences, then **undoing** choices (backtracking) to try other options.

**Think of it as**: Try → Explore → Undo

**Why it works**: Systematically explores all possible solutions by building candidates incrementally and abandoning them when they can't lead to valid solution.

---

 When to Use
- Generate **all** combinations/permutations
- Find **all** solutions (not just one)
- **Constraint satisfaction** problems
- **Decision tree** exploration

**Keywords to spot**:
- "All subsets"
- "All permutations"
- "All combinations"
- "Generate all"
- "N-Queens"
- "Sudoku"
- "Word search"

---

 The Template

```cpp
void backtrack(result, current_candidate, remaining_choices) {
    // Base case: found valid solution
    if (is_solution(current_candidate)) {
        result.push_back(current_candidate);
        return;
    }
    
    // Try each possibility
    for (choice in remaining_choices) {
        // Make choice
        current_candidate.push_back(choice);
        
        // Explore
        backtrack(result, current_candidate, new_remaining_choices);
        
        // Undo choice (backtrack)
        current_candidate.pop_back();
    }
}
```

---

 Example 1: Generate All Subsets
**Problem**: Generate all possible subsets of a set.

```cpp
void backtrack(vector<int>& nums, int start, vector<int>& current, 
               vector<vector<int>>& result) {
    result.push_back(current);  // Add current subset
    
    for (int i = start; i < nums.size(); i++) {
        current.push_back(nums[i]);           // Choose
        backtrack(nums, i + 1, current, result);  // Explore
        current.pop_back();                   // Unchoose (backtrack)
    }
}

vector<vector<int>> subsets(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> current;
    backtrack(nums, 0, current, result);
    return result;
}

// Example
vector<int> nums = {1, 2, 3};
// Output: [[], [1], [2], [3], [1,2], [1,3], [2,3], [1,2,3]]
```

**Decision tree**:
```
                    []
          /         |        \
        [1]        [2]       [3]
       /   \        |
    [1,2] [1,3]   [2,3]
      |
   [1,2,3]
```

---

 Example 2: All Permutations
**Problem**: Generate all permutations of array.

```cpp
void backtrack(vector<int>& nums, vector<int>& current, vector<bool>& used,
               vector<vector<int>>& result) {
    if (current.size() == nums.size()) {
        result.push_back(current);
        return;
    }
    
    for (int i = 0; i < nums.size(); i++) {
        if (used[i]) continue;  // Skip if already used
        
        current.push_back(nums[i]);
        used[i] = true;
        
        backtrack(nums, current, used, result);
        
        current.pop_back();
        used[i] = false;
    }
}

vector<vector<int>> permute(vector<int>& nums) {
    vector<vector<int>> result;
    vector<int> current;
    vector<bool> used(nums.size(), false);
    backtrack(nums, current, used, result);
    return result;
}

// Example
vector<int> nums = {1, 2, 3};
// Output: [[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], [3,2,1]]
```

---

 Example 3: Combination Sum
**Problem**: Find all combinations that sum to target (can reuse elements).

```cpp
void backtrack(vector<int>& candidates, int target, int start,
               vector<int>& current, vector<vector<int>>& result) {
    if (target == 0) {
        result.push_back(current);
        return;
    }
    
    if (target < 0) {
        return;  // Exceeded target
    }
    
    for (int i = start; i < candidates.size(); i++) {
        current.push_back(candidates[i]);
        backtrack(candidates, target - candidates[i], i, current, result);
        current.pop_back();
    }
}

vector<vector<int>> combination_sum(vector<int>& candidates, int target) {
    vector<vector<int>> result;
    vector<int> current;
    backtrack(candidates, target, 0, current, result);
    return result;
}

// Example
vector<int> candidates = {2, 3, 6, 7};
int target = 7;
// Output: [[2,2,3], [7]]
```

---

 Example 4: Letter Combinations of Phone Number
**Problem**: Generate all letter combinations from phone number digits.

```cpp
vector<string> letter_map = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

void backtrack(string& digits, int index, string& current, vector<string>& result) {
    if (index == digits.size()) {
        result.push_back(current);
        return;
    }
    
    string letters = letter_map[digits[index] - '0'];
    
    for (char letter : letters) {
        current.push_back(letter);
        backtrack(digits, index + 1, current, result);
        current.pop_back();
    }
}

vector<string> letter_combinations(string digits) {
    if (digits.empty()) return {};
    
    vector<string> result;
    string current;
    backtrack(digits, 0, current, result);
    return result;
}

// Example
string digits = "23";
// Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

---

 Example 5: Generate Parentheses
**Problem**: Generate all valid combinations of n pairs of parentheses.

```cpp
void backtrack(int n, int open, int close, string& current, vector<string>& result) {
    if (current.size() == 2 * n) {
        result.push_back(current);
        return;
    }
    
    if (open < n) {
        current.push_back('(');
        backtrack(n, open + 1, close, current, result);
        current.pop_back();
    }
    
    if (close < open) {
        current.push_back(')');
        backtrack(n, open, close + 1, current, result);
        current.pop_back();
    }
}

vector<string> generate_parenthesis(int n) {
    vector<string> result;
    string current;
    backtrack(n, 0, 0, current, result);
    return result;
}

// Example
int n = 3;
// Output: ["((()))","(()())","(())()","()(())","()()()"]
```

---

 Example 6: N-Queens
**Problem**: Place N queens on N×N chessboard so no two queens attack each other.

```cpp
bool is_safe(vector<string>& board, int row, int col, int n) {
    // Check column
    for (int i = 0; i < row; i++) {
        if (board[i][col] == 'Q') return false;
    }
    
    // Check diagonal (top-left)
    for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
        if (board[i][j] == 'Q') return false;
    }
    
    // Check diagonal (top-right)
    for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
        if (board[i][j] == 'Q') return false;
    }
    
    return true;
}

void backtrack(int row, int n, vector<string>& board, vector<vector<string>>& result) {
    if (row == n) {
        result.push_back(board);
        return;
    }
    
    for (int col = 0; col < n; col++) {
        if (is_safe(board, row, col, n)) {
            board[row][col] = 'Q';
            backtrack(row + 1, n, board, result);
            board[row][col] = '.';
        }
    }
}

vector<vector<string>> solve_n_queens(int n) {
    vector<vector<string>> result;
    vector<string> board(n, string(n, '.'));
    backtrack(0, n, board, result);
    return result;
}
```

---

 Example 7: Word Search
**Problem**: Find if word exists in 2D board.

```cpp
bool backtrack(vector<vector<char>>& board, string& word, int index, int row, int col) {
    if (index == word.size()) {
        return true;  // Found complete word
    }
    
    if (row < 0 || row >= board.size() || col < 0 || col >= board[0].size() ||
        board[row][col] != word[index]) {
        return false;
    }
    
    char temp = board[row][col];
    board[row][col] = '';  // Mark as visited
    
    bool found = backtrack(board, word, index + 1, row + 1, col) ||
                 backtrack(board, word, index + 1, row - 1, col) ||
                 backtrack(board, word, index + 1, row, col + 1) ||
                 backtrack(board, word, index + 1, row, col - 1);
    
    board[row][col] = temp;  // Restore
    
    return found;
}

bool exist(vector<vector<char>>& board, string word) {
    for (int i = 0; i < board.size(); i++) {
        for (int j = 0; j < board[0].size(); j++) {
            if (backtrack(board, word, 0, i, j)) {
                return true;
            }
        }
    }
    return false;
}
```

---

 Example 8: Palindrome Partitioning
**Problem**: Partition string into all possible palindrome substrings.

```cpp
bool is_palindrome(string& s, int left, int right) {
    while (left < right) {
        if (s[left++] != s[right--]) return false;
    }
    return true;
}

void backtrack(string& s, int start, vector<string>& current, 
               vector<vector<string>>& result) {
    if (start == s.size()) {
        result.push_back(current);
        return;
    }
    
    for (int end = start; end < s.size(); end++) {
        if (is_palindrome(s, start, end)) {
            current.push_back(s.substr(start, end - start + 1));
            backtrack(s, end + 1, current, result);
            current.pop_back();
        }
    }
}

vector<vector<string>> partition(string s) {
    vector<vector<string>> result;
    vector<string> current;
    backtrack(s, 0, current, result);
    return result;
}

// Example
string s = "aab";
// Output: [["a","a","b"], ["aa","b"]]
```

---

 Time & Space Complexity
- **Time**: O(2^n) for subsets, O(n!) for permutations
  - Exponential - explores all possibilities
- **Space**: O(n) for recursion stack

---

 Optimization Techniques

 1. Pruning
```cpp
if (current_sum > target) {
    return;  // Stop early, no need to explore further
}
```

 2. Sorting
```cpp
sort(nums.begin(), nums.end());  // For early termination
```

 3. Visited Array
```cpp
vector<bool> visited(n, false);
// Mark and unmark during backtracking
```

 4. Memoization
```cpp
unordered_map<string, bool> memo;
// Cache results of subproblems
```

---

 Common Patterns

 Generate All
```cpp
void backtrack(/* params */) {
    result.push_back(current);  // Add every state
    for (choice : choices) {
        make_choice();
        backtrack(/* params */);
        undo_choice();
    }
}
```

 Find Any Solution
```cpp
bool backtrack(/* params */) {
    if (is_solution()) return true;
    for (choice : choices) {
        make_choice();
        if (backtrack(/* params */)) return true;
        undo_choice();
    }
    return false;
}
```

---

 Tips & Tricks

1. **Three steps**: Choose → Explore → Unchoose
2. **Base case**: When to save solution
3. **Pruning**: Stop early if path can't lead to solution
4. **Visited marking**: Use temp variable or separate array
5. **Start index**: Prevent duplicate combinations
6. **Draw decision tree**: Visualize the exploration

---

 Backtracking vs Other Patterns

| Pattern | Use Case |
|---------|----------|
| Backtracking | All solutions |
| Greedy | One optimal solution (fast) |
| DP | Optimal with overlapping subproblems |
| DFS | Explore graph/tree |

---

 Practice Problems

1. **Medium**: Subsets (LeetCode 78)
2. **Medium**: Permutations (LeetCode 46)
3. **Medium**: Combination Sum (LeetCode 39)
4. **Medium**: Letter Combinations of Phone Number (LeetCode 17)
5. **Medium**: Generate Parentheses (LeetCode 22)
6. **Hard**: N-Queens (LeetCode 51)
7. **Medium**: Word Search (LeetCode 79)
8. **Medium**: Palindrome Partitioning (LeetCode 131)
9. **Medium**: Combinations (LeetCode 77)
10. **Hard**: Sudoku Solver (LeetCode 37)

---

 Key Takeaways
- ✅ Choose → Explore → Unchoose
- ✅ Generate **all** solutions
- ✅ Use recursion to explore possibilities
- ✅ Backtrack by undoing choices
- ✅ Prune invalid paths early
- ✅ Exponential time complexity
- ✅ Perfect for constraint satisfaction
