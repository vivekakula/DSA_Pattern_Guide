# In-place Reversal of LinkedList Pattern ↩️

## The Big Idea
Reverse a linked list (or part of it) by changing pointers **in-place** without using extra space.

**Why it works**: We iterate through the list once, reversing the direction of pointers as we go.

---

 When to Use
- **Reverse** a linked list (whole or part)
- Reverse **k-group** of nodes
- Problems involving linked list **pointer manipulation**

**Keywords to spot**:
- "Reverse linked list"
- "Reverse nodes in k-group"
- "Reverse between positions"
- "Swap nodes in pairs"

---

 The Template

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* reverse_list(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* current = head;
    
    while (current != nullptr) {
        ListNode* next = current->next;  // Save next
        current->next = prev;            // Reverse pointer
        prev = current;                  // Move prev forward
        current = next;                  // Move current forward
    }
    
    return prev;  // New head
}
```

---

 Example 1: Reverse Entire Linked List
**Problem**: Reverse a linked list.

```cpp
ListNode* reverse_list(ListNode* head) {
    ListNode* prev = nullptr;
    ListNode* current = head;
    
    while (current) {
        ListNode* next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    
    return prev;
}

// Example
// Input:  1 -> 2 -> 3 -> 4 -> 5
// Output: 5 -> 4 -> 3 -> 2 -> 1
```

**Visual walkthrough**:
```
Initial: 1 -> 2 -> 3 -> 4 -> 5 -> null
         c

Step 1:  null <- 1    2 -> 3 -> 4 -> 5 -> null
              p       c

Step 2:  null <- 1 <- 2    3 -> 4 -> 5 -> null
                   p       c

Step 3:  null <- 1 <- 2 <- 3    4 -> 5 -> null
                        p       c

Step 4:  null <- 1 <- 2 <- 3 <- 4    5 -> null
                             p       c

Step 5:  null <- 1 <- 2 <- 3 <- 4 <- 5
                                  p       c (null)

Return prev (which is 5, the new head)
```

---

 Example 2: Reverse Sublist (Between Positions)
**Problem**: Reverse nodes from position m to n.

```cpp
ListNode* reverse_between(ListNode* head, int left, int right) {
    if (!head || left == right) {
        return head;
    }
    
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* prev = dummy;
    
    // Move to node before 'left'
    for (int i = 1; i < left; i++) {
        prev = prev->next;
    }
    
    // Reverse the sublist
    ListNode* current = prev->next;
    ListNode* next = nullptr;
    
    for (int i = 0; i < right - left; i++) {
        next = current->next;
        current->next = next->next;
        next->next = prev->next;
        prev->next = next;
    }
    
    return dummy->next;
}

// Example
// Input:  1 -> 2 -> 3 -> 4 -> 5, left=2, right=4
// Output: 1 -> 4 -> 3 -> 2 -> 5
```

**Visual**:
```
Original: 1 -> 2 -> 3 -> 4 -> 5
             (left)   (right)

Reverse between 2 and 4:
Result:   1 -> 4 -> 3 -> 2 -> 5
```

---

 Example 3: Reverse Nodes in k-Group
**Problem**: Reverse nodes in groups of k.

```cpp
ListNode* reverse_k_group(ListNode* head, int k) {
    // Count nodes
    ListNode* current = head;
    int count = 0;
    while (current && count < k) {
        current = current->next;
        count++;
    }
    
    if (count < k) {
        return head;  // Not enough nodes
    }
    
    // Reverse first k nodes
    ListNode* prev = nullptr;
    current = head;
    for (int i = 0; i < k; i++) {
        ListNode* next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }
    
    // Recursively reverse remaining
    head->next = reverse_k_group(current, k);
    
    return prev;
}

// Example
// Input:  1 -> 2 -> 3 -> 4 -> 5, k=2
// Output: 2 -> 1 -> 4 -> 3 -> 5

// Input:  1 -> 2 -> 3 -> 4 -> 5, k=3
// Output: 3 -> 2 -> 1 -> 4 -> 5
```

**Visual for k=3**:
```
Original: 1 -> 2 -> 3 -> 4 -> 5

Group 1 (size 3): [1,2,3] -> reversed to [3,2,1]
Group 2 (size 2): [4,5] -> too small, unchanged

Result: 3 -> 2 -> 1 -> 4 -> 5
```

---

 Example 4: Swap Nodes in Pairs
**Problem**: Swap every two adjacent nodes.

```cpp
ListNode* swap_pairs(ListNode* head) {
    if (!head || !head->next) {
        return head;
    }
    
    ListNode* dummy = new ListNode(0);
    dummy->next = head;
    ListNode* prev = dummy;
    
    while (head && head->next) {
        ListNode* first = head;
        ListNode* second = head->next;
        
        // Swap
        prev->next = second;
        first->next = second->next;
        second->next = first;
        
        // Move forward
        prev = first;
        head = first->next;
    }
    
    return dummy->next;
}

// Example
// Input:  1 -> 2 -> 3 -> 4
// Output: 2 -> 1 -> 4 -> 3
```

**Visual**:
```
Original: 1 -> 2 -> 3 -> 4

Swap (1,2): 2 -> 1 -> 3 -> 4
Swap (3,4): 2 -> 1 -> 4 -> 3
```

---

 Example 5: Reverse Alternating k-Group
**Problem**: Reverse every alternating k nodes.

```cpp
ListNode* reverse_alternating_k(ListNode* head, int k) {
    if (!head || k <= 1) {
        return head;
    }
    
    ListNode* current = head;
    ListNode* prev = nullptr;
    
    while (current) {
        ListNode* last_node_of_prev = prev;
        ListNode* last_node_of_sublist = current;
        
        // Reverse k nodes
        for (int i = 0; i < k && current; i++) {
            ListNode* next = current->next;
            current->next = prev;
            prev = current;
            current = next;
        }
        
        // Connect with previous part
        if (last_node_of_prev) {
            last_node_of_prev->next = prev;
        } else {
            head = prev;
        }
        
        last_node_of_sublist->next = current;
        
        // Skip k nodes
        for (int i = 0; i < k && current; i++) {
            prev = current;
            current = current->next;
        }
    }
    
    return head;
}

// Example
// Input:  1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8, k=2
// Output: 2 -> 1 -> 3 -> 4 -> 6 -> 5 -> 7 -> 8
//         [reversed] [skip] [reversed] [skip]
```

---

 Example 6: Rotate List
**Problem**: Rotate list to the right by k places.

```cpp
ListNode* rotate_right(ListNode* head, int k) {
    if (!head || !head->next || k == 0) {
        return head;
    }
    
    // Find length and connect end to head (make circular)
    ListNode* last = head;
    int length = 1;
    while (last->next) {
        last = last->next;
        length++;
    }
    last->next = head;  // Make circular
    
    // Find new tail
    k = k % length;  // Handle k > length
    int steps_to_new_tail = length - k;
    
    ListNode* new_tail = head;
    for (int i = 1; i < steps_to_new_tail; i++) {
        new_tail = new_tail->next;
    }
    
    ListNode* new_head = new_tail->next;
    new_tail->next = nullptr;  // Break circle
    
    return new_head;
}

// Example
// Input:  1 -> 2 -> 3 -> 4 -> 5, k=2
// Output: 4 -> 5 -> 1 -> 2 -> 3
```

---

 Time & Space Complexity
- **Time**: O(n) - single pass through list
- **Space**: O(1) - only using pointers

This is better than:
- Creating new list: O(n) space
- Using stack: O(n) space

---

 Common Patterns

 Basic Reversal (3 pointers)
```cpp
ListNode* prev = nullptr;
ListNode* current = head;
while (current) {
    ListNode* next = current->next;
    current->next = prev;
    prev = current;
    current = next;
}
return prev;
```

 Dummy Node Technique
```cpp
ListNode* dummy = new ListNode(0);
dummy->next = head;
// Work with dummy->next
return dummy->next;
```

 Finding kth Node
```cpp
ListNode* node = head;
for (int i = 1; i < k && node; i++) {
    node = node->next;
}
```

---

 Tips & Tricks

1. **Use dummy node** for edge cases (empty list, single node)
2. **Three pointers**: prev, current, next
3. **Save next**: Always save `next` before changing `current->next`
4. **Draw it out**: Visualize pointer changes on paper
5. **Check null**: Always check if nodes exist before accessing
6. **Return prev**: After reversal, `prev` is the new head

---

 Practice Problems

1. **Easy**: Reverse Linked List (LeetCode 206)
2. **Medium**: Reverse Linked List II (LeetCode 92)
3. **Hard**: Reverse Nodes in k-Group (LeetCode 25)
4. **Easy**: Swap Nodes in Pairs (LeetCode 24)
5. **Medium**: Rotate List (LeetCode 61)
6. **Medium**: Reorder List (LeetCode 143)
7. **Medium**: Reverse Alternating k-Element Sublist (Educational)

---

 Key Takeaways
- ✅ Use three pointers: prev, current, next
- ✅ Always save next before changing pointers
- ✅ O(1) space - in-place reversal
- ✅ Dummy node helps with edge cases
- ✅ Draw diagrams to visualize pointer changes
- ✅ Check for null before accessing next
