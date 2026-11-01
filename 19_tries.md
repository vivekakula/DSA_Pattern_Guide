# Trie (Prefix Tree) Pattern 🌳

## In One Sentence
A trie stores words by sharing the nodes for prefixes they have in common.

To look up `apple`, follow the `a-p-p-l-e` path. A marker on the last node tells you whether that path is a complete word. A trie is especially useful for prefix searches such as “does any word start with `app`?”

---

## When to Use
- **Autocomplete** / search suggestions
- **Prefix matching** ("starts with")
- **Word search** problems on grids
- **IP routing** / dictionary lookups
- Counting words with a given prefix

**Keywords to spot**:
- "Implement autocomplete"
- "Count words with prefix"
- "Search words with wildcards"
- "Word search in board"
- "Prefix"
- "Dictionary"

---

 The Trie Node Structure

```cpp
struct TrieNode {
    TrieNode* children[26];
    bool is_end;  // true if a complete word ends here

    TrieNode() : is_end(false) {
        fill(children, children + 26, nullptr);
    }
};
```

**Visual for words "app", "apple", "apt"**:
```
root
 └── a
      └── p
           ├── p  [end=true]  ← "app"
           │    └── l
           │         └── e  [end=true]  ← "apple"
           └── t  [end=true]  ← "apt"
```

Each node = one character. `is_end=true` marks complete words.

---

 The Template: Full Trie Class

```cpp
class Trie {
private:
    TrieNode* root;

public:
    Trie() {
        root = new TrieNode();
    }

    // Insert word into trie — O(length)
    void insert(string word) {
        TrieNode* node = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!node->children[idx]) {
                node->children[idx] = new TrieNode();
            }
            node = node->children[idx];
        }
        node->is_end = true;  // Mark end of word
    }

    // Search for exact word — O(length)
    bool search(string word) {
        TrieNode* node = root;
        for (char c : word) {
            int idx = c - 'a';
            if (!node->children[idx]) return false;  // Path doesn't exist
            node = node->children[idx];
        }
        return node->is_end;  // Must be marked as complete word
    }

    // Check if any word starts with prefix — O(length)
    bool startsWith(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            int idx = c - 'a';
            if (!node->children[idx]) return false;
            node = node->children[idx];
        }
        return true;  // Path exists (don't care about is_end)
    }
};
```

**Key difference: `search` vs `startsWith`**
- `search("app")` → must reach the 'p' node AND it must have `is_end=true`
- `startsWith("app")` → just needs to reach the 'p' node (any word that passes through here qualifies)

---

 Example 1: Implement Trie — LeetCode 208

```cpp
// Usage example
Trie trie;
trie.insert("apple");
trie.search("apple");    // true
trie.search("app");      // false (not inserted as complete word)
trie.startsWith("app");  // true (apple starts with app)
trie.insert("app");
trie.search("app");      // true (now inserted)
```

**Step-by-step trace** — inserting "cat":
```
Start at root

c: root->children['c'-'a'] = nullptr → create new node, move to it
a: node->children['a'-'a'] = nullptr → create new node, move to it
t: node->children['t'-'a'] = nullptr → create new node, move to it

Mark current node is_end = true

Tree now has path: root → c → a → t[end]
```

> **Try it yourself**: Insert "car" after "cat". Draw the tree. Which nodes are shared between "cat" and "car"?

---

 Example 2: Word Search II (Multiple Words on Grid) — LeetCode 212 ⭐
**Problem**: Given a grid of letters and a list of words, find all words present in the grid.

**Why Trie?** Searching for each word independently with DFS is too slow. A Trie lets you search for ALL words simultaneously — when you're at a prefix that no word starts with, you stop early.

```cpp
class Solution {
    struct TrieNode {
        TrieNode* children[26] = {};
        string word = "";  // Store full word at end node
    };

    void insert(TrieNode* root, string& word) {
        TrieNode* node = root;
        for (char c : word) {
            int i = c - 'a';
            if (!node->children[i]) node->children[i] = new TrieNode();
            node = node->children[i];
        }
        node->word = word;
    }

    void dfs(vector<vector<char>>& board, int r, int c,
             TrieNode* node, vector<string>& result) {
        if (r < 0 || r >= board.size() || c < 0 || c >= board[0].size())
            return;

        char ch = board[r][c];
        if (ch == '#' || !node->children[ch - 'a']) return;  // Already visited or no path

        node = node->children[ch - 'a'];

        if (!node->word.empty()) {
            result.push_back(node->word);
            node->word = "";  // Avoid duplicates
        }

        board[r][c] = '#';  // Mark visited
        dfs(board, r+1, c, node, result);
        dfs(board, r-1, c, node, result);
        dfs(board, r, c+1, node, result);
        dfs(board, r, c-1, node, result);
        board[r][c] = ch;  // Restore
    }

public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        TrieNode* root = new TrieNode();
        for (string& w : words) insert(root, w);

        vector<string> result;
        for (int r = 0; r < board.size(); r++) {
            for (int c = 0; c < board[0].size(); c++) {
                dfs(board, r, c, root, result);
            }
        }
        return result;
    }
};
```

**Why `board[r][c] = '#'`?** Marks the cell as visited within the current DFS path. Restored after DFS so other paths can use it.

---

 Example 3: Count Words with Given Prefix
**Problem**: Given a list of words and a prefix, count how many words start with the prefix.

```cpp
// Trie with count at each node
struct TrieNode {
    TrieNode* children[26] = {};
    int count = 0;  // How many words pass through this node
};

class PrefixCounter {
    TrieNode* root = new TrieNode();

public:
    void insert(string word) {
        TrieNode* node = root;
        for (char c : word) {
            int i = c - 'a';
            if (!node->children[i]) node->children[i] = new TrieNode();
            node = node->children[i];
            node->count++;  // Increment for every word that passes through
        }
    }

    int countWithPrefix(string prefix) {
        TrieNode* node = root;
        for (char c : prefix) {
            int i = c - 'a';
            if (!node->children[i]) return 0;
            node = node->children[i];
        }
        return node->count;  // All words that reached this prefix node
    }
};

// Example:
// Insert: "apple", "app", "ape", "banana"
// countWithPrefix("ap") → 3 (apple, app, ape)
// countWithPrefix("ban") → 1 (banana)
// countWithPrefix("xyz") → 0
```

---

 Example 4: Search with Wildcard ('.' matches any letter) — LeetCode 211

```cpp
class WordDictionary {
    struct TrieNode {
        TrieNode* children[26] = {};
        bool is_end = false;
    };

    TrieNode* root = new TrieNode();

    bool dfs(string& word, int i, TrieNode* node) {
        if (i == word.size()) return node->is_end;

        char c = word[i];
        if (c == '.') {
            // Try all 26 children
            for (int j = 0; j < 26; j++) {
                if (node->children[j] && dfs(word, i + 1, node->children[j]))
                    return true;
            }
            return false;
        } else {
            int idx = c - 'a';
            if (!node->children[idx]) return false;
            return dfs(word, i + 1, node->children[idx]);
        }
    }

public:
    void addWord(string word) {
        TrieNode* node = root;
        for (char c : word) {
            int i = c - 'a';
            if (!node->children[i]) node->children[i] = new TrieNode();
            node = node->children[i];
        }
        node->is_end = true;
    }

    bool search(string word) {
        return dfs(word, 0, root);
    }
};

// Example:
// addWord("bad"), addWord("dad"), addWord("mad")
// search("pad") → false
// search(".ad") → true  ('.' matches b, d, or m)
// search("b..") → true  (matches "bad")
```

---

 Time & Space Complexity

| Operation | Time | Space |
|-----------|------|-------|
| Insert word of length L | O(L) | O(L × 26) worst case |
| Search word of length L | O(L) | O(1) |
| StartsWith prefix length L | O(L) | O(1) |
| Total space for n words avg length L | — | O(n × L × 26) |

**Compare to hash set**: HashSet gives O(1) search but O(n × L) for prefix queries. Trie gives O(L) for both exact and prefix search.

---

 After Solving, Ask Yourself

1. **Do I need prefix search or exact search?** If only exact, a hash set is simpler. Use Trie when prefix matters.
2. **What extra info do I need per node?** Word count? Full word string? End marker only?
3. **Grid + words problem?** Almost certainly Trie + DFS. The Trie prunes paths that can't lead to any word.

> **Tutor's rule**: To truly own the Trie, implement it from scratch once — without looking. `insert` then `search` then `startsWith`. If you can write those 3 methods from memory, you know Tries.

---

 Practice Problems

 Must-Solve
1. **Medium**: Implement Trie (LeetCode 208) — **Start here, do this first**
2. **Medium**: Add and Search Word (LeetCode 211)
3. **Hard**: Word Search II (LeetCode 212)

 Good to Know
4. Longest Word in Dictionary (LeetCode 720)
5. Replace Words (LeetCode 648)
6. Maximum XOR of Two Numbers (LeetCode 421) — Trie on bits

---

 Key Takeaways
- ✅ Trie = tree where paths spell words character by character
- ✅ `is_end` marks complete words; absence means prefix only
- ✅ Always store indices `c - 'a'`, not characters directly
- ✅ `search` checks `is_end`; `startsWith` does not
- ✅ Combine with DFS for grid-based word search problems
