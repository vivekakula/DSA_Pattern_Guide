# Fast & Slow Pointers Pattern 🐇🐢

## The Big Idea
Use two pointers moving at **different speeds** through a linked list or sequence. The fast pointer moves 2x as fast as the slow pointer.

**Why it works**: When there's a cycle, the fast pointer will eventually catch up to the slow pointer. For finding middle, when fast reaches end, slow is at middle.

---

 When to Use
- **Linked list cycle** detection
- Finding **middle** of linked list
- Finding **start of cycle**
- **Happy number** problems
- Any problem where you need to meet at some point

**Keywords to spot**:
- "Detect cycle"
- "Find middle of linked list"
- "Happy number"
- "Linked list"
- "Start of cycle"

---

 The Template

```cpp
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

ListNode* fast_slow_pattern(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;        // Move 1 step
        fast = fast->next->next;  // Move 2 steps
        
        if (slow == fast) {
            // They met - do something
            break;
        }
    }
    
    return slow;  // or whatever you need
}
```

---

 Example 1: Detect Cycle in Linked List
**Problem**: Determine if a linked list has a cycle.

```cpp
bool has_cycle(ListNode* head) {
    if (!head || !head->next) {
        return false;
    }
    
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        
        if (slow == fast) {
            return true;  // Cycle detected!
        }
    }
    
    return false;  // Fast reached end, no cycle
}

// Example
// 1 -> 2 -> 3 -> 4
//      ^         |
//      |_________|
// has_cycle(head) = true
```

**Why it works**: 
- If there's a cycle, fast will eventually catch up to slow
- If no cycle, fast will reach the end (nullptr)
- It's like two runners on a circular track - the faster one will lap the slower one

---

 Example 2: Find Middle of Linked List
**Problem**: Find the middle node of a linked list.

```cpp
ListNode* find_middle(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return slow;  // Slow is at middle
}

// Example
// 1 -> 2 -> 3 -> 4 -> 5
// When fast is at 5, slow is at 3
```

**Visual**:
```
Start: S,F at 1
1 -> 2 -> 3 -> 4 -> 5
S F

Step 1:
1 -> 2 -> 3 -> 4 -> 5
     S         F

Step 2:
1 -> 2 -> 3 -> 4 -> 5
          S              F (null)
          
Slow is at middle!
```

---

 Example 3: Find Start of Cycle
**Problem**: If there's a cycle, find where it begins.

```cpp
ListNode* find_cycle_start(ListNode* head) {
    ListNode* slow = head;
    ListNode* fast = head;
    
    // Step 1: Detect if cycle exists
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        
        if (slow == fast) {
            break;  // Cycle detected
        }
    }
    
    // No cycle
    if (!fast || !fast->next) {
        return nullptr;
    }
    
    // Step 2: Find cycle start
    // Move slow to head, keep fast at meeting point
    slow = head;
    
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;  // Both move 1 step now
    }
    
    return slow;  // This is the cycle start
}
```

**Why it works**:
- Mathematical proof: Distance from head to cycle start = distance from meeting point to cycle start
- When they meet again (moving at same speed), that's the cycle start!

---

 Example 4: Happy Number
**Problem**: A happy number is defined by repeatedly replacing with sum of squares of digits, ending at 1. Detect if number is happy or cycles forever.

```cpp
int get_next(int n) {
    int sum = 0;
    while (n > 0) {
        int digit = n % 10;
        sum += digit * digit;
        n /= 10;
    }
    return sum;
}

bool is_happy(int n) {
    int slow = n;
    int fast = n;
    
    do {
        slow = get_next(slow);              // Move 1 step
        fast = get_next(get_next(fast));    // Move 2 steps
        
        if (fast == 1) {
            return true;  // Happy number!
        }
    } while (slow != fast);
    
    return false;  // Caught in cycle, not happy
}

// Example
// 19 -> 82 -> 68 -> 100 -> 1 (Happy!)
// 2 -> 4 -> 16 -> 37 -> 58 -> 89 -> 145 -> 42 -> 20 -> 4 (Cycle!)
```

---

 Common Variations

 Find Nth Node from End
```cpp
ListNode* nth_from_end(ListNode* head, int n) {
    ListNode* fast = head;
    ListNode* slow = head;
    
    // Move fast n steps ahead
    for (int i = 0; i < n; i++) {
        fast = fast->next;
    }
    
    // Move both until fast reaches end
    while (fast) {
        slow = slow->next;
        fast = fast->next;
    }
    
    return slow;
}
```

 Palindrome Linked List
```cpp
bool is_palindrome(ListNode* head) {
    // Find middle using fast & slow
    ListNode* slow = head;
    ListNode* fast = head;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    // Reverse second half (starting from slow)
    ListNode* second_half = reverse(slow);
    
    // Compare first half with reversed second half
    ListNode* p1 = head;
    ListNode* p2 = second_half;
    
    while (p2) {
        if (p1->val != p2->val) {
            return false;
        }
        p1 = p1->next;
        p2 = p2->next;
    }
    
    return true;
}
```

---

 Time & Space Complexity
- **Time**: O(n) - traverse list once
- **Space**: O(1) - only using two pointers!

This is better than using a hash set which would take O(n) space.

---

 Tips & Tricks

1. **Always check for null**: Check `fast && fast->next` before moving fast pointer
2. **Cycle detection**: If fast catches slow, there's a cycle
3. **Finding middle**: When fast reaches end, slow is at middle
4. **Off by one**: For even-length lists, slow will be at start of second half
5. **Speed ratio**: Usually 2:1, but can be adjusted for different problems

---

 Practice Problems

1. **Easy**: Linked List Cycle (LeetCode 141)
2. **Easy**: Middle of the Linked List (LeetCode 876)
3. **Easy**: Happy Number (LeetCode 202)
4. **Medium**: Linked List Cycle II (LeetCode 142)
5. **Medium**: Find the Duplicate Number (LeetCode 287)
6. **Easy**: Remove Nth Node From End (LeetCode 19)
7. **Easy**: Palindrome Linked List (LeetCode 234)

---

 Key Takeaways
- ✅ Use for cycle detection in linked lists
- ✅ Use for finding middle element
- ✅ Space efficient: O(1) instead of O(n)
- ✅ Works because of speed difference
- ✅ Always check for null pointers
