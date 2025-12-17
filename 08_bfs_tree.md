# BFS (Breadth-First Search) - Tree Level Order 🌳

## The Big Idea
Traverse tree **level by level** using a queue. Process all nodes at current level before moving to next level.

**Why it works**: Queue ensures FIFO (First In First Out) - nodes are processed in the order they were discovered.

---

 When to Use
- Tree/graph traversal **level by level**
- Find **shortest path** in unweighted graph
- **Minimum depth** of tree
- Level order traversal

**Keywords to spot**:
- "Level order traversal"
- "Minimum depth"
- "Right side view"
- "Zigzag traversal"
- "Level averages"
- "Connect nodes at same level"

---

 The Template

```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
};

vector<vector<int>> level_order(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) {
        return result;
    }
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int level_size = q.size();
        vector<int> current_level;
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            
            current_level.push_back(node->val);
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        
        result.push_back(current_level);
    }
    
    return result;
}
```

---

 Example 1: Level Order Traversal
**Problem**: Return level order traversal of a tree.

```cpp
vector<vector<int>> level_order(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int level_size = q.size();
        vector<int> current_level;
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            current_level.push_back(node->val);
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        
        result.push_back(current_level);
    }
    
    return result;
}

// Example
//       3
//      / \
//     9  20
//       /  \
//      15   7
// Output: [[3], [9,20], [15,7]]
```

**Visual walkthrough**:
```
Queue: [3]          Level 0: [3]
Queue: [9, 20]      Level 1: [9, 20]
Queue: [15, 7]      Level 2: [15, 7]
```

---

 Example 2: Zigzag Level Order
**Problem**: Return zigzag level order (left-to-right, then right-to-left alternating).

```cpp
vector<vector<int>> zigzag_level_order(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    
    queue<TreeNode*> q;
    q.push(root);
    bool left_to_right = true;
    
    while (!q.empty()) {
        int level_size = q.size();
        vector<int> current_level(level_size);
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            
            // Find position to insert
            int index = left_to_right ? i : (level_size - 1 - i);
            current_level[index] = node->val;
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        
        left_to_right = !left_to_right;
        result.push_back(current_level);
    }
    
    return result;
}

// Example
//       3
//      / \
//     9  20
//       /  \
//      15   7
// Output: [[3], [20,9], [15,7]]
```

---

 Example 3: Minimum Depth
**Problem**: Find minimum depth of tree (shortest path to leaf).

```cpp
int min_depth(TreeNode* root) {
    if (!root) return 0;
    
    queue<TreeNode*> q;
    q.push(root);
    int depth = 0;
    
    while (!q.empty()) {
        depth++;
        int level_size = q.size();
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            
            // Check if leaf node
            if (!node->left && !node->right) {
                return depth;  // First leaf found!
            }
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
    
    return depth;
}

// Example
//       3
//      / \
//     9  20
//       /  \
//      15   7
// Output: 2 (path: 3 -> 9)
```

---

 Example 4: Right Side View
**Problem**: Return values you would see from the right side of the tree.

```cpp
vector<int> right_side_view(TreeNode* root) {
    vector<int> result;
    if (!root) return result;
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int level_size = q.size();
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            
            // Last node of level
            if (i == level_size - 1) {
                result.push_back(node->val);
            }
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
    
    return result;
}

// Example
//       1
//      / \
//     2   3
//      \   \
//       5   4
// Output: [1, 3, 4]
```

**Visual**:
```
Right view:
Level 0: 1
Level 1: 3 (rightmost)
Level 2: 4 (rightmost)
```

---

 Example 5: Level Averages
**Problem**: Find average value of nodes on each level.

```cpp
vector<double> average_of_levels(TreeNode* root) {
    vector<double> result;
    if (!root) return result;
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int level_size = q.size();
        double sum = 0;
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            sum += node->val;
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        
        result.push_back(sum / level_size);
    }
    
    return result;
}

// Example
//       3
//      / \
//     9  20
//       /  \
//      15   7
// Output: [3.0, 14.5, 11.0]
```

---

 Example 6: Connect Level Order Siblings
**Problem**: Connect all nodes at the same level (with next pointer).

```cpp
struct Node {
    int val;
    Node* left;
    Node* right;
    Node* next;
};

Node* connect(Node* root) {
    if (!root) return root;
    
    queue<Node*> q;
    q.push(root);
    
    while (!q.empty()) {
        int level_size = q.size();
        Node* prev = nullptr;
        
        for (int i = 0; i < level_size; i++) {
            Node* node = q.front();
            q.pop();
            
            if (prev) {
                prev->next = node;
            }
            prev = node;
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        
        prev->next = nullptr;  // Last node of level
    }
    
    return root;
}

// Example
//       1
//      / \
//     2   3
//    / \ / \
//   4  5 6  7
// After: 1->NULL, 2->3->NULL, 4->5->6->7->NULL
```

---

 Example 7: Level Order Successor
**Problem**: Find the node that comes right after given node in level order.

```cpp
TreeNode* find_successor(TreeNode* root, int key) {
    if (!root) return nullptr;
    
    queue<TreeNode*> q;
    q.push(root);
    bool found = false;
    
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        
        if (found) {
            return node;  // Return next node after key
        }
        
        if (node->val == key) {
            found = true;
        }
        
        if (node->left) q.push(node->left);
        if (node->right) q.push(node->right);
    }
    
    return nullptr;
}

// Example
//       1
//      / \
//     2   3
//    / \
//   4   5
// Key = 3, Output: 4 (next in level order)
```

---

 Example 8: Bottom-Up Level Order
**Problem**: Return level order traversal from bottom to top.

```cpp
vector<vector<int>> level_order_bottom(TreeNode* root) {
    vector<vector<int>> result;
    if (!root) return result;
    
    queue<TreeNode*> q;
    q.push(root);
    
    while (!q.empty()) {
        int level_size = q.size();
        vector<int> current_level;
        
        for (int i = 0; i < level_size; i++) {
            TreeNode* node = q.front();
            q.pop();
            current_level.push_back(node->val);
            
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        
        result.push_back(current_level);
    }
    
    reverse(result.begin(), result.end());
    return result;
}

// Example
//       3
//      / \
//     9  20
//       /  \
//      15   7
// Output: [[15,7], [9,20], [3]]
```

---

 Time & Space Complexity
- **Time**: O(n) - visit each node once
- **Space**: O(w) - w is maximum width of tree (queue size)

For balanced tree: O(log n)
For skewed tree: O(n)

---

 Common Variations

 Track Level Number
```cpp
int level = 0;
while (!q.empty()) {
    level++;
    int level_size = q.size();
    // ... process level
}
```

 Track Null Nodes
```cpp
q.push(nullptr);  // Use as level separator
```

 Bi-directional BFS (Graph)
```cpp
queue<Node*> q1, q2;  // Search from both ends
```

---

 Tips & Tricks

1. **Save level_size**: Before processing, save `q.size()`
2. **Use for loop**: Process exactly `level_size` nodes
3. **Check children**: Only add non-null children to queue
4. **Edge cases**: Empty tree, single node
5. **Queue operations**: `push()`, `front()`, `pop()`

---

 BFS vs DFS

| BFS | DFS |
|-----|-----|
| Uses Queue | Uses Stack/Recursion |
| Level by level | Depth first |
| Shortest path | All paths |
| More memory | Less memory |

---

 Practice Problems

1. **Medium**: Binary Tree Level Order Traversal (LeetCode 102)
2. **Medium**: Binary Tree Zigzag Level Order (LeetCode 103)
3. **Easy**: Minimum Depth of Binary Tree (LeetCode 111)
4. **Easy**: Average of Levels in Binary Tree (LeetCode 637)
5. **Medium**: Binary Tree Right Side View (LeetCode 199)
6. **Medium**: Populating Next Right Pointers (LeetCode 116)
7. **Medium**: Binary Tree Level Order Traversal II (LeetCode 107)
8. **Easy**: Symmetric Tree (LeetCode 101)

---

 Key Takeaways
- ✅ Use queue for BFS (FIFO order)
- ✅ Save level_size before processing
- ✅ Process one level at a time
- ✅ Perfect for shortest path problems
- ✅ Add children left-to-right
- ✅ Check for null before adding to queue
