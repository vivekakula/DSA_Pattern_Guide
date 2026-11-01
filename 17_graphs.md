# Graph Patterns 🕸️

## In One Sentence
A graph represents things as nodes and the relationships between them as edges.

For example, people can be nodes and friendships can be edges. Edges may be one-way or two-way, and may have costs. Unlike a tree, a graph can contain cycles or separate groups, so traversal usually needs a `visited` set.

---

## Graph Vocabulary

| Term | Meaning |
|------|---------|
| **Node / Vertex** | A point in the graph |
| **Edge** | A connection between two nodes |
| **Directed** | Edges have a direction (one-way road) |
| **Undirected** | Edges go both ways (two-way road) |
| **Weighted** | Edges have a cost (toll road) |
| **Cycle** | A path that returns to its starting node |
| **Connected** | Every node can reach every other node |
| **Component** | A group of connected nodes isolated from others |
| **Degree** | Number of edges a node has |
| **In-degree** | For directed graphs: edges coming IN to a node |

---

 How Graphs Are Stored

 Adjacency List (Use This)
```cpp
// n nodes, edges as pairs
int n = 5;
vector<vector<int>> adj(n);  // adj[u] = list of neighbors of u

// Add edge u -> v (directed)
adj[u].push_back(v);

// Add edge u <-> v (undirected)
adj[u].push_back(v);
adj[v].push_back(u);
```

 Adjacency List with Weights
```cpp
// adj[u] = {v, weight} pairs
vector<vector<pair<int,int>>> adj(n);
adj[u].push_back({v, weight});
```

**Why adjacency list?** Space O(V + E) vs adjacency matrix O(V²). Almost always preferred.

---

 Pattern 1: BFS on Graphs

## The Big Idea (Graph BFS vs Tree BFS)
Same queue logic, BUT you must track **visited** nodes to avoid infinite loops in cycles.

**Template**:
```cpp
void bfs(int start, vector<vector<int>>& adj, int n) {
    vector<bool> visited(n, false);
    queue<int> q;

    visited[start] = true;
    q.push(start);

    while (!q.empty()) {
        int node = q.front();
        q.pop();

        // Process node
        cout << node << " ";

        for (int neighbor : adj[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```

**Step-by-step trace** for graph: `0-1, 0-2, 1-3, 2-3`, starting at 0:

| Step | Queue | Visited | Node popped | Neighbors pushed |
|------|-------|---------|-------------|-----------------|
| Start | [0] | {0} | — | — |
| 1 | [1, 2] | {0,1,2} | 0 | 1, 2 |
| 2 | [2, 3] | {0,1,2,3} | 1 | 3 (2 already visited) |
| 3 | [3] | {0,1,2,3} | 2 | none (3 already visited) |
| 4 | [] | {0,1,2,3} | 3 | none |

**Key insight**: Mark visited BEFORE pushing to queue, not after popping. Marking after popping causes the same node to be pushed multiple times.

> **Try it yourself**: Add edge `1-2` to the graph above. Does the BFS output change? Does the visited set change?

---

 Example 1: Number of Provinces (Connected Components)
**Problem**: Count disconnected groups of nodes (LeetCode 547).

```cpp
int findCircleNum(vector<vector<int>>& isConnected) {
    int n = isConnected.size();
    vector<bool> visited(n, false);
    int provinces = 0;

    auto bfs = [&](int start) {
        queue<int> q;
        visited[start] = true;
        q.push(start);
        while (!q.empty()) {
            int node = q.front(); q.pop();
            for (int j = 0; j < n; j++) {
                if (isConnected[node][j] == 1 && !visited[j]) {
                    visited[j] = true;
                    q.push(j);
                }
            }
        }
    };

    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            bfs(i);       // Each BFS call covers one full component
            provinces++;  // One new disconnected group found
        }
    }

    return provinces;
}
```

**Pattern**: "For each unvisited node, run BFS/DFS and count how many times you had to start fresh."

> **Try it yourself**: What happens if ALL nodes are connected? What if NO nodes are connected (no edges)?

---

 Example 2: Rotten Oranges (Multi-source BFS)
**Problem**: All rotten oranges rot neighbors each minute. Find minimum minutes to rot all (LeetCode 994).

```cpp
int orangesRotting(vector<vector<int>>& grid) {
    int rows = grid.size(), cols = grid[0].size();
    queue<pair<int,int>> q;
    int fresh = 0;

    // Add ALL rotten oranges to queue at once (multi-source BFS)
    for (int r = 0; r < rows; r++) {
        for (int c = 0; c < cols; c++) {
            if (grid[r][c] == 2) q.push({r, c});
            if (grid[r][c] == 1) fresh++;
        }
    }

    if (fresh == 0) return 0;

    vector<pair<int,int>> dirs = {{0,1},{0,-1},{1,0},{-1,0}};
    int minutes = 0;

    while (!q.empty() && fresh > 0) {
        minutes++;
        int level_size = q.size();

        for (int i = 0; i < level_size; i++) {
            auto [r, c] = q.front(); q.pop();
            for (auto [dr, dc] : dirs) {
                int nr = r + dr, nc = c + dc;
                if (nr >= 0 && nr < rows && nc >= 0 && nc < cols
                    && grid[nr][nc] == 1) {
                    grid[nr][nc] = 2;
                    fresh--;
                    q.push({nr, nc});
                }
            }
        }
    }

    return fresh == 0 ? minutes : -1;
}
```

**Key insight**: Start BFS from ALL rotten oranges simultaneously — this is the "multi-source BFS" trick. It naturally finds the minimum time because BFS explores by distance.

---

 Pattern 2: DFS on Graphs

**Template**:
```cpp
void dfs(int node, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;

    // Process node
    cout << node << " ";

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            dfs(neighbor, adj, visited);
        }
    }
}
```

---

 Example 3: Detect Cycle in Undirected Graph
**Problem**: Check if an undirected graph has a cycle (LeetCode 684).

```cpp
bool dfs(int node, int parent, vector<vector<int>>& adj, vector<bool>& visited) {
    visited[node] = true;

    for (int neighbor : adj[node]) {
        if (!visited[neighbor]) {
            if (dfs(neighbor, node, adj, visited)) return true;
        } else if (neighbor != parent) {
            // Visited neighbor that is NOT our parent = cycle!
            return true;
        }
    }
    return false;
}

bool hasCycle(int n, vector<vector<int>>& adj) {
    vector<bool> visited(n, false);
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            if (dfs(i, -1, adj, visited)) return true;
        }
    }
    return false;
}
```

**Why `neighbor != parent`?** In an undirected graph, every edge goes both ways. If you're at node 1 which came from node 0, seeing node 0 again is normal — it's your parent. If you see any OTHER already-visited node, that's a real cycle.

---

 Pattern 3: Topological Sort ⭐ (Most Asked in Interviews)

## The Big Idea
Order tasks so that all prerequisites come before the task. Only works on **Directed Acyclic Graphs (DAGs)**.

**Real-world**: Build order of software packages. Course prerequisites. Task scheduling.

**Keywords**: "Prerequisites", "ordering", "dependency", "course schedule"

 Method: Kahn's Algorithm (BFS approach — easier to understand)

1. Calculate in-degree (number of incoming edges) for each node
2. Start with all nodes that have in-degree = 0 (no prerequisites)
3. Process them: for each neighbor, reduce its in-degree by 1
4. When a neighbor's in-degree becomes 0, it's ready — add to queue

```cpp
vector<int> topologicalSort(int n, vector<vector<int>>& prerequisites) {
    vector<vector<int>> adj(n);
    vector<int> in_degree(n, 0);

    // Build graph
    for (auto& pre : prerequisites) {
        int course = pre[0], prereq = pre[1];
        adj[prereq].push_back(course);  // prereq -> course
        in_degree[course]++;
    }

    // Start with nodes that have no prerequisites
    queue<int> q;
    for (int i = 0; i < n; i++) {
        if (in_degree[i] == 0) q.push(i);
    }

    vector<int> order;

    while (!q.empty()) {
        int node = q.front(); q.pop();
        order.push_back(node);

        for (int neighbor : adj[node]) {
            in_degree[neighbor]--;
            if (in_degree[neighbor] == 0) {
                q.push(neighbor);  // All prerequisites done!
            }
        }
    }

    return order;  // If order.size() != n, there's a cycle (impossible to finish!)
}
```

**Step-by-step trace** for `courses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]`:
```
Graph: 0->1, 0->2, 1->3, 2->3

In-degrees: [0:0, 1:1, 2:1, 3:2]

Step 1: Queue = [0] (in-degree 0)
  Pop 0, order=[0]
  Reduce 1's in-degree: 1->0, push 1
  Reduce 2's in-degree: 2->0, push 2
  Queue = [1, 2]

Step 2: Pop 1, order=[0,1]
  Reduce 3's in-degree: 3->1
  Queue = [2]

Step 3: Pop 2, order=[0,1,2]
  Reduce 3's in-degree: 3->0, push 3
  Queue = [3]

Step 4: Pop 3, order=[0,1,2,3] ✅
```

> **Try it yourself**: Add edge `3->0` to create a cycle. Run through the algorithm. What happens to `order.size()`?

---

 Example 4: Course Schedule (Can You Finish?)  — LeetCode 207
**Problem**: Given prerequisites, can you finish all courses?

```cpp
bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
    vector<vector<int>> adj(numCourses);
    vector<int> in_degree(numCourses, 0);

    for (auto& pre : prerequisites) {
        adj[pre[1]].push_back(pre[0]);
        in_degree[pre[0]]++;
    }

    queue<int> q;
    for (int i = 0; i < numCourses; i++) {
        if (in_degree[i] == 0) q.push(i);
    }

    int completed = 0;
    while (!q.empty()) {
        int node = q.front(); q.pop();
        completed++;
        for (int neighbor : adj[node]) {
            if (--in_degree[neighbor] == 0) q.push(neighbor);
        }
    }

    // If we completed all courses, no cycle exists
    return completed == numCourses;
}
```

---

 Pattern 4: Shortest Path — Dijkstra's Algorithm ⭐

## The Big Idea
Find shortest path from a source to all other nodes in a **weighted** graph (non-negative weights only).

**Think of it as**: BFS, but instead of a regular queue we use a **min-heap** to always process the closest unvisited node next.

**Keywords**: "Minimum cost", "cheapest path", "shortest weighted path", "network delay"

```cpp
vector<int> dijkstra(int src, int n, vector<vector<pair<int,int>>>& adj) {
    // dist[i] = shortest distance from src to i
    vector<int> dist(n, INT_MAX);
    dist[src] = 0;

    // Min-heap: {distance, node}
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;
    pq.push({0, src});

    while (!pq.empty()) {
        auto [d, node] = pq.top(); pq.pop();

        // Skip if we already found a better path
        if (d > dist[node]) continue;

        for (auto [neighbor, weight] : adj[node]) {
            int new_dist = dist[node] + weight;
            if (new_dist < dist[neighbor]) {
                dist[neighbor] = new_dist;
                pq.push({new_dist, neighbor});
            }
        }
    }

    return dist;  // dist[i] = minimum distance from src to i
}
```

**Step-by-step trace** for graph: `0->(1,4), 0->(2,1), 2->(1,2)`, source=0:

| Heap top | dist[] | Action |
|----------|--------|--------|
| {0,0} | [0, ∞, ∞] | Process 0: update 1→4, 2→1 |
| {1,2} | [0, 4, 1] | Process 2: update 1→min(4,1+2)=3 |
| {3,1} | [0, 3, 1] | Process 1: no better paths |
| done | [0, 3, 1] | ✅ Shortest paths found |

> **Try it yourself**: Swap the weights (0→1 costs 2, 0→2 costs 4). What does `dist` look like now?

---

 Example 5: Network Delay Time — LeetCode 743
**Problem**: Find minimum time for signal to reach all nodes.

```cpp
int networkDelayTime(vector<vector<int>>& times, int n, int k) {
    vector<vector<pair<int,int>>> adj(n + 1);
    for (auto& t : times) {
        adj[t[0]].push_back({t[1], t[2]});
    }

    vector<int> dist(n + 1, INT_MAX);
    dist[k] = 0;

    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;
    pq.push({0, k});

    while (!pq.empty()) {
        auto [d, node] = pq.top(); pq.pop();
        if (d > dist[node]) continue;
        for (auto [neighbor, weight] : adj[node]) {
            if (dist[node] + weight < dist[neighbor]) {
                dist[neighbor] = dist[node] + weight;
                pq.push({dist[neighbor], neighbor});
            }
        }
    }

    int max_dist = *max_element(dist.begin() + 1, dist.end());
    return max_dist == INT_MAX ? -1 : max_dist;
}
```

---

 Pattern 5: Union-Find (Disjoint Set)

## The Big Idea
Efficiently answer: "Are these two nodes in the same connected component?" and "Connect these two nodes."

**Keywords**: "Connected", "same group", "cycle in undirected graph", "number of components"

```cpp
struct UnionFind {
    vector<int> parent, rank;

    UnionFind(int n) : parent(n), rank(n, 0) {
        iota(parent.begin(), parent.end(), 0);  // parent[i] = i
    }

    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);  // Path compression
        return parent[x];
    }

    bool unite(int x, int y) {
        int px = find(x), py = find(y);
        if (px == py) return false;  // Already connected — this edge creates a cycle!

        // Union by rank
        if (rank[px] < rank[py]) swap(px, py);
        parent[py] = px;
        if (rank[px] == rank[py]) rank[px]++;
        return true;
    }

    bool connected(int x, int y) {
        return find(x) == find(y);
    }
};
```

**Trace** for nodes {0,1,2,3,4}, edges: {0-1, 1-2, 3-4}:
```
Initial: parent = [0, 1, 2, 3, 4]

unite(0,1): parent[1] = 0  →  [0, 0, 2, 3, 4]
unite(1,2): find(1)=0, parent[2] = 0  →  [0, 0, 0, 3, 4]
unite(3,4): parent[4] = 3  →  [0, 0, 0, 3, 3]

connected(0,2)? find(0)=0, find(2)=0 → YES ✅
connected(0,3)? find(0)=0, find(3)=3 → NO ✅
```

---

 After Solving, Ask Yourself

For every graph problem, answer these before moving on:

1. **Is the graph directed or undirected?** This changes cycle detection logic completely.
2. **What do I need?** Shortest path → Dijkstra's. Order tasks → Topo Sort. Count groups → BFS/DFS + counter. Detect cycle → Union-Find or DFS with color.
3. **Did I mark nodes visited BEFORE pushing** to the queue (not after popping)?

> **Tutor's rule**: Graph problems look intimidating because they combine multiple ideas. Break every graph problem into: (1) How is it stored? (2) Which traversal? (3) What am I tracking? Answer these three, and the code writes itself.

---

 Practice Problems (Striver Sheet Order)

 Must-Solve (Interview Frequent)
1. **BFS**: Number of Provinces (LeetCode 547)
2. **BFS**: Rotten Oranges (LeetCode 994)
3. **DFS**: Flood Fill (LeetCode 733)
4. **DFS**: Detect Cycle in Undirected Graph (LeetCode 684)
5. **Topo Sort**: Course Schedule (LeetCode 207)
6. **Topo Sort**: Course Schedule II (LeetCode 210)
7. **Dijkstra**: Network Delay Time (LeetCode 743)
8. **Dijkstra**: Path with Minimum Effort (LeetCode 1631)
9. **Union-Find**: Number of Connected Components (LeetCode 323)
10. **Union-Find**: Redundant Connection (LeetCode 684)

 Good to Know
11. Bipartite Graph Check (LeetCode 785)
12. Alien Dictionary (LeetCode 269)
13. Cheapest Flights within K Stops (LeetCode 787)

---

 Key Takeaways
- ✅ Use **BFS** for shortest path in unweighted graphs, level-by-level problems
- ✅ Use **DFS** for cycle detection, connected components, all paths
- ✅ Use **Topological Sort** for ordering with dependencies (DAG only)
- ✅ Use **Dijkstra** for shortest path in weighted graphs (non-negative weights)
- ✅ Use **Union-Find** for dynamic connectivity, cycle detection in undirected graphs
- ⚠️ Always track `visited` — the #1 bug in graph problems
