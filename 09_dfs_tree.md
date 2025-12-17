# DFS (Depth-First Search) - Tree Depth 🌲

## The Big Idea
Explore tree/graph by going as **deep as possible** before backtracking. Use recursion or stack.

**Why it works**: Recursion naturally explores depth-first by following one path completely before trying another.

---

 When to Use
- Find **all paths** in tree/graph
- Calculate **path sum**
- Find **diameter** or **height**
- Check tree **properties** (balanced, symmetric)
- **Backtracking** problems

**Keywords to spot**:
- "All paths"
- "Path sum"
- "Height/depth of tree"
- "Diameter"
- "Validate BST"
- "Serialize/deserialize"

---

 The Template

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

// Recursive DFS Template
void dfs(TreeNode* node) {
    if (!node) {
        return;  // Base case
    }
    
    // Process current node
    // ... do something with node->val
    
    // Recurse on children
    dfs(node->left);
    dfs(node->right);
}
```

---

 Three Types of DFS

 1. Preorder (Root → Left → Right)
```cpp
void preorder(TreeNode* root) {
    if (!root) return;
    
    process(root);        // Process first
    preorder(root->left);
    preorder(root->right);
}
```

 2. Inorder (Left → Root → Right)
```cpp
void inorder(TreeNode* root) {
    if (!root) return;
    
    inorder(root->left);
    process(root);        // Process in middle
    inorder(root->right);
}
```

 3. Postorder (Left → Right → Root)
```cpp
void postorder(TreeNode* root) {
    if (!root) return;
    
    postorder(root->left);
    postorder(root->right);
    process(root);        // Process last
}
```

---

 Example 1: Maximum Depth
**Problem**: Find maximum depth of binary tree.

```cpp
int max_depth(TreeNode* root) {
    if (!root) {
        return 0;
    }
    
    int left_depth = max_depth(root->left);
    int right_depth = max_depth(root->right);
    
    return 1 + max(left_depth, right_depth);
}

// Example
//       3
//      / \
//     9  20
//       /  \
//      15   7
// Output: 3
```

---

 Example 2: Path Sum
**Problem**: Check if there exists a root-to-leaf path with given sum.

```cpp
bool has_path_sum(TreeNode* root, int target_sum) {
    if (!root) {
        return false;
    }
    
    // Leaf node - check if sum matches
    if (!root->left && !root->right) {
        return root->val == target_sum;
    }
    
    // Recurse with reduced sum
    return has_path_sum(root->left, target_sum - root->val) ||
           has_path_sum(root->right, target_sum - root->val);
}

// Example
//       5
//      / \
//     4   8
//    /   / \
//   11  13  4
//  /  \      \
// 7    2      1
// target_sum = 22, Output: true (5->4->11->2)
```

---

 Example 3: All Root-to-Leaf Paths
**Problem**: Return all root-to-leaf paths.

```cpp
void find_paths_helper(TreeNode* node, vector<int>& path, vector<vector<int>>& all_paths) {
    if (!node) {
        return;
    }
    
    path.push_back(node->val);
    
    // Leaf node - save path
    if (!node->left && !node->right) {
        all_paths.push_back(path);
    } else {
        find_paths_helper(node->left, path, all_paths);
        find_paths_helper(node->right, path, all_paths);
    }
    
    path.pop_back();  // Backtrack
}

vector<vector<int>> all_paths(TreeNode* root) {
    vector<vector<int>> result;
    vector<int> current_path;
    find_paths_helper(root, current_path, result);
    return result;
}

// Example
//     1
//    / \
//   2   3
//  / \
// 4   5
// Output: [[1,2,4], [1,2,5], [1,3]]
```

---

 Example 4: Path Sum II (All Paths with Sum)
**Problem**: Find all root-to-leaf paths with given sum.

```cpp
void path_sum_helper(TreeNode* node, int target_sum, vector<int>& path, 
                     vector<vector<int>>& result) {
    if (!node) return;
    
    path.push_back(node->val);
    
    if (!node->left && !node->right && node->val == target_sum) {
        result.push_back(path);
    }
    
    path_sum_helper(node->left, target_sum - node->val, path, result);
    path_sum_helper(node->right, target_sum - node->val, path, result);
    
    path.pop_back();
}

vector<vector<int>> path_sum(TreeNode* root, int target_sum) {
    vector<vector<int>> result;
    vector<int> path;
    path_sum_helper(root, target_sum, path, result);
    return result;
}
```

---

 Example 5: Diameter of Binary Tree
**Problem**: Find longest path between any two nodes.

```cpp
int diameter_helper(TreeNode* node, int& diameter) {
    if (!node) {
        return 0;
    }
    
    int left_height = diameter_helper(node->left, diameter);
    int right_height = diameter_helper(node->right, diameter);
    
    // Update diameter (path through this node)
    diameter = max(diameter, left_height + right_height);
    
    // Return height
    return 1 + max(left_height, right_height);
}

int diameter_of_tree(TreeNode* root) {
    int diameter = 0;
    diameter_helper(root, diameter);
    return diameter;
}

// Example
//       1
//      / \
//     2   3
//    / \
//   4   5
// Diameter = 3 (path: 4->2->1->3)
```

---

 Example 6: Path with Maximum Sum
**Problem**: Find path with maximum sum (any node to any node).

```cpp
int max_path_sum_helper(TreeNode* node, int& max_sum) {
    if (!node) {
        return 0;
    }
    
    // Get max sum from left and right (ignore negative)
    int left_sum = max(0, max_path_sum_helper(node->left, max_sum));
    int right_sum = max(0, max_path_sum_helper(node->right, max_sum));
    
    // Update global max (path through this node)
    max_sum = max(max_sum, left_sum + right_sum + node->val);
    
    // Return max path going through this node
    return max(left_sum, right_sum) + node->val;
}

int max_path_sum(TreeNode* root) {
    int max_sum = INT_MIN;
    max_path_sum_helper(root, max_sum);
    return max_sum;
}
```

---

 Example 7: Count Paths with Sum
**Problem**: Count paths with given sum (not necessarily root-to-leaf).

```cpp
int count_paths_helper(TreeNode* node, int target_sum) {
    if (!node) return 0;
    
    int count = 0;
    
    // Count paths starting from this node
    if (node->val == target_sum) {
        count++;
    }
    
    // Continue path to children
    count += count_paths_helper(node->left, target_sum - node->val);
    count += count_paths_helper(node->right, target_sum - node->val);
    
    return count;
}

int path_sum_count(TreeNode* root, int target_sum) {
    if (!root) return 0;
    
    // Count paths starting from root
    int paths_from_root = count_paths_helper(root, target_sum);
    
    // Count paths in left and right subtrees
    int paths_left = path_sum_count(root->left, target_sum);
    int paths_right = path_sum_count(root->right, target_sum);
    
    return paths_from_root + paths_left + paths_right;
}
```

---

 Example 8: Lowest Common Ancestor
**Problem**: Find lowest common ancestor of two nodes.

```cpp
TreeNode* lowest_common_ancestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) {
        return root;
    }
    
    TreeNode* left = lowest_common_ancestor(root->left, p, q);
    TreeNode* right = lowest_common_ancestor(root->right, p, q);
    
    if (left && right) {
        return root;  // Both found in different subtrees
    }
    
    return left ? left : right;  // Return non-null side
}
```

---

 Example 9: Validate BST
**Problem**: Check if tree is a valid binary search tree.

```cpp
bool is_valid_bst_helper(TreeNode* node, long min_val, long max_val) {
    if (!node) {
        return true;
    }
    
    if (node->val <= min_val || node->val >= max_val) {
        return false;
    }
    
    return is_valid_bst_helper(node->left, min_val, node->val) &&
           is_valid_bst_helper(node->right, node->val, max_val);
}

bool is_valid_bst(TreeNode* root) {
    return is_valid_bst_helper(root, LONG_MIN, LONG_MAX);
}
```

---

 Example 10: Tree Paths Sum
**Problem**: Sum all numbers formed by root-to-leaf paths.

```cpp
int sum_numbers_helper(TreeNode* node, int current_number) {
    if (!node) {
        return 0;
    }
    
    current_number = current_number * 10 + node->val;
    
    // Leaf node
    if (!node->left && !node->right) {
        return current_number;
    }
    
    return sum_numbers_helper(node->left, current_number) +
           sum_numbers_helper(node->right, current_number);
}

int sum_numbers(TreeNode* root) {
    return sum_numbers_helper(root, 0);
}

// Example
//     1
//    / \
//   2   3
// Paths: 12, 13 -> Sum = 25
```

---

 Iterative DFS (Using Stack)

```cpp
void iterative_dfs(TreeNode* root) {
    if (!root) return;
    
    stack<TreeNode*> s;
    s.push(root);
    
    while (!s.empty()) {
        TreeNode* node = s.top();
        s.pop();
        
        // Process node
        process(node);
        
        // Push children (right first, so left is processed first)
        if (node->right) s.push(node->right);
        if (node->left) s.push(node->left);
    }
}
```

---

 Time & Space Complexity
- **Time**: O(n) - visit each node once
- **Space**: 
  - O(h) recursion stack - h is height
  - Best case (balanced): O(log n)
  - Worst case (skewed): O(n)

---

 DFS Templates Summary

 Preorder (Process → Recurse)
- **Use for**: Copy tree, serialize, prefix expression

 Inorder (Recurse left → Process → Recurse right)
- **Use for**: BST sorted order, validate BST

 Postorder (Recurse → Process)
- **Use for**: Delete tree, calculate heights, postfix expression

---

 Tips & Tricks

1. **Base case**: Always check for `!node`
2. **Leaf check**: `!node->left && !node->right`
3. **Backtracking**: Remember to pop from path after recursion
4. **Pass by reference**: Use `&` for variables you want to update globally
5. **Return value**: Return value vs pass by reference - choose wisely

---

 Common Patterns

 Height Calculation
```cpp
return 1 + max(left_height, right_height);
```

 Path Problems
```cpp
path.push_back(node->val);
// ... recurse
path.pop_back();  // Backtrack
```

 Global Variable
```cpp
void helper(TreeNode* node, int& global_var) {
    // Update global_var
}
```

---

 Practice Problems

1. **Easy**: Maximum Depth of Binary Tree (LeetCode 104)
2. **Easy**: Path Sum (LeetCode 112)
3. **Medium**: Path Sum II (LeetCode 113)
4. **Easy**: Diameter of Binary Tree (LeetCode 543)
5. **Hard**: Binary Tree Maximum Path Sum (LeetCode 124)
6. **Medium**: Path Sum III (LeetCode 437)
7. **Easy**: Sum of Root To Leaf Binary Numbers (LeetCode 1022)
8. **Easy**: Lowest Common Ancestor of BST (LeetCode 235)
9. **Medium**: Validate Binary Search Tree (LeetCode 98)
10. **Medium**: Flatten Binary Tree to Linked List (LeetCode 114)

---

 Key Takeaways
- ✅ Use recursion for natural DFS
- ✅ Always check base case (!node)
- ✅ Choose traversal order based on problem
- ✅ Backtrack when maintaining path
- ✅ Use reference for global updates
- ✅ Space: O(height) for recursion stack
