---
Arrays & Hashing: Dynamic Arrays, Hash Usage, Hash Implementation, Prefix Sums
Two Pointers:
Stack: Stacks
Binary Search: Search Array, Search Range
Sliding window: Sliding Window Fixed Size, Variable Size
Linked List: Singly Linked Lists, Doubly Linked Lists, Fast and Slow Pointers
Trees: BST Insert and Remove, Depth-First Search, Breadth-First Search, BST Sets and Maps, Iterative DFS
Tries: Trie
Heap/Priority Queue: Heap Priorities, Push and Pop, Heapify, Two Heaps
Backtracking: Tree Maze, Subsets, Combinations, Permutations
Graphs: Intro to Graphs, Matrix DFS, Matrix BFS, Adjacency List
1-D DP: 1-Dimension DP, Palindromes
Intervals:
Greedy: Kadane's Algorithm
2-D DP: 2-Dimension DP, 0/1 Knapsack, Unbounded Knapsack, LCS
Bit Manipulation: Bit Operations
Advanced Graphs: Djikstra's, Prim's, Kruskal's, Topological Sort
Math & Geography:
---

### Data Structures
---
#### Arrays / Lists
- What is this data structure?
  - A contiguous dynamic array in Python (`list`) with O(1) average append and O(1) index access.
- What is this data structure for?
  - Storing ordered data, scanning, in-place transforms, two-pointer patterns, sorting-based solutions.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Input is a sequence and order/index matters.
  - You need frequent index access or in-place updates.
  - The target complexity is O(n) or O(n log n) with sorting.
- How do I use this data structure in python?
```python
nums = [3, 1, 4]
nums.append(2)
nums.sort()
for i, x in enumerate(nums):
    pass
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Scan + state tracking: one pass with variables/maps.
  - Rearrangement: sort then greedy/two pointers.
  - Prefix accumulation: prefix sums/difference arrays.
- What are example leetcode problems I can solve to practice this?
  - 1. Two Sum
  - 53. Maximum Subarray
  - 238. Product of Array Except Self
  - 56. Merge Intervals

#### Hash Map / Hash Set
- What is this data structure?
  - Hash table dictionaries (`dict`) for key-value and sets (`set`) for unique membership.
- What is this data structure for?
  - O(1) average lookup, counting, deduplication, frequency maps, seen-state checks.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Problem asks for "contains", "seen", "count", "first index", "group by key".
  - Brute force compares many pairs; map can reduce O(n^2) to O(n).
- How do I use this data structure in python?
```python
freq = {}
for x in [1, 2, 2]:
    freq[x] = freq.get(x, 0) + 1
seen = set()
seen.add("abc")
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Pair sum/complement: store needed complement or seen numbers.
  - Grouping: use tuple/string signature keys.
  - De-dup windows: map char -> latest index.
- What are example leetcode problems I can solve to practice this?
  - 1. Two Sum
  - 49. Group Anagrams
  - 128. Longest Consecutive Sequence
  - 347. Top K Frequent Elements

#### Stack
- What is this data structure?
  - Last-in-first-out structure; in Python, list with `.append()` and `.pop()`.
- What is this data structure for?
  - Nested structure parsing, backtracking state, monotonic maintenance, DFS iterative simulation.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Matching brackets/tags, next greater/smaller, undo behavior, recursion-like traversal.
- How do I use this data structure in python?
```python
st = []
st.append('(')
last = st.pop()
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Parentheses validation: push opens, match closes.
  - Monotonic stack: maintain increasing/decreasing order for next element queries.
  - Expression evaluation: operator/operand stacks.
- What are example leetcode problems I can solve to practice this?
  - 20. Valid Parentheses
  - 739. Daily Temperatures
  - 84. Largest Rectangle in Histogram

#### Queue / Deque
- What is this data structure?
  - First-in-first-out queue; `collections.deque` supports O(1) append/pop both ends.
- What is this data structure for?
  - BFS layers, fixed/variable windows, scheduling and stream processing.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - "Nearest/shortest in unweighted graph", "level order", "window slides by one".
- How do I use this data structure in python?
```python
from collections import deque
q = deque([1, 2])
q.append(3)
front = q.popleft()
q.appendleft(0)
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - BFS shortest path in unweighted graph: queue + visited.
  - Monotonic deque window max: maintain decreasing deque of indices.
  - Task processing by order: push new work, pop oldest.
- What are example leetcode problems I can solve to practice this?
  - 102. Binary Tree Level Order Traversal
  - 994. Rotting Oranges
  - 239. Sliding Window Maximum

#### Linked List
- What is this data structure?
  - Node-based structure where each node points to next (and sometimes prev) node.
- What is this data structure for?
  - O(1) insertion/removal given node pointer, pointer manipulation practice.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Input is already a linked list.
  - You need cycle detection, reversing, merge/reorder by pointers without extra arrays.
- How do I use this data structure in python?
```python
# LeetCode provides ListNode
curr = head
while curr:
    curr = curr.next
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Reverse/partition/merge: dummy head + pointer rewiring.
  - Cycle/middle detection: fast and slow pointers.
  - K-group reversal: local pointer reversal in chunks.
- What are example leetcode problems I can solve to practice this?
  - 206. Reverse Linked List
  - 141. Linked List Cycle
  - 21. Merge Two Sorted Lists
  - 143. Reorder List

#### Heap / Priority Queue
- What is this data structure?
  - Binary heap where parent priority dominates children; Python has min-heap via `heapq`.
- What is this data structure for?
  - Repeated access to min/max in O(log n), top-k maintenance, scheduling.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - "k largest/smallest", "always take next best", stream median/top-k updates.
- How do I use this data structure in python?
```python
import heapq
h = []
heapq.heappush(h, 5)
heapq.heappush(h, 2)
smallest = heapq.heappop(h)
# max-heap trick: push negatives
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Top-k: maintain size-k min heap.
  - Merge sorted streams: heap of current heads.
  - Two-heaps median: max-heap lower + min-heap upper.
- What are example leetcode problems I can solve to practice this?
  - 215. Kth Largest Element in an Array
  - 347. Top K Frequent Elements
  - 295. Find Median from Data Stream
  - 973. K Closest Points to Origin

#### Trees / BST
- What is this data structure?
  - Hierarchical node structure with parent-child edges; BST enforces ordered left < root < right.
- What is this data structure for?
  - Hierarchical search, recursive divide-and-conquer, ordered queries in BST.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Input is tree/BST.
  - You see ancestor/path/depth/subtree language.
  - Need sorted order from structure (inorder traversal in BST).
- How do I use this data structure in python?
```python
# LeetCode provides TreeNode

def dfs(node):
    if not node:
        return 0
    return 1 + max(dfs(node.left), dfs(node.right))
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Traversal/aggregation: DFS postorder returns local summaries.
  - Level operations: BFS queue by levels.
  - BST validity/search/range: inorder or boundary constraints.
- What are example leetcode problems I can solve to practice this?
  - 104. Maximum Depth of Binary Tree
  - 98. Validate Binary Search Tree
  - 102. Binary Tree Level Order Traversal
  - 236. Lowest Common Ancestor of a Binary Tree

#### Trie
- What is this data structure?
  - Prefix tree where each edge is a character and nodes represent prefixes.
- What is this data structure for?
  - Fast prefix queries, dictionary word search, autocomplete-style checks.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Repeated prefix matching over many words.
  - You need faster than checking every word each query.
- How do I use this data structure in python?
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end = False
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Insert/search/prefix API: child map traversal.
  - Word search on board: trie + DFS pruning.
  - Replace words by root: stop at first terminal prefix.
- What are example leetcode problems I can solve to practice this?
  - 208. Implement Trie (Prefix Tree)
  - 211. Design Add and Search Words Data Structure
  - 212. Word Search II

#### Graph Representations (Adjacency List / Matrix)
- What is this data structure?
  - Representation of nodes and edges via adjacency list (`dict[list]`) or matrix.
- What is this data structure for?
  - Traversal, connectivity, shortest path, cycle detection, topological ordering.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Entities with pairwise relationships, prerequisites, routes, connected components.
- How do I use this data structure in python?
```python
from collections import defaultdict
graph = defaultdict(list)
for u, v in edges:
    graph[u].append(v)
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Connectivity/components: DFS/BFS + visited.
  - DAG ordering: Kahn indegree BFS or DFS topo.
  - Shortest path: BFS (unweighted), Dijkstra (non-negative weights).
- What are example leetcode problems I can solve to practice this?
  - 200. Number of Islands
  - 133. Clone Graph
  - 207. Course Schedule
  - 743. Network Delay Time

#### Union-Find (Disjoint Set Union)
- What is this data structure?
  - Structure tracking connected components with `find` and `union`.
- What is this data structure for?
  - Dynamic connectivity queries, cycle detection in undirected edges.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Many connectivity checks across edge additions.
  - Need near-O(1) component merges/queries.
- How do I use this data structure in python?
```python
parent = list(range(n))
rank = [0] * n

def find(x):
    if parent[x] != x:
        parent[x] = find(parent[x])
    return parent[x]

def union(a, b):
    ra, rb = find(a), find(b)
    if ra == rb:
        return False
    if rank[ra] < rank[rb]:
        ra, rb = rb, ra
    parent[rb] = ra
    if rank[ra] == rank[rb]:
        rank[ra] += 1
    return True
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Count components after unions.
  - Detect cycle while adding edges.
  - Build MST (Kruskal).
- What are example leetcode problems I can solve to practice this?
  - 684. Redundant Connection
  - 547. Number of Provinces
  - 1584. Min Cost to Connect All Points

#### Monotonic Stack / Monotonic Queue
- What is this data structure?
  - Stack/deque that keeps values in sorted monotonic order of candidates.
- What is this data structure for?
  - Next greater/smaller queries and window extremes in O(n).
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - "Next greater", "previous smaller", "window maximum", linear-time requirement.
- How do I use this data structure in python?
```python
# Monotonic decreasing stack of indices
st = []
for i, x in enumerate(nums):
    while st and nums[st[-1]] < x:
        j = st.pop()
    st.append(i)
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Next warmer day: decreasing stack.
  - Largest histogram rectangle: increasing stack with flush.
  - Sliding max: decreasing deque of indices.
- What are example leetcode problems I can solve to practice this?
  - 739. Daily Temperatures
  - 84. Largest Rectangle in Histogram
  - 239. Sliding Window Maximum

#### Prefix Sum / Difference Array
- What is this data structure?
  - Prefix sum: cumulative totals for O(1) range sum.
  - Difference array: range update trick with endpoint increments.
- What is this data structure for?
  - Fast repeated range queries or batch range updates.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Many subarray sum checks or repeated range operations.
  - Need better than O(n) per query.
- How do I use this data structure in python?
```python
prefix = [0]
for x in nums:
    prefix.append(prefix[-1] + x)
# sum(i..j) = prefix[j + 1] - prefix[i]
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Range sum queries: build prefix once.
  - Subarray sum equals k: hash map on prefix frequencies.
  - Range increment operations: difference + final prefix pass.
- What are example leetcode problems I can solve to practice this?
  - 303. Range Sum Query - Immutable
  - 560. Subarray Sum Equals K
  - 2381. Shifting Letters II

#### Bitmask as a Structure
- What is this data structure?
  - Integer used as compact set/flags representation via bits.
- What is this data structure for?
  - Subset states, toggles, fast membership for small universes.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Universe size small (usually <= 20-26).
  - Frequent subset checks/DP over subsets.
- How do I use this data structure in python?
```python
mask = 0
mask |= 1 << 3     # add 3
has3 = (mask >> 3) & 1
mask ^= 1 << 3     # toggle 3
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - State compression DP (TSP-style, assignment).
  - Character set uniqueness checks.
  - Backtracking with bit constraints.
- What are example leetcode problems I can solve to practice this?
  - 136. Single Number
  - 78. Subsets
  - 1125. Smallest Sufficient Team



### Advanced / Exhaustive Appendix
---

#### Segment Tree
- What is this data structure?
  - Balanced tree over array intervals supporting range query + point/range update.
- What is this data structure for?
  - Dynamic range min/max/sum queries with updates in O(log n).
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Frequent interleaved updates and range queries.
- How do I use this data structure in python?
```python
# Common in contests/interview-hard; implement as array tree of size 4*n.
# Ops: build, query(l, r), update(idx, val)
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Range sum/min/max mutable arrays.
  - Query + update constraints up to 1e5.
- What are example leetcode problems I can solve to practice this?
  - 307. Range Sum Query - Mutable
  - 315. Count of Smaller Numbers After Self

#### Fenwick Tree (Binary Indexed Tree)
- What is this data structure?
  - Compact structure for prefix aggregates with O(log n) update/query.
- What is this data structure for?
  - Prefix sums and inversion/counting tasks with coordinate compression.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Need dynamic prefix counts/sums repeatedly.
- How do I use this data structure in python?
```python
class BIT:
    def __init__(self, n):
        self.n = n
        self.bit = [0] * (n + 1)

    def add(self, i, delta):
        while i <= self.n:
            self.bit[i] += delta
            i += i & -i

    def sum(self, i):
        s = 0
        while i > 0:
            s += self.bit[i]
            i -= i & -i
        return s
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Count smaller elements to left/right.
  - Dynamic prefix sums over mutable frequencies.
- What are example leetcode problems I can solve to practice this?
  - 315. Count of Smaller Numbers After Self
  - 327. Count of Range Sum

#### Ordered Structures via `bisect`
- What is this data structure?
  - Sorted list maintained with binary search insertion (`bisect_left/right`).
- What is this data structure for?
  - Ordered predecessor/successor queries when n is moderate.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Need nearest value/rank in sorted order, updates are not too heavy.
- How do I use this data structure in python?
```python
import bisect
arr = [1, 4, 7]
i = bisect.bisect_left(arr, 5)
arr.insert(i, 5)
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Keep running sorted prefix and query neighbors.
  - Coordinate compress then use BIT/segment tree if too slow.
- What are example leetcode problems I can solve to practice this?
  - 35. Search Insert Position
  - 981. Time Based Key-Value Store

#### Sparse Table / RMQ Context
- What is this data structure?
  - Immutable range query precomputation using powers of two.
- What is this data structure for?
  - O(1) idempotent range queries (min/max/gcd) after O(n log n) build.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Many range queries, array is static, no updates.
- How do I use this data structure in python?
```python
# Build st[k][i] for interval length 2^k; query with two overlapping blocks.
# Usually appears in advanced RMQ/LCA contexts.
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Static RMQ heavy query workloads.
  - LCA reduction to RMQ (advanced).
- What are example leetcode problems I can solve to practice this?
  - 1483. Kth Ancestor of a Tree Node (related lifting idea)
  - 304. Range Sum Query 2D - Immutable (prefix-table mindset)

#### Interval / Event Structures
- What is this data structure?
  - Sorted intervals or event points used with sweep line and active sets/heaps.
- What is this data structure for?
  - Overlap counting, meeting rooms, skyline, merge coverage.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - Interval start/end events and "max overlap" style asks.
- How do I use this data structure in python?
```python
events = []
for s, e in intervals:
    events.append((s, 1))
    events.append((e, -1))
events.sort()
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - Merge by sorting starts.
  - Count overlap by sweep events.
  - Track current minimum end with min-heap.
- What are example leetcode problems I can solve to practice this?
  - 56. Merge Intervals
  - 253. Meeting Rooms II
  - 759. Employee Free Time

#### Advanced Graph Utility Structures
- What is this data structure?
  - Supporting structures: indegree arrays, min-heaps for frontier, DSU for MST, visited state tuples.
- What is this data structure for?
  - Topological sort, shortest path, MST, multi-state BFS/DFS.
- How can I quickly diagnose that I am meant to use this for the optimal solution of a problem?
  - DAG prerequisites, weighted edges, constrained states.
- How do I use this data structure in python?
```python
from collections import deque
import heapq
# indegree + queue (Kahn), or min-heap for Dijkstra frontier
```
- What are the types of questions I can see with this data structure and what are the solutions?
  - DAG order: indegree queue.
  - Weighted shortest path: heap-based Dijkstra.
  - MST: DSU + sorted edges.
- What are example leetcode problems I can solve to practice this?
  - 207. Course Schedule
  - 210. Course Schedule II
  - 743. Network Delay Time
  - 1584. Min Cost to Connect All Points




### Leetcode Problem Types
---


### Arrays and Hashing
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Dynamic Arrays, Hash Usage, Hash Implementation, Prefix Sums.
- Connected structures: `list`, `dict`, `set`, prefix-sum array, counting arrays.

**Term definitions:**
- **Dynamic Array** (`list` in Python): A resizable array that doubles its capacity when full. Amortized O(1) append, O(1) index access, O(n) insert/delete at arbitrary position.
- **Hash Usage**: Using a hash table (`dict` or `set`) to store and retrieve values in average O(1) time by mapping keys through a hash function.
- **Hash Implementation**: The underlying mechanics of a hash table -- hash function, bucket array, and collision resolution (chaining or open addressing). Python `dict` uses open addressing with probing.
- **Prefix Sums**: A precomputed array where `prefix[i] = sum(nums[0..i])`. Lets you compute any subarray sum `nums[l..r]` in O(1) via `prefix[r+1] - prefix[l]`.

#### 2) Subtopic Deep Dives

**Dynamic Arrays**
- *Definition*: A contiguous block of memory that grows by allocating a new, larger block and copying elements when capacity is exceeded.
- *When you encounter it*: Any problem where you build a result list, need random access by index, or iterate in order.
- *Core pattern*: Append to build, index to access. `result = []` then `result.append(x)`.
- *Key insight*: Amortized O(1) append works because doubling capacity means each element is copied O(log n) times total across all resizes, averaging to O(1) per operation.

**Hash Usage**
- *Definition*: Leveraging `dict` or `set` to answer membership, frequency, or mapping queries in average O(1).
- *When you encounter it*: "Find if complement exists," "count occurrences," "group by property," "have we seen this before?"
- *Core pattern*: `seen = {}; for x in data: if condition(x) in seen: answer; seen[x] = info`
- *Key insight*: A hash map trades O(n) space to eliminate an inner loop, turning O(n^2) brute force into O(n).

**Hash Implementation**
- *Definition*: Building a hash table from scratch -- choosing a hash function, sizing the bucket array, and resolving collisions.
- *When you encounter it*: Interview asks you to design a HashMap, or you need to understand why worst-case is O(n) (all keys collide).
- *Core pattern*: `hash(key) % bucket_count` gives the index; store `(key, value)` pairs in a list at that index (chaining).
- *Key insight*: A good hash function distributes keys uniformly. Load factor (elements/buckets) determines when to resize; Python resizes at 2/3 full.

**Prefix Sums**
- *Definition*: A preprocessed array where each element stores the cumulative sum of all elements before it.
- *When you encounter it*: "Subarray sum equals K," "range sum query," "product of array except self."
- *Core pattern*: Build `prefix[0] = 0; prefix[i+1] = prefix[i] + nums[i]`. Query: `sum(l, r) = prefix[r+1] - prefix[l]`.
- *Key insight*: Prefix sums turn any range-sum query from O(n) to O(1) by reducing subtraction to two lookups. When combined with a hash map (storing prefix sum frequencies), you can find subarrays with a target sum in O(n).

#### 3) Key Insight / Mental Model
**The "seen" dictionary is a memory of the past.** As you scan left to right, each element asks: "Has anything I need already appeared?" The hash map answers that question in O(1). Every arrays-and-hashing problem is fundamentally: "What do I need to remember about the elements I have already processed, and how do I look it up instantly?"

#### 4) Fast Recognition Cues
- You need O(1) membership/count while scanning array/string.
- Pair/grouping/dedup language appears ("find two numbers that...", "group all...").
- Brute force is O(n^2), but one-pass state can reduce to O(n).
- Problem says "subarray sum" -- think prefix sums + hash map.
- Problem says "frequency," "most common," or "top K" -- think counting map.
- Problem says "contains duplicate" or "unique" -- think set.
- Problem says "anagram," "permutation," or "rearrange" -- think character frequency signature.

#### 5) When NOT to Use This Pattern
- **Order matters and you need sorted output**: Hashing destroys order. If the answer depends on sorted positions, consider sorting + two pointers instead.
- **Need range queries on mutable data**: Prefix sums are static. If values change between queries, you need a segment tree or BIT, not a prefix array.
- **Problem constraints are tiny (n < 20)**: Brute force or bitmask enumeration may be simpler and sufficient; hashing adds unnecessary complexity.
- **Sliding window signals are present**: If the problem asks for "longest/shortest subarray with property X" on contiguous elements, sliding window is usually more direct than hashing (though some problems use both).

#### 6) Universal Solve Framework
1. **Identify if order matters or only counts/membership matter.** If you only care about existence or frequency, a set or counting dict is your tool. If index positions matter, store indices as values in your dict.
2. **Choose the map key.** Common choices: the value itself (Two Sum), a canonical signature like sorted string or frequency tuple (Group Anagrams), a prefix sum (Subarray Sum Equals K), or `(row, col)` tuples (Valid Sudoku).
3. **Write a one-pass invariant.** State clearly: "After processing index i, the map contains ___." For Two Sum: "After processing index i, `seen` maps every value in `nums[0..i]` to its index." This invariant guarantees correctness.
4. **Confirm edge cases are handled.** Collisions (two elements with same value), duplicates (should you overwrite or skip?), negative numbers (prefix sums still work), empty input, single-element input.

#### 7) Common Mistakes & Pitfalls
1. **Overwriting index too early (Two Sum)**: If you store `seen[x] = i` before checking for the complement, you might match an element with itself. Always check first, then store.
2. **Forgetting prefix sum offset**: The prefix sum array needs a leading 0: `prefix[0] = 0`. Without it, you miss subarrays starting at index 0.
3. **Using sorted string as key when character counts suffice**: `sorted(s)` costs O(k log k) per string. A 26-length count tuple costs O(k), which matters when k is large.
4. **Ignoring hash collision worst-case**: In adversarial inputs, hash map operations degrade to O(n). In interviews, acknowledge this but note Python's dict uses randomized hashing to mitigate it.
5. **Mutating the collection while iterating**: Adding/removing keys from a dict during iteration raises `RuntimeError`. Build results in a separate structure.

#### 8) Worked Examples (Full Python)
##### Example A: 1. Two Sum
```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        seen = {}
        for i, x in enumerate(nums):
            need = target - x
            if need in seen:
                return [seen[need], i]
            seen[x] = i
        return []
```

**Line-by-line explanation:**

- `seen = {}` -- Initialize an empty hash map. This will store each number we have processed as a key, mapped to its index as the value. We need this to look up complements in O(1).
- `for i, x in enumerate(nums):` -- Iterate through the array with both index `i` and value `x`. We need the index because the problem asks us to return indices, not values. `enumerate` gives us both in one pass.
- `need = target - x` -- Calculate the complement: the value that, when added to `x`, equals `target`. This is the core algebraic insight: instead of searching for two numbers, we search for one number and check if its partner already exists.
- `if need in seen:` -- Check if the complement exists in our hash map. This is an average O(1) lookup. If it exists, we have found our pair. This generalizes to any problem where you ask "have I seen the thing I need?"
- `return [seen[need], i]` -- Return the index of the complement (stored in the map) and the current index. The earlier index comes first because we stored it before reaching the current element.
- `seen[x] = i` -- Store the current value and its index in the map. This happens AFTER the complement check to avoid matching an element with itself. This line maintains our invariant: "seen contains all elements before index i."
- `return []` -- Fallback if no pair is found. Per the problem constraints, this line is never reached, but it satisfies the return type.

**Complexity: O(n) time, O(n) space.**
- Time is O(n) because we do one pass through the array, and each hash map operation (lookup and insert) is O(1) on average.
- Space is O(n) because in the worst case, we store all n elements in the map before finding a pair.

##### Example B: 49. Group Anagrams
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        groups = defaultdict(list)
        for s in strs:
            count = [0] * 26
            for ch in s:
                count[ord(ch) - ord('a')] += 1
            groups[tuple(count)].append(s)
        return list(groups.values())
```

**Line-by-line explanation:**

- `from collections import defaultdict` -- Import `defaultdict`, a dict subclass that auto-creates a default value (here, an empty list) when accessing a missing key. This avoids manual `if key not in dict` checks.
- `groups = defaultdict(list)` -- Create a mapping from character-frequency signature to list of strings sharing that signature. Each unique signature represents one anagram group.
- `for s in strs:` -- Iterate over every input string. We will compute a canonical key for each string and group strings with identical keys.
- `count = [0] * 26` -- Initialize a frequency array of 26 zeros, one per lowercase letter. This is our canonical representation of the string's character composition. Using an array instead of `sorted(s)` gives O(k) instead of O(k log k).
- `for ch in s:` -- Iterate over each character in the current string to build its frequency profile.
- `count[ord(ch) - ord('a')] += 1` -- Map character to index (a=0, b=1, ..., z=25) and increment its count. `ord()` returns the Unicode code point. Subtracting `ord('a')` normalizes to a 0-25 range. This is the standard technique for character counting with fixed alphabet.
- `groups[tuple(count)].append(s)` -- Convert the count list to a tuple (lists are not hashable, but tuples are) and use it as the dict key. Append the original string to the group. Two strings are anagrams if and only if they produce the same frequency tuple.
- `return list(groups.values())` -- Return all groups as a list of lists. `dict.values()` gives a view; wrapping in `list()` satisfies the return type.

**Complexity: O(n * k) time, O(n * k) space** where n is the number of strings and k is the maximum string length.
- Time: We process each of the n strings, and for each string we iterate through its k characters. No sorting is needed.
- Space: We store all n strings in the groups dict, and each string can be up to length k.

#### 9) Additional Practice
- 128\. Longest Consecutive Sequence
- 238\. Product of Array Except Self
- 36\. Valid Sudoku
- 560\. Subarray Sum Equals K
- 347\. Top K Frequent Elements

---

### Two Pointers
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Opposite-end scanning, same-direction (fast/slow) pointers, partitioning.
- Connected structures: arrays/strings, sorted arrays, sometimes linked lists.

**Term definitions:**
- **Opposite-end scanning**: Two pointers start at the first and last element, moving inward. Used when you need to consider pairs from both ends (e.g., container with most water, palindrome check).
- **Same-direction (fast/slow) pointers**: Both pointers start at the same end. The fast pointer advances ahead while the slow pointer marks a boundary. Used for in-place removal, cycle detection, and partitioning.
- **Partitioning**: Rearranging elements so that all elements satisfying a condition come before those that do not, using a write pointer (slow) and a scan pointer (fast).

#### 2) Subtopic Deep Dives

**Opposite-End Pointers**
- *Definition*: Place one pointer at index 0 and another at index n-1, then move them toward each other based on a comparison.
- *When you encounter it*: Sorted arrays where you need pairs summing to a target, palindrome verification, or maximizing a value constrained by width.
- *Core pattern*: `l, r = 0, len(a)-1; while l < r: compare a[l] and a[r], move the pointer that can improve the answer.`
- *Key insight*: Each move provably eliminates candidates. In Container With Most Water, moving the taller line can never produce a better answer, so you always move the shorter one.

**Same-Direction Pointers**
- *Definition*: Two pointers moving in the same direction at different speeds. The slow pointer marks the "write position" or "valid boundary."
- *When you encounter it*: Remove duplicates in place, move zeroes, find the middle of a linked list, detect cycles.
- *Core pattern*: `slow = 0; for fast in range(n): if condition: a[slow] = a[fast]; slow += 1`
- *Key insight*: The slow pointer represents "how much valid output we have built so far." Everything before slow is the answer.

**Three-Pointer / k-Sum Reduction**
- *Definition*: Fix one element, then use two pointers on the remaining sorted subarray. Reduces k-Sum to (k-1)-Sum.
- *When you encounter it*: 3Sum, 4Sum, or any problem asking for k elements with a target sum.
- *Core pattern*: Sort, then for each fixed element, run opposite-end two pointers on the rest. Skip duplicates after each match.
- *Key insight*: Sorting costs O(n log n) but enables O(n) per fixed element, giving O(n^2) for 3Sum instead of O(n^3).

#### 3) Key Insight / Mental Model
**Two pointers is a pruning strategy.** At each step, you prove that one candidate (or an entire range of candidates) cannot lead to a better answer, so you discard it by moving a pointer. The invariant is: "the answer, if it exists, lies between l and r." Every move shrinks the search space by at least one while preserving this invariant.

#### 4) Fast Recognition Cues
- Ask for pair/triplet conditions in sorted data.
- Need in-place compaction or opposite-end scanning.
- Brute force nested loops can be replaced by coordinated pointer moves.
- Problem says "sorted array" and asks for O(n) or O(1) space.
- Problem says "in-place" removal or rearrangement.
- Problem involves comparing characters from both ends (palindrome, mirroring).
- Problem asks for "maximum area," "minimum distance," or "closest pair" on a sorted or monotonic structure.

#### 5) When NOT to Use This Pattern
- **Unsorted data where sorting changes the answer**: If the problem requires returning original indices (like Two Sum), sorting destroys index information. Use a hash map instead.
- **Non-linear search space**: If the condition is not monotonic (i.e., you cannot determine which pointer to move), two pointers will not work. Consider binary search or brute force with pruning.
- **Need all pairs, not just one**: Two pointers find one optimal pair per pass. If you need to enumerate all valid pairs (like in some combinatorics problems), you may need a different approach.
- **Linked list without fast/slow pattern**: If you need random access in a linked list, two pointers will not help; convert to an array first.

#### 6) Universal Solve Framework
1. **Decide pointer direction.** If the input is sorted and you are looking for pairs or maximizing/minimizing a function of two positions, use opposite ends. If you need in-place compaction or cycle detection, use same direction.
2. **Define the movement rule from comparison outcome.** For opposite ends: if the current sum is too small, move the left pointer right (increase value); if too large, move right pointer left. For same direction: advance fast always, advance slow only when a condition is met.
3. **Prove each move discards impossible candidates.** This is the correctness argument. For Container With Most Water: moving the taller line while shrinking width cannot increase `min(h[l], h[r]) * (r - l)` because the height is already capped by the shorter line.
4. **Handle duplicates and boundaries explicitly.** In 3Sum, after finding a valid triplet, skip duplicate values: `while l < r and nums[l] == nums[l+1]: l += 1`. Always check `l < r` before accessing elements.

#### 7) Common Mistakes & Pitfalls
1. **Forgetting to sort first**: Opposite-end two pointers only works on sorted data. If you skip sorting, pointer movements do not prune correctly.
2. **Off-by-one on termination**: Use `while l < r` (not `l <= r`) for opposite-end problems. When `l == r`, you are at one element, not a pair.
3. **Not skipping duplicates in 3Sum**: After finding a valid triplet, failing to skip duplicate values at both pointers produces duplicate triplets in the output.
4. **Moving the wrong pointer**: In Container With Most Water, always move the pointer pointing to the shorter line. Moving the taller one can never improve the result. Getting this wrong breaks correctness.
5. **Confusing two pointers with sliding window**: Two pointers shrink the window by moving either end based on a comparison. Sliding window expands the right end unconditionally and contracts the left end to maintain a constraint. They are different techniques.

#### 8) Worked Examples (Full Python)
##### Example A: 125. Valid Palindrome
```python
class Solution:
    def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1
        while l < r:
            while l < r and not s[l].isalnum():
                l += 1
            while l < r and not s[r].isalnum():
                r -= 1
            if s[l].lower() != s[r].lower():
                return False
            l += 1
            r -= 1
        return True
```

**Line-by-line explanation:**

- `l, r = 0, len(s) - 1` -- Initialize two pointers at opposite ends of the string. `l` starts at the first character, `r` at the last. This is the standard opposite-end setup for palindrome checking.
- `while l < r:` -- Continue as long as the pointers have not met or crossed. When `l >= r`, all character pairs have been verified (or the string has odd length and we have reached the middle character, which does not need a pair).
- `while l < r and not s[l].isalnum():` -- Skip non-alphanumeric characters from the left. `isalnum()` returns True for letters and digits, False for spaces, punctuation, etc. The `l < r` guard prevents going out of bounds. This handles the problem's requirement to ignore non-alphanumeric characters.
- `l += 1` -- Advance the left pointer past the non-alphanumeric character. This generalizes to any problem where certain elements should be skipped during comparison.
- `while l < r and not s[r].isalnum():` -- Same skip logic for the right pointer, moving leftward past non-alphanumeric characters.
- `r -= 1` -- Advance the right pointer past the non-alphanumeric character.
- `if s[l].lower() != s[r].lower():` -- Compare the two alphanumeric characters in a case-insensitive manner. `.lower()` normalizes case. If they differ, the string is not a palindrome.
- `return False` -- Immediately return on mismatch. No need to check remaining characters.
- `l += 1` / `r -= 1` -- Move both pointers inward after a successful match to check the next pair.
- `return True` -- If all pairs matched, the string is a palindrome.

**Complexity: O(n) time, O(1) space.**
- Time is O(n) because each pointer moves at most n times total, and each character is visited at most once.
- Space is O(1) because we only use two integer pointers regardless of input size.

##### Example B: 11. Container With Most Water
```python
class Solution:
    def maxArea(self, height: list[int]) -> int:
        l, r = 0, len(height) - 1
        ans = 0
        while l < r:
            h = min(height[l], height[r])
            ans = max(ans, h * (r - l))
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return ans
```

**Line-by-line explanation:**

- `l, r = 0, len(height) - 1` -- Start with the widest possible container (first and last lines). This maximizes width; we will trade width for potentially taller lines as we search.
- `ans = 0` -- Track the maximum area found so far. We update this every iteration.
- `while l < r:` -- Continue until pointers meet. Every pair `(l, r)` with `l < r` is a candidate container; we prune most without evaluating.
- `h = min(height[l], height[r])` -- The water level is limited by the shorter of the two lines. This is the key physical constraint: water spills over the shorter side.
- `ans = max(ans, h * (r - l))` -- Compute area as height times width and update the running maximum. `r - l` is the distance between the two lines (the width).
- `if height[l] < height[r]:` -- Decide which pointer to move. We move the pointer at the shorter line because keeping the shorter line and moving the taller one can only decrease or maintain the height while also decreasing width, so it can never improve the area.
- `l += 1` -- Move the left pointer rightward, hoping to find a taller line that increases the bottleneck height enough to compensate for the reduced width.
- `r -= 1` -- Move the right pointer leftward (when right is shorter or equal).
- `return ans` -- Return the maximum area found.

**Complexity: O(n) time, O(1) space.**
- Time is O(n) because each iteration moves one pointer inward, and we start with at most n-1 gap, so at most n-1 iterations.
- Space is O(1) because we use only a constant number of variables.

#### 9) Additional Practice
- 15\. 3Sum
- 167\. Two Sum II - Input Array Is Sorted
- 42\. Trapping Rain Water
- 283\. Move Zeroes

---

### Stack
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Stacks, Monotonic Stacks.
- Connected structures: list-as-stack, monotonic stack, call stack (recursion).

**Term definitions:**
- **Stack**: A Last-In-First-Out (LIFO) data structure. In Python, use a `list` with `append()` (push) and `pop()` (pop from top). O(1) for both operations.
- **Monotonic Stack**: A stack that maintains elements in strictly increasing or strictly decreasing order. When a new element violates the ordering, you pop elements until the invariant is restored. Each pop finalizes an answer for the popped element.
- **Call Stack**: The implicit stack used by recursion. Understanding the explicit stack pattern helps you convert recursive solutions to iterative ones when stack depth is a concern.

#### 2) Subtopic Deep Dives

**Basic Stack (Matching / Balancing)**
- *Definition*: Using a stack to match opening and closing delimiters, or to track unresolved items that will be resolved later.
- *When you encounter it*: Parentheses validation, HTML tag matching, expression evaluation, undo operations.
- *Core pattern*: Push openers; when you see a closer, pop and verify the top matches. If the stack is empty at the end, everything was matched.
- *Key insight*: The stack naturally handles nesting. The most recently opened delimiter must be the first one closed. This is exactly LIFO order.

**Monotonic Stack**
- *Definition*: A stack where elements are maintained in sorted order (either all increasing or all decreasing from bottom to top). Pushing a new element triggers pops of all elements that violate the ordering.
- *When you encounter it*: "Next greater element," "next smaller element," "largest rectangle in histogram," "daily temperatures," "stock span."
- *Core pattern*: `for i, x in enumerate(arr): while stack and arr[stack[-1]] < x: j = stack.pop(); answer[j] = i - j; stack.append(i)`
- *Key insight*: Each element is pushed once and popped once, so the total work across all iterations is O(n), even though there is a while loop inside the for loop.

**Expression Evaluation**
- *Definition*: Using one or two stacks to evaluate arithmetic expressions, handling operator precedence and parentheses.
- *When you encounter it*: "Evaluate Reverse Polish Notation," "Basic Calculator," any infix/postfix expression problem.
- *Core pattern*: For RPN, push operands; when you see an operator, pop two operands, apply the operator, push the result. For infix, use the shunting-yard algorithm.
- *Key insight*: RPN eliminates the need for parentheses and precedence rules because the order of operations is encoded in the token sequence itself.

#### 3) Key Insight / Mental Model
**A stack is a "TODO list" of unresolved items.** You push items when you cannot determine their answer yet, and you pop them when a new element provides the missing information. The LIFO property ensures you always resolve the most recent unresolved item first -- which is exactly right for nested structures and "nearest" queries.

#### 4) Fast Recognition Cues
- Nested structure matching (`()[]{}`, HTML tags, nested function calls).
- Next greater/smaller element or nearest boundary.
- Need to process elements while preserving unresolved candidates.
- Problem involves "nearest" something to the left or right.
- Expression evaluation (postfix, infix with parentheses).
- Problem naturally has recursive structure but you need an iterative solution.
- Problem asks about "spans" or "visible buildings" -- monotonic stack signals.
- Undo/back operations (browser history, text editor).

#### 5) When NOT to Use This Pattern
- **Need to access arbitrary elements**: A stack only gives you the top element. If you need to query the minimum/maximum at any time, you need an augmented stack (Min Stack) or a different structure.
- **Problem requires FIFO order**: If elements must be processed in the order they were added, you need a queue, not a stack. Look for "first come first served" language.
- **Sorted order across all elements**: A monotonic stack maintains local ordering, but if you need globally sorted data, use a heap or sorted container.
- **Problem has "sliding window" language**: Sliding window minimum/maximum uses a monotonic deque (double-ended queue), not a stack, because you need to remove from both ends.

#### 6) Universal Solve Framework
1. **Define what each stack element stores.** Common choices: index only (when the array is accessible), value only (for simple matching), or `(index, value)` pairs (when both are needed for the answer computation). For monotonic stacks, indices are almost always needed to compute distances.
2. **Define the pop condition.** "Pop while the stack is not empty AND the top element satisfies [condition] relative to the current element." For monotonic decreasing: pop while `stack[-1] < current`. For matching: pop when closer matches opener.
3. **On pop, finalize the answer for the popped item.** The current element is what "resolved" the popped element. For Daily Temperatures: `ans[j] = i - j` (the distance to the next warmer day). For Valid Parentheses: the pop confirms a match.
4. **Push the current element as an unresolved candidate.** After all pops, push the current element. It will be resolved later by a future element, or it remains unresolved (which may have a default answer like 0 or -1).

#### 7) Common Mistakes & Pitfalls
1. **Forgetting to check `not st` before accessing `st[-1]`**: Popping or peeking an empty stack raises `IndexError`. Always guard with `if st` or `while st and ...`.
2. **Storing values instead of indices in monotonic stack**: You almost always need indices to compute distances. Store indices and look up values via `arr[stack[-1]]`.
3. **Wrong monotonic direction**: For "next greater element," you want a decreasing stack (from bottom to top). For "next smaller element," you want an increasing stack. Getting this backward inverts the answer.
4. **Not handling remaining elements after the loop**: After processing all elements, items left on the stack had no resolving element. Their answer is typically 0, -1, or n (depending on the problem). Do not forget to handle them.
5. **Off-by-one in histogram problems**: In Largest Rectangle in Histogram, you often need to append a sentinel value (0) to the end of the heights array to force all remaining elements to pop.

#### 8) Worked Examples (Full Python)
##### Example A: 20. Valid Parentheses
```python
class Solution:
    def isValid(self, s: str) -> bool:
        match = {')': '(', ']': '[', '}': '{'}
        st = []
        for ch in s:
            if ch in match.values():
                st.append(ch)
            else:
                if not st or st[-1] != match.get(ch):
                    return False
                st.pop()
        return not st
```

**Line-by-line explanation:**

- `match = {')': '(', ']': '[', '}': '{'}` -- Create a mapping from each closing bracket to its corresponding opening bracket. This lets us look up what opener a closer expects in O(1). Using a dict is cleaner than if/elif chains.
- `st = []` -- Initialize an empty stack (Python list). This will hold unmatched opening brackets. The stack is the core data structure: it tracks which openers are waiting for their closers.
- `for ch in s:` -- Process each character in the string exactly once. One pass is sufficient because the stack handles nesting.
- `if ch in match.values():` -- Check if the character is an opening bracket ('(', '[', '{'). `match.values()` returns the openers. An alternative is `if ch in '([{'` which is more explicit.
- `st.append(ch)` -- Push the opening bracket onto the stack. It is now an "unresolved" opener waiting for its matching closer. The most recent opener (top of stack) must be matched first due to nesting rules.
- `else:` -- The character is a closing bracket (or could be invalid, but the problem guarantees only bracket characters).
- `if not st or st[-1] != match.get(ch):` -- Two failure conditions: (1) `not st` means we have a closer with no unmatched opener -- too many closers. (2) `st[-1] != match.get(ch)` means the top opener does not match this closer (e.g., `(]`). Either case means invalid.
- `return False` -- Immediately return invalid on mismatch.
- `st.pop()` -- The top opener matches this closer. Remove it from the stack; this pair is resolved.
- `return not st` -- After processing all characters, the string is valid only if no unmatched openers remain. `not st` is True when the stack is empty. If the stack is non-empty, there are unclosed openers.

**Complexity: O(n) time, O(n) space.**
- Time is O(n) because each character is processed once, and each push/pop is O(1).
- Space is O(n) in the worst case when all characters are openers (e.g., `(((((`), all pushed to the stack.

##### Example B: 739. Daily Temperatures
```python
class Solution:
    def dailyTemperatures(self, temperatures: list[int]) -> list[int]:
        n = len(temperatures)
        ans = [0] * n
        st = []  # decreasing stack of indices by temperature

        for i, t in enumerate(temperatures):
            while st and temperatures[st[-1]] < t:
                j = st.pop()
                ans[j] = i - j
            st.append(i)

        return ans
```

**Line-by-line explanation:**

- `n = len(temperatures)` -- Store the length for readability. Used to initialize the answer array.
- `ans = [0] * n` -- Initialize the answer array with all zeros. Zero is the correct default: if no warmer day exists, the answer for that day is 0. Pre-allocating avoids repeated appends.
- `st = []` -- Initialize the monotonic stack. It will hold indices of days whose "next warmer day" has not yet been found. The stack maintains a decreasing order of temperatures from bottom to top: each element on the stack has a temperature greater than or equal to the one above it.
- `for i, t in enumerate(temperatures):` -- Iterate through each day with its index and temperature. Each day is both a potential answer (for days on the stack) and a new unresolved candidate.
- `while st and temperatures[st[-1]] < t:` -- Pop all stack elements whose temperature is less than the current temperature. The current day is the "next warmer day" for each of these popped days. The `while` (not `if`) is critical: one warm day can resolve multiple cooler days.
- `j = st.pop()` -- Remove the top index from the stack. Day `j` has found its next warmer day (day `i`).
- `ans[j] = i - j` -- The number of days day `j` had to wait is the difference between the current index and the popped index. This is why we store indices, not temperatures, on the stack.
- `st.append(i)` -- Push the current day as an unresolved candidate. Its next warmer day has not been found yet. This maintains the decreasing invariant because all elements smaller than `t` were already popped.
- `return ans` -- Return the completed answer array. Days left on the stack at the end have no warmer future day, and their answer remains the default 0.

**Complexity: O(n) time, O(n) space.**
- Time is O(n) despite the nested while loop because each index is pushed exactly once and popped at most once. Total pushes + pops = 2n = O(n).
- Space is O(n) for the answer array and stack, which in the worst case (strictly decreasing temperatures) holds all n indices.

#### 9) Additional Practice
- 84\. Largest Rectangle in Histogram
- 155\. Min Stack
- 150\. Evaluate Reverse Polish Notation
- 853\. Car Fleet

---

### Binary Search
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Search Array, Search Range.
- Connected structures: sorted arrays, implicit monotonic answer space, search trees (conceptually).

**Term definitions:**
- **Search Array**: Classic binary search on a sorted array to find a target value or its insertion point. The array itself provides the sorted domain.
- **Search Range** (Binary Search on Answer): Instead of searching an array, you binary search over a range of possible answers (e.g., speeds, capacities, distances). A feasibility function `can(mid)` determines which half to keep. Also called "binary search the answer" or "parametric search."
- **Monotonic Predicate**: A boolean function `f(x)` that is False for all `x < threshold` and True for all `x >= threshold` (or vice versa). Binary search finds the exact threshold where the flip occurs.
- **Lower Bound / Upper Bound**: Lower bound is the first position where `f(x)` becomes True. Upper bound is the first position where `f(x)` becomes False again (or the position after the last True). Python's `bisect_left` finds the lower bound; `bisect_right` finds the upper bound.

#### 2) Subtopic Deep Dives

**Search Array (Classic Binary Search)**
- *Definition*: Find a target in a sorted array by repeatedly halving the search space.
- *When you encounter it*: "Find target in sorted array," "find insertion point," any problem that explicitly gives you a sorted array and asks for O(log n).
- *Core pattern*: `l, r = 0, n-1; while l <= r: m = (l+r)//2; compare nums[m] to target; adjust l or r.`
- *Key insight*: The `while l <= r` template with `l = m+1` and `r = m-1` guarantees termination and covers all elements. When the loop exits, `l` is the insertion point (first element > target if not found).

**Search Range (Binary Search on Answer)**
- *Definition*: When the answer itself is a number in a range, and you can write a function `can(mid)` that returns True if `mid` is feasible, binary search over the answer range.
- *When you encounter it*: "Minimum speed to finish in time," "minimum capacity to ship," "maximum minimum distance" -- any optimization problem where checking feasibility is easier than finding the optimum directly.
- *Core pattern*: `l, r = min_possible, max_possible; while l <= r: m = (l+r)//2; if can(m): ans = m; adjust toward better; else: adjust other way.`
- *Key insight*: You are not searching an array. You are searching a number line. The feasibility function `can(mid)` must be monotonic: once it becomes True, it stays True for all larger (or smaller) values.

**Rotated / Modified Sorted Array**
- *Definition*: An array that was sorted but then rotated at some pivot, creating two sorted segments.
- *When you encounter it*: "Search in rotated sorted array," "find minimum in rotated sorted array."
- *Core pattern*: Compare `nums[m]` to `nums[r]` (or `nums[l]`) to determine which half is sorted. Then check if the target lies within the sorted half.
- *Key insight*: At least one half of a rotated sorted array is always sorted. Identify which half is sorted, check if the target is in that half, and eliminate the other half.

#### 3) Key Insight / Mental Model
**Binary search does not require a sorted array. It requires a monotonic predicate.** Forget "searching for a target." Instead, think: "There is a boundary where a condition flips from False to True. I am finding that boundary." Whether the domain is array indices, integer speeds, or floating-point distances, if you can define a function that flips once, binary search finds the flip point in O(log n) evaluations.

#### 4) Fast Recognition Cues
- Sorted input and O(log n) target.
- Condition flips from false to true (monotonic predicate).
- Asking for first/last valid position or minimum feasible value.
- Problem says "minimum maximum" or "maximum minimum" -- classic binary search on answer.
- Problem says "within D days" or "at most H hours" -- feasibility check for binary search on answer.
- Problem says "rotated sorted array" -- modified binary search.
- Problem gives a huge numeric range (e.g., 1 to 10^9) and asks for an optimal value -- brute force is impossible, binary search on the answer space.
- The word "sorted" or "monotonic" appears anywhere in the problem.

#### 5) When NOT to Use This Pattern
- **Unsorted data without a monotonic property**: If neither the array is sorted nor the answer space has a monotonic feasibility function, binary search does not apply. You might need hashing or sorting first.
- **Need all occurrences, not just one boundary**: Binary search finds one boundary point. If you need to enumerate all matches, you may need two binary searches (for range) or a different approach.
- **Multi-dimensional search**: Binary search works on one dimension. For 2D problems (e.g., search a 2D matrix), you can sometimes reduce to 1D, but not always.
- **The feasibility function is not monotonic**: If `can(5)` is True but `can(6)` is False and `can(7)` is True again, binary search will give incorrect results. Verify monotonicity before applying.

#### 6) Universal Solve Framework
1. **Define the search domain.** For array search: `l, r = 0, len(nums)-1`. For answer search: `l, r = minimum_possible_answer, maximum_possible_answer`. Choosing tight bounds speeds up the search.
2. **Define the monotonic predicate `can(mid)`.** For array search: `nums[mid] >= target` (finding lower bound). For answer search: write a function that checks if `mid` is a feasible answer (e.g., "can Koko eat all bananas at speed `mid` within `h` hours?"). This function must be monotonic.
3. **Use the boundary pattern.** Two common templates:
   - `while l <= r` with `l = m+1` and `r = m-1`: terminates when `l > r`, and `l` is the insertion point. Good for exact match or lower bound.
   - `while l < r` with `l = m+1` and `r = m` (or `l = m` and `r = m-1`): terminates when `l == r`, which is the answer. Good for "find minimum satisfying condition."
4. **Prove correctness on edge cases.** Test mentally: What if all elements satisfy the predicate? (Answer is `l`.) What if none do? (Answer is `r+1` or "not found.") What about a single-element array? Does `m = (l+r)//2` avoid infinite loops?

#### 7) Common Mistakes & Pitfalls
1. **Integer overflow in `(l + r) // 2`**: In languages like Java/C++, `l + r` can overflow. Use `l + (r - l) // 2` instead. Python has arbitrary precision integers so this is not an issue in Python, but mention it in interviews.
2. **Off-by-one causing infinite loops**: The most dangerous bug. With `while l < r` and `m = (l+r)//2`, setting `l = m` (not `m+1`) can cause infinite loops when `l + 1 == r` because `m` rounds down to `l`. Fix: use `m = (l+r+1)//2` (round up) when setting `l = m`.
3. **Wrong half elimination in rotated arrays**: When comparing `nums[m]` with `nums[l]` or `nums[r]`, getting the inequality direction wrong eliminates the wrong half. Draw out small examples with the rotation.
4. **Forgetting to track the answer separately**: In "search the answer" problems, when `can(m)` is True, store `ans = m` before adjusting bounds. If you rely solely on `l` or `r` at the end, you might return an infeasible value.
5. **Non-monotonic feasibility function**: If your `can(mid)` function is not truly monotonic, binary search silently gives wrong answers. Always verify: if `can(k)` is True, is `can(k+1)` also True (for minimization) or is `can(k-1)` also True (for maximization)?

#### 8) Worked Examples (Full Python)
##### Example A: 704. Binary Search
```python
class Solution:
    def search(self, nums: list[int], target: int) -> int:
        l, r = 0, len(nums) - 1
        while l <= r:
            m = (l + r) // 2
            if nums[m] == target:
                return m
            if nums[m] < target:
                l = m + 1
            else:
                r = m - 1
        return -1
```

**Line-by-line explanation:**

- `l, r = 0, len(nums) - 1` -- Initialize the search range to the entire array. `l` is the leftmost candidate index, `r` is the rightmost. The target, if it exists, must be at an index in `[l, r]`.
- `while l <= r:` -- Continue searching as long as there is at least one candidate index. The `<=` (not `<`) is critical: when `l == r`, there is one element left to check. Using `<` would skip it.
- `m = (l + r) // 2` -- Compute the midpoint using integer division. This is the index we will probe. Floor division ensures `m` is always a valid index between `l` and `r`. In Python, no overflow risk; in other languages, use `l + (r - l) // 2`.
- `if nums[m] == target:` -- Check for exact match. If the midpoint value equals the target, we have found it.
- `return m` -- Return the index immediately. No need to continue searching.
- `if nums[m] < target:` -- The target is larger than the midpoint value. Since the array is sorted, the target must be to the right of `m`.
- `l = m + 1` -- Eliminate the left half including `m` (already checked). Moving `l` to `m + 1` ensures progress: the search space shrinks by at least one element every iteration.
- `r = m - 1` -- The target is smaller than the midpoint value; eliminate the right half including `m`. Same shrinking guarantee.
- `return -1` -- The loop exited without finding the target, meaning `l > r` and the search space is empty. The target is not in the array.

**Complexity: O(log n) time, O(1) space.**
- Time is O(log n) because each iteration halves the search space. Starting with n elements, after k iterations we have n/2^k elements. The loop ends when n/2^k < 1, giving k = log2(n).
- Space is O(1) because we use only three integer variables regardless of input size.

##### Example B: 875. Koko Eating Bananas
```python
import math

class Solution:
    def minEatingSpeed(self, piles: list[int], h: int) -> int:
        def can(k: int) -> bool:
            hours = 0
            for p in piles:
                hours += math.ceil(p / k)
            return hours <= h

        l, r = 1, max(piles)
        ans = r
        while l <= r:
            m = (l + r) // 2
            if can(m):
                ans = m
                r = m - 1
            else:
                l = m + 1
        return ans
```

**Line-by-line explanation:**

- `import math` -- Import the math module for `math.ceil`, which rounds a number up to the nearest integer. We need ceiling division to compute how many hours a pile takes.
- `def can(k: int) -> bool:` -- Define the feasibility function. Given eating speed `k` (bananas per hour), returns True if Koko can finish all piles within `h` hours. This is the monotonic predicate: if she can finish at speed `k`, she can also finish at any speed > `k`.
- `hours = 0` -- Accumulate total hours needed across all piles.
- `for p in piles:` -- Iterate over each pile to compute how long it takes at speed `k`.
- `hours += math.ceil(p / k)` -- A pile of `p` bananas at speed `k` takes `ceil(p/k)` hours. Koko eats at most `k` per hour and cannot start a new pile in the same hour. Ceiling division handles the partial last hour. Equivalent to `(p + k - 1) // k` using integer arithmetic.
- `return hours <= h` -- Return True if total hours is within the allowed limit. This is the feasibility check.
- `l, r = 1, max(piles)` -- Define the search range for speed. Minimum speed is 1 (must eat at least one banana per hour). Maximum useful speed is `max(piles)` (can finish any pile in one hour; going faster wastes no time since she only eats from one pile per hour).
- `ans = r` -- Initialize the answer to the maximum speed (always feasible). We will try to find a smaller feasible speed.
- `while l <= r:` -- Standard binary search loop over the answer space.
- `m = (l + r) // 2` -- Try the midpoint speed.
- `if can(m):` -- If speed `m` is feasible, it is a candidate answer, but there might be a smaller feasible speed.
- `ans = m` -- Record this feasible speed as the best so far.
- `r = m - 1` -- Search for a smaller feasible speed in the left half.
- `l = m + 1` -- Speed `m` is not feasible. We need a faster speed; search the right half.
- `return ans` -- Return the smallest feasible speed found.

**Complexity: O(n log M) time, O(1) space** where n = len(piles) and M = max(piles).
- Time: Binary search runs O(log M) iterations (searching speeds from 1 to M). Each iteration calls `can()`, which iterates over all n piles in O(n). Total: O(n log M).
- Space is O(1) because we use only a few variables. The input array is not modified.

#### 9) Additional Practice
- 34\. Find First and Last Position of Element in Sorted Array
- 153\. Find Minimum in Rotated Sorted Array
- 33\. Search in Rotated Sorted Array
- 1011\. Capacity To Ship Packages Within D Days




### Sliding Window
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** Sliding Window Fixed Size, Variable Size.
- **Connected structures:** two pointers, hash map/set, deque (for monotonic windows).

**Term Definitions:**
- **Sliding Window:** A technique where you maintain a "window" (a contiguous range of elements defined by two pointers) over a sequence, and slide it across the data to avoid redundant computation.
- **Fixed Size Window:** The window length is predetermined (e.g., "find max sum of k consecutive elements"). Both pointers advance in lockstep.
- **Variable Size Window:** The window expands and contracts dynamically based on a constraint (e.g., "find the shortest subarray with sum >= target"). The right pointer expands, the left pointer shrinks.
- **Two Pointers:** A general technique using two indices to traverse data; sliding window is a specialized form where both pointers move in the same direction.
- **Hash Map/Set:** Used to track element frequencies or presence within the current window in O(1) time.
- **Deque (Double-Ended Queue):** A data structure supporting O(1) push/pop from both ends; used in monotonic window problems (e.g., sliding window maximum) to maintain candidates in sorted order.
- **Monotonic Deque:** A deque where elements are maintained in non-increasing or non-decreasing order, allowing O(1) access to the current window's max or min.

#### 2) Subtopic Deep Dives

##### Fixed Size Sliding Window
- **Definition:** A window of exactly k elements slides one position at a time. When the right pointer advances, the left pointer also advances to maintain size k.
- **When you encounter it:** The problem specifies a fixed window size k, or asks about "every subarray of length k."
- **Core implementation pattern:**
  1. Build the first window of size k (process indices 0 to k-1).
  2. Slide: add the new right element, remove the old left element, update your answer.
- **Key insight:** You never need to recompute the full window — you only add one element and remove one element per step, turning O(n*k) brute force into O(n).

##### Variable Size Sliding Window
- **Definition:** The window size changes dynamically. The right pointer expands the window to explore; the left pointer contracts it to restore a constraint.
- **When you encounter it:** The problem says "minimum length subarray such that..." or "longest substring where..." — any optimization over contiguous ranges with a condition.
- **Core implementation pattern:**
  1. Expand right pointer unconditionally.
  2. While the window violates (or satisfies) the condition, shrink from the left.
  3. Record the answer at the valid state.
- **Key insight:** Both pointers only move forward. The left pointer across the entire algorithm moves at most n times total (not n times per right step), giving O(n) amortized.

#### 3) Key Insight / Mental Model
Think of the window as a caterpillar crawling along the array. The front (right pointer) stretches forward to explore, and the back (left pointer) contracts forward to shed elements that make the window invalid. The caterpillar never moves backward — this is why the technique is O(n). Every element enters the window exactly once and leaves exactly once.

For fixed-size windows: the caterpillar has a rigid body length. For variable-size windows: the caterpillar is elastic.

#### 4) Fast Recognition Cues
- The word **"contiguous"** appears — subarray, substring (not subsequence).
- The problem asks for **max/min length** of a subarray/substring meeting a condition.
- You need the **best/optimal** over all windows (max sum, min length, etc.).
- Brute force would be O(n^2) by checking every subarray — sliding window reduces to O(n).
- Constraints involve **character frequency**, **distinct count**, or a **running sum** within a range.
- The phrase **"at most k"** or **"exactly k"** distinct/unique elements.
- The problem involves **permutation/anagram** checks within a string (fixed-size window = length of pattern).

#### 5) When NOT to Use This Pattern
- **Non-contiguous selections:** If the problem asks for a subsequence (not substring/subarray), sliding window doesn't apply. Use DP or greedy instead.
- **Unordered collections:** If you can pick elements from anywhere (like knapsack), there's no "window" to slide.
- **The shrink condition isn't monotonic:** Sliding window requires that once the window becomes invalid, adding more elements from the right won't make it valid again (or vice versa). If removing the left element can make things worse, the two-pointer invariant breaks.
- **Need all pairs/combinations:** If you need every pair (i, j), not just the optimal contiguous range, sliding window won't cover it.
- **Tree/graph structures:** Contiguous range logic doesn't apply to non-linear data.

#### 6) Universal Solve Framework
1. **Initialize pointers and state:** Set `left = 0`. Choose an appropriate data structure for window state (counter dict for frequencies, integer for running sum, deque for monotonic queries). Initialize your answer variable.
2. **Expand right pointer:** Iterate `right` from 0 to n-1. Add `arr[right]` to the window state (increment count, add to sum, push onto deque, etc.).
3. **Shrink from left while invalid:** Determine your window validity condition. While the window violates the constraint, remove `arr[left]` from the state and increment `left`. For fixed-size windows, shrink whenever `right - left + 1 > k`.
4. **Record the answer:** After the window is valid, check if the current window improves your best answer. For "minimum length" problems, record inside the shrink loop. For "maximum length" problems, record after the shrink loop.
5. **Return the answer.**

**Deciding where to record the answer** is a common source of confusion:
- Minimum length → record inside the while loop (you want the smallest valid window).
- Maximum length → record outside the while loop (you want the largest valid window).

#### 7) Common Mistakes & Pitfalls
1. **Off-by-one in window size:** The window `[left, right]` has size `right - left + 1`, not `right - left`. Getting this wrong corrupts every length calculation.
2. **Not updating state on shrink:** When you move `left` forward, you must undo the effect of the element leaving the window (decrement its count, subtract from sum). Forgetting this means your window state is stale.
3. **Using `in` checks on a Counter instead of `> 0`:** A Python Counter keeps keys even after their count hits 0. Checking `if ch in counter` will return True even if the count is 0. Always check `counter[ch] > 0`.
4. **Shrinking too eagerly or too lazily:** For "longest" problems, only shrink while the window is invalid. For "shortest" problems, keep shrinking while the window is still valid. Mixing these up inverts your answer.
5. **Resetting left pointer:** Never reset `left = 0` inside the loop. The left pointer is monotonically non-decreasing across the entire run — resetting it turns the algorithm into O(n^2).

#### 8) Worked Examples (Full Python)

##### Example A: 3. Longest Substring Without Repeating Characters
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        last = {}
        l = 0
        best = 0
        for r, ch in enumerate(s):
            if ch in last and last[ch] >= l:
                l = last[ch] + 1
            last[ch] = r
            best = max(best, r - l + 1)
        return best
```

**Line-by-line explanation:**

- `last = {}` — Initialize an empty dictionary that maps each character to the index where it was most recently seen. This is our window state: it lets us detect duplicates in O(1) without scanning the window.
- `l = 0` — The left boundary of our window. Starts at the beginning of the string. This pointer only moves forward (never backward), which is the hallmark of sliding window.
- `best = 0` — Tracks the length of the longest valid window found so far. We want the maximum, so we record after shrinking.
- `for r, ch in enumerate(s):` — Expand the right pointer one step at a time. `r` is the right boundary index, `ch` is the character at that index. Every character enters the window exactly once through this loop.
- `if ch in last and last[ch] >= l:` — Check if `ch` is a duplicate within the current window. Two conditions: (1) we've seen `ch` before (`ch in last`), and (2) that occurrence is within our current window (`last[ch] >= l`). If the previous occurrence is before `l`, it's outside our window and doesn't count as a duplicate.
- `l = last[ch] + 1` — Shrink the window by jumping the left pointer past the previous occurrence of the duplicate character. This is an optimization over the typical "while loop" shrink — because we stored exact positions, we can jump directly. This generalizes to any problem where you can compute the new left boundary in O(1).
- `last[ch] = r` — Update the most recent position of `ch` to the current index. This must happen after the duplicate check so we don't compare a character against itself.
- `best = max(best, r - l + 1)` — The window `[l, r]` is now valid (no duplicates). Its length is `r - l + 1`. Update the best if this window is longer. We record here (after shrink) because we want the maximum length.
- `return best` — Return the length of the longest substring without repeating characters.

**Complexity:** O(n) time — each character is visited once by the right pointer, and the left pointer moves at most n times total across the entire run. O(min(n, k)) space where k is the alphabet size, for the `last` dictionary. This is optimal because any solution must examine every character at least once.

##### Example B: 76. Minimum Window Substring
```python
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        need = Counter(t)
        missing = len(t)
        l = 0
        best_len = float('inf')
        best = (0, 0)

        for r, ch in enumerate(s):
            if need[ch] > 0:
                missing -= 1
            need[ch] -= 1

            while missing == 0:
                if r - l + 1 < best_len:
                    best_len = r - l + 1
                    best = (l, r + 1)
                left_ch = s[l]
                need[left_ch] += 1
                if need[left_ch] > 0:
                    missing += 1
                l += 1

        return s[best[0]:best[1]] if best_len != float('inf') else ""
```

**Line-by-line explanation:**

- `from collections import Counter` — Import Counter, a dict subclass that counts hashable objects. It provides default values of 0 for missing keys, which simplifies frequency tracking.
- `need = Counter(t)` — Build a frequency map of all characters required by string `t`. For example, if `t = "ABC"`, then `need = {'A': 1, 'B': 1, 'C': 1}`. This represents how many of each character we still need inside our window.
- `missing = len(t)` — Total number of individual character obligations remaining. When this reaches 0, our window contains all characters of `t` (with sufficient multiplicity). Using a single integer avoids having to check every key in `need` each iteration.
- `l = 0` — Left pointer of the window, starts at the beginning.
- `best_len = float('inf')` — Track the length of the smallest valid window found. Initialized to infinity so any valid window will be smaller.
- `best = (0, 0)` — Store the (start, end) indices of the best window. Using a tuple avoids storing the substring itself until the end.
- `for r, ch in enumerate(s):` — Expand the right pointer across every character in `s`. This is the outer expansion loop of the variable-size sliding window.
- `if need[ch] > 0:` — If `ch` is a character we still need (its count in `need` is positive), then adding it to the window satisfies one obligation. Characters not in `t` will have `need[ch] = 0` (Counter default), so they won't affect `missing`. Characters of `t` that we already have enough of will also have `need[ch] <= 0`.
- `missing -= 1` — Decrement the total obligations counter. One fewer character is needed.
- `need[ch] -= 1` — Consume this character by decrementing its count in `need`. This happens for every character, not just ones in `t`. Characters not in `t` will go negative, which is fine — negative means "we have more than we need." This is the key trick: `need[ch] > 0` means we're still short, `need[ch] <= 0` means we have enough or more.
- `while missing == 0:` — While the window contains all required characters, try to shrink it from the left to find a smaller valid window. This is the shrink phase. For minimum-length problems, we record the answer inside this loop.
- `if r - l + 1 < best_len:` — Check if the current valid window is smaller than the best found so far.
- `best_len = r - l + 1` — Update the best length.
- `best = (l, r + 1)` — Store the window boundaries. `r + 1` because Python slicing is exclusive on the right end.
- `left_ch = s[l]` — Capture the character about to leave the window (the one at the left boundary).
- `need[left_ch] += 1` — "Return" this character: increment its count in `need`, reflecting that we no longer have it in the window. If the count was negative (surplus), it becomes less negative. If it was 0, it becomes positive (we now need it again).
- `if need[left_ch] > 0:` — If after returning this character we now need it (count went positive), the window is no longer valid.
- `missing += 1` — Reflect that we're now missing one more character, which will cause the while loop to exit.
- `l += 1` — Move the left pointer forward, completing the shrink step.
- `return s[best[0]:best[1]] if best_len != float('inf') else ""` — Return the smallest window substring if one was found, otherwise return empty string (no valid window exists).

**Complexity:** O(|s| + |t|) time — building the Counter is O(|t|), and each pointer traverses `s` at most once, so the main loop is O(|s|). O(|s| + |t|) space for the Counter (bounded by alphabet size in practice). This is optimal because every character in `s` must be examined at least once to determine if it belongs in the answer.

#### 9) Additional Practice
- 209. Minimum Size Subarray Sum
- 567. Permutation in String
- 424. Longest Repeating Character Replacement
- 239. Sliding Window Maximum

---

### Linked List
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** Singly Linked Lists, Doubly Linked Lists, Fast and Slow Pointers.
- **Connected structures:** `ListNode`, dummy nodes, fast/slow pointers.

**Term Definitions:**
- **Linked List:** A linear data structure where each element (node) contains a value and a pointer (reference) to the next node. Unlike arrays, elements are not stored contiguously in memory.
- **Singly Linked List:** Each node has one pointer (`next`). You can only traverse forward. This is the default linked list type in most interview problems.
- **Doubly Linked List:** Each node has two pointers (`next` and `prev`), allowing traversal in both directions. Used in LRU cache implementations and when you need O(1) deletion given a node reference.
- **Fast and Slow Pointers (Floyd's Tortoise and Hare):** A technique where two pointers traverse the list at different speeds. The slow pointer moves one step at a time, the fast pointer moves two steps. Used for cycle detection, finding the middle node, and finding the start of a cycle.
- **ListNode:** The standard node class: `class ListNode: def __init__(self, val=0, next=None)`.
- **Dummy Node (Sentinel):** A fake node placed before the real head. It simplifies edge cases where the head itself might be deleted or changed, because you always return `dummy.next` as the real head.

#### 2) Subtopic Deep Dives

##### Singly Linked Lists
- **Definition:** A chain of nodes where each node points to the next. The last node points to `None`.
- **When you encounter it:** Any problem that gives you a `ListNode` head and asks you to traverse, reverse, merge, or modify the list.
- **Core implementation pattern:** Iterate with `curr = head; while curr: ... curr = curr.next`. For modifications, always save `curr.next` before rewiring.
- **Key insight:** You can't go backward. If you need information about a previous node, either track it with a `prev` pointer, or use recursion (which implicitly uses the call stack to "remember" previous nodes).

##### Doubly Linked Lists
- **Definition:** Each node has both `next` and `prev` pointers, allowing O(1) insertion and deletion at any known position.
- **When you encounter it:** LRU Cache (LeetCode 146), problems requiring O(1) removal given a direct reference to a node, or when you need to traverse in both directions.
- **Core implementation pattern:** Maintain sentinel head and tail nodes. To remove a node: `node.prev.next = node.next; node.next.prev = node.prev`. To insert after a node: update four pointers.
- **Key insight:** The trade-off is memory (extra pointer per node) for the ability to delete any node in O(1) without needing to find its predecessor.

##### Fast and Slow Pointers
- **Definition:** Two pointers starting at the head, where slow advances by 1 and fast advances by 2 per iteration.
- **When you encounter it:** Cycle detection, finding the middle of a list, finding the node where a cycle begins, or checking if a linked list is a palindrome.
- **Core implementation pattern:** `slow = fast = head; while fast and fast.next: slow = slow.next; fast = fast.next.next`.
- **Key insight:** When fast reaches the end, slow is at the middle (because fast traveled 2x the distance). If there's a cycle, fast will eventually lap slow — they must meet because the fast pointer closes the gap by 1 each step.

#### 3) Key Insight / Mental Model
Think of linked list problems as **pointer surgery**. You're a surgeon rewiring connections between nodes. The three rules of pointer surgery are:
1. **Save before you cut** — always store `curr.next` in a temp variable before you redirect `curr.next` somewhere else, or you lose the rest of the list.
2. **Use a dummy to avoid special cases** — a sentinel node before the head means you never need separate logic for "what if we delete the head?"
3. **Draw it out** — linked list bugs are almost always pointer-order bugs. Drawing the before/after state of 3-4 nodes on paper catches them instantly.

#### 4) Fast Recognition Cues
- The input is explicitly a `ListNode` or linked list.
- The problem asks to **reverse**, **merge**, **reorder**, **partition**, or **detect a cycle** in a list.
- You need to find the **middle** or **kth from end** — classic fast/slow or two-pass pattern.
- The problem asks for **in-place** modification with O(1) space — linked lists support this naturally since rewiring pointers doesn't require extra memory.
- Words like **"node"**, **"pointer"**, **"next"** appear in the problem.
- The problem involves **adding numbers** represented as linked lists (carry propagation).

#### 5) When NOT to Use This Pattern
- **Random access needed:** If you need to access the i-th element frequently, an array is better. Linked lists require O(n) traversal to reach index i.
- **The input is an array:** Don't convert an array to a linked list just to use linked list techniques. Two-pointer on arrays is simpler.
- **Heavy searching:** If you need to find elements by value repeatedly, a hash map or BST is more appropriate. Linked lists require O(n) search.
- **The problem involves subsequences or subarrays:** These are array/string concepts, not linked list concepts.

#### 6) Universal Solve Framework
1. **Identify the operation type:** Is this a traversal, reversal, merge, cycle detection, or structural modification?
2. **Decide on dummy node:** If the head might change (deletion, insertion at head, merging), create `dummy = ListNode(0); dummy.next = head`. This eliminates null-head edge cases.
3. **Draw the pointer transitions:** Sketch 3-4 nodes. Draw arrows for the current state. Draw arrows for the desired state. Identify which pointers need to change and in what order.
4. **Choose traversal strategy:**
   - Simple traversal: single pointer.
   - Middle/cycle: fast and slow pointers.
   - Kth from end: two pointers with k-step offset.
   - Reversal: three pointers (prev, curr, nxt).
5. **Implement with save-before-cut discipline:** Always `nxt = curr.next` before `curr.next = something_else`.
6. **Return `dummy.next`** if you used a dummy node, otherwise return the appropriate head.

#### 7) Common Mistakes & Pitfalls
1. **Losing the rest of the list:** Overwriting `curr.next` before saving it means you've disconnected everything after `curr`. Always use a temp variable.
2. **Forgetting the dummy node:** Writing special-case code for "if head is None" or "if we need to delete head" when a dummy node would eliminate all of it. If your code has more than one return path, consider a dummy.
3. **Infinite loops from incorrect cycle handling:** When rewiring in a cycle-related problem, if you don't properly break the cycle, your traversal never terminates.
4. **Off-by-one with fast pointer:** The condition `while fast and fast.next` is crucial. Using just `while fast` causes a null pointer error on `fast.next.next` when the list has even length.
5. **Not handling empty list or single-node list:** Always test your solution mentally with `head = None` and `head = ListNode(1)`. These are the most common edge cases interviewers check.

#### 8) Worked Examples (Full Python)

##### Example A: 206. Reverse Linked List
```python
class Solution:
    def reverseList(self, head):
        prev = None
        curr = head
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt
        return prev
```

**Line-by-line explanation:**

- `prev = None` — Initialize the "previous" pointer to None. After reversal, the original head will point to None (it becomes the tail), so the first node's new `next` should be None. This variable tracks the already-reversed portion of the list. This pattern generalizes to any problem where you need to build a result by processing nodes one at a time.
- `curr = head` — Start processing from the head of the list. `curr` is the node we're currently rewiring.
- `while curr:` — Continue until we've processed every node. When `curr` is None, we've gone past the last node. This is the standard linked list traversal condition.
- `nxt = curr.next` — **Save before you cut.** Store the next node before we overwrite `curr.next`. Without this line, we'd lose access to the rest of the list after rewiring. This is the single most important line in any linked list modification.
- `curr.next = prev` — **The reversal step.** Point the current node backward instead of forward. This is the actual pointer surgery — one line changes the direction of the edge.
- `prev = curr` — Advance `prev` to the current node. The current node is now part of the reversed portion. This "shifts the window" of what's been processed.
- `curr = nxt` — Advance `curr` to the saved next node. Move to the next unprocessed node. Using the saved reference ensures we haven't lost our place.
- `return prev` — After the loop, `curr` is None and `prev` points to the last node we processed, which is the new head of the reversed list. We don't return `curr` (that's None) or `head` (that's now the tail).

**Complexity:** O(n) time — we visit each node exactly once. O(1) space — we only use three pointer variables regardless of list size. This is optimal because you must visit every node to reverse it, and you can't do it in fewer than n pointer operations.

##### Example B: 141. Linked List Cycle
```python
class Solution:
    def hasCycle(self, head) -> bool:
        slow = fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```

**Line-by-line explanation:**

- `slow = fast = head` — Both pointers start at the head. The slow pointer will move 1 step per iteration, the fast pointer 2 steps. If there's a cycle, fast will eventually catch up to slow from behind. This is Floyd's Tortoise and Hare algorithm.
- `while fast and fast.next:` — Continue while fast can take two steps. We check `fast` (not None) and `fast.next` (not None) because `fast.next.next` would crash if either is None. If fast reaches None, there's no cycle — the list has an end. This two-part check is essential for even-length and odd-length lists.
- `slow = slow.next` — Move slow one step forward. Slow covers n/2 nodes by the time fast covers n nodes.
- `fast = fast.next.next` — Move fast two steps forward. The speed difference of 1 step per iteration means fast closes the gap by 1 node each iteration inside a cycle, guaranteeing they meet.
- `if slow == fast:` — If both pointers reference the same node, they've met inside the cycle. This is identity comparison (same node object), not value comparison. In a cycle of length C, they'll meet within C iterations of entering the cycle.
- `return True` — A meeting point was found, confirming a cycle exists.
- `return False` — The fast pointer reached the end of the list (None), so there's no cycle. A list with a cycle has no end.

**Complexity:** O(n) time — in the worst case, slow traverses the entire list once. If there's a cycle of length C, after slow enters the cycle, fast catches up in at most C steps. O(1) space — only two pointer variables, no matter the list size. This is why Floyd's algorithm is preferred over the hash set approach (which uses O(n) space to store visited nodes).

#### 9) Additional Practice
- 21. Merge Two Sorted Lists
- 19. Remove Nth Node From End of List
- 143. Reorder List
- 2. Add Two Numbers

---

### Trees
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** BST Insert and Remove, Depth-First Search, Breadth-First Search, BST Sets and Maps, Iterative DFS.
- **Connected structures:** `TreeNode`, recursion stack, queue for BFS, explicit stack for iterative DFS.

**Term Definitions:**
- **Tree:** A hierarchical data structure with a root node and zero or more child subtrees. Each node has exactly one parent (except the root). No cycles.
- **Binary Tree:** A tree where each node has at most two children: `left` and `right`.
- **Binary Search Tree (BST):** A binary tree where for every node, all values in the left subtree are less than the node's value, and all values in the right subtree are greater. This ordering enables O(h) search, insert, and delete.
- **TreeNode:** The standard node class: `class TreeNode: def __init__(self, val=0, left=None, right=None)`.
- **Depth-First Search (DFS):** A traversal that explores as deep as possible before backtracking. Three orderings: preorder (node, left, right), inorder (left, node, right), postorder (left, right, node).
- **Breadth-First Search (BFS) / Level-Order Traversal:** A traversal that visits all nodes at depth d before visiting any node at depth d+1. Implemented with a queue.
- **BST Insert and Remove:** Operations that maintain the BST property. Insert follows the search path to a null child. Remove has three cases: leaf (delete), one child (bypass), two children (replace with inorder successor/predecessor).
- **BST Sets and Maps:** Using a BST as the underlying structure for a sorted set or sorted map, enabling O(log n) ordered operations. Python's `SortedList` from `sortedcontainers` is the practical equivalent.
- **Iterative DFS:** DFS implemented with an explicit stack instead of recursion. Necessary when recursion depth could overflow the call stack (very deep trees), or when you need finer control over traversal state.

#### 2) Subtopic Deep Dives

##### BST Insert and Remove
- **Definition:** Insert places a new value in the correct position to maintain BST ordering. Remove deletes a node while preserving BST ordering, handling three cases based on the node's children.
- **When you encounter it:** Problems asking you to build a BST from a sequence, delete nodes from a BST, or implement a data structure with ordered operations.
- **Core implementation pattern:**
  - Insert: recursively go left if value < node.val, right if value > node.val, until you find a null spot.
  - Remove: find the node, then handle leaf / one-child / two-children cases.
- **Key insight:** For the two-children case, replace the node's value with its inorder successor (smallest value in right subtree), then delete the successor. This transforms a hard delete into an easy one.

##### Depth-First Search (DFS)
- **Definition:** Recursively (or iteratively with a stack) explore one branch fully before moving to the next.
- **When you encounter it:** Path problems, subtree aggregation, tree validation, serialization — almost any tree problem.
- **Core implementation pattern:**
  ```
  def dfs(node):
      if not node: return base_case
      left = dfs(node.left)
      right = dfs(node.right)
      return combine(node.val, left, right)
  ```
- **Key insight:** The key decision is what your recursive function returns. Define this precisely ("returns the height of the subtree," "returns True if the subtree is valid") and the rest follows naturally.

##### Breadth-First Search (BFS)
- **Definition:** Visit nodes level by level using a queue. Process all nodes at the current depth before moving deeper.
- **When you encounter it:** Level-order traversal, finding shortest path in unweighted trees, "right side view," "zigzag" traversal, or any problem that groups nodes by depth.
- **Core implementation pattern:**
  ```
  queue = deque([root])
  while queue:
      for _ in range(len(queue)):  # process one level
          node = queue.popleft()
          if node.left: queue.append(node.left)
          if node.right: queue.append(node.right)
  ```
- **Key insight:** The `for _ in range(len(queue))` trick lets you process exactly one level per outer iteration. Snapshot the queue length before the inner loop, because the queue grows as you add children.

##### Iterative DFS
- **Definition:** DFS using an explicit stack instead of the function call stack.
- **When you encounter it:** When the tree could be very deep (risk of stack overflow), or when you need to pause/resume traversal (e.g., BST iterator, LeetCode 173).
- **Core implementation pattern (inorder):**
  ```
  stack, curr = [], root
  while stack or curr:
      while curr:
          stack.append(curr)
          curr = curr.left
      curr = stack.pop()
      process(curr)
      curr = curr.right
  ```
- **Key insight:** The inner `while curr` loop pushes all left children — this simulates the recursive calls diving left. Each `pop` is like returning from a recursive call.

#### 3) Key Insight / Mental Model
Every tree problem boils down to one question: **"What information does each node need from its children, and what does it pass up to its parent?"**

Think of it as a company org chart. Each employee (node) collects reports from their direct reports (children), combines them with their own data, and sends a summary up to their manager (parent). Your job is to define: (1) what the "report" looks like (the return type), and (2) how to combine child reports (the recursive logic).

For BSTs specifically, the inorder traversal gives you a sorted sequence — this is the BST superpower. Any problem that needs sorted order from a BST should immediately make you think "inorder."

#### 4) Fast Recognition Cues
- Input is a `TreeNode` or described as a binary tree / BST.
- Words: **depth**, **height**, **level**, **ancestor**, **descendant**, **subtree**, **path**, **root-to-leaf**.
- **Aggregation language:** "sum of all nodes," "count leaves," "max path sum" — these are postorder (collect from children, combine).
- **Validation language:** "is it a valid BST," "is it balanced," "are two trees identical" — DFS with constraints passed top-down.
- **Level-by-level:** "right side view," "average of levels," "zigzag" — BFS.
- **BST with ordering:** "kth smallest," "successor/predecessor," "range sum" — leverage BST property with inorder or pruned search.

#### 5) When NOT to Use This Pattern
- **The data is a graph, not a tree:** If nodes can have multiple parents or cycles exist, you need graph algorithms (BFS/DFS with a visited set), not tree recursion. Trees are a special case of graphs (connected, acyclic, undirected).
- **The problem is about arrays/strings with tree-like recursion (e.g., divide and conquer):** While the recursion structure is tree-shaped, the actual data structure isn't a tree. Use the divide-and-conquer pattern instead.
- **You need random access by index:** Trees give O(log n) access in balanced BSTs but O(n) in worst case. If you need O(1) index access, use an array.
- **The tree is given as an adjacency list:** This is a graph problem disguised with tree language. Root it first, then apply tree techniques.

#### 6) Universal Solve Framework
1. **Identify the traversal order:**
   - Need to process children before the current node? → **Postorder** (height, subtree sum, diameter).
   - Need to process the current node before children? → **Preorder** (serialization, copying, passing constraints down).
   - Need sorted order from a BST? → **Inorder**.
   - Need level-by-level processing? → **BFS**.
2. **Define the recursive return type:** Be precise. "Returns an integer representing the height." "Returns a boolean indicating validity." "Returns a tuple (is_balanced, height)." If you need multiple pieces of information, return a tuple.
3. **Write the base case:** Usually `if not node: return ...`. For height it's 0, for validity it's True, for sum it's 0.
4. **Write the recursive case:** Recurse on `node.left` and `node.right`, then combine results with `node.val`.
5. **Handle global state if needed:** For problems like diameter or max path sum where the answer isn't the root's return value, use a nonlocal variable or instance variable updated at each node.
6. **For BST problems, exploit ordering:** Pass `(low, high)` bounds for validation. Use inorder traversal for kth element. Prune branches that can't contain the answer.

#### 7) Common Mistakes & Pitfalls
1. **Confusing height vs. depth:** Height is measured from the node down to the deepest leaf (bottom-up). Depth is measured from the root down to the node (top-down). Mixing these up leads to wrong base cases and off-by-one errors.
2. **Returning early without checking both subtrees:** In problems like "path sum," checking only one subtree and returning early can miss valid paths through the other subtree. Always process both children unless you can provably prune.
3. **BST validation with only parent check:** Checking `node.left.val < node.val` only validates against the immediate parent. A left child's right subtree could violate the BST property with respect to an ancestor. Always pass bounds.
4. **Forgetting that the answer might not be at the root:** In diameter, max path sum, and longest path problems, the optimal answer might pass through an internal node without going through the root. Use a global variable to track the best seen at any node.
5. **BFS without level separation:** If you need per-level processing, you must snapshot `len(queue)` before the inner loop. Without this, you'll mix nodes from different levels in the same iteration.

#### 8) Worked Examples (Full Python)

##### Example A: 104. Maximum Depth of Binary Tree
```python
class Solution:
    def maxDepth(self, root) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```

**Line-by-line explanation:**

- `def maxDepth(self, root) -> int:` — The function takes a TreeNode root and returns an integer representing the maximum depth (number of nodes along the longest root-to-leaf path). Defining the return meaning clearly is the first step in any tree recursion problem.
- `if not root:` — Base case: if the node is None (empty subtree), we've gone past a leaf. This is the termination condition for the recursion. Every recursive tree function needs this check to avoid accessing `.left` or `.right` on None.
- `return 0` — An empty tree has depth 0. This is the base case value. Some problems use -1 or 1 here depending on whether depth counts nodes or edges — read the problem carefully.
- `return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))` — **The recursive case.** Recurse on both children to get their depths, take the maximum (the deeper subtree determines the overall depth), and add 1 for the current node. This is postorder: we need child results before we can compute the current node's result. This pattern generalizes to any "aggregate from children" problem — just change `max` to `sum`, `+`, `and`, etc.

**Complexity:** O(n) time — every node is visited exactly once. O(h) space — the recursion stack goes as deep as the tree's height. For a balanced tree, h = O(log n). For a skewed tree (essentially a linked list), h = O(n). This is optimal because you must examine every node to determine the maximum depth.

##### Example B: 98. Validate Binary Search Tree
```python
class Solution:
    def isValidBST(self, root) -> bool:
        def dfs(node, low, high):
            if not node:
                return True
            if not (low < node.val < high):
                return False
            return dfs(node.left, low, node.val) and dfs(node.right, node.val, high)

        return dfs(root, float('-inf'), float('inf'))
```

**Line-by-line explanation:**

- `def dfs(node, low, high):` — Define a helper that checks whether `node`'s subtree is a valid BST, given that all values must be strictly between `low` and `high`. Passing bounds top-down is the correct way to validate a BST — it accounts for all ancestors, not just the immediate parent. This "constraint narrowing" pattern appears in many tree problems.
- `if not node:` — Base case: an empty subtree is trivially a valid BST. A None child doesn't violate any ordering constraint.
- `return True` — An empty tree satisfies the BST property vacuously.
- `if not (low < node.val < high):` — Check whether the current node's value is within the allowed range. Python's chained comparison `low < node.val < high` is equivalent to `low < node.val and node.val < high`. If the value is out of range, this subtree violates the BST property. This catches violations that a naive "check only parent" approach would miss.
- `return False` — The current node violates BST ordering; no need to check further.
- `return dfs(node.left, low, node.val) and dfs(node.right, node.val, high)` — Recurse on both children with tightened bounds. For the left child, the upper bound narrows to `node.val` (everything in the left subtree must be less than the current node). For the right child, the lower bound narrows to `node.val` (everything must be greater). The `and` short-circuits: if the left subtree is invalid, we don't bother checking the right. This generalizes: any time you need to pass constraints down a tree, use extra parameters.
- `return dfs(root, float('-inf'), float('inf'))` — Start the recursion with the widest possible bounds. The root can be any value, so the initial range is (-infinity, infinity). Using `float('-inf')` and `float('inf')` handles all integer values cleanly.

**Complexity:** O(n) time — each node is visited exactly once, and each visit does O(1) work (one comparison, two recursive calls). O(h) space — recursion stack depth equals the tree height. For a balanced BST, h = O(log n). This is optimal: you must inspect every node because a single invalid node anywhere in the tree makes the whole BST invalid.

#### 9) Additional Practice
- 226. Invert Binary Tree
- 230. Kth Smallest Element in a BST
- 199. Binary Tree Right Side View
- 236. Lowest Common Ancestor of a Binary Tree

---

### Tries
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** Trie.
- **Connected structures:** trie node with children map and terminal flag.

**Term Definitions:**
- **Trie (Prefix Tree):** A tree-like data structure where each node represents a single character. Paths from root to nodes represent prefixes of stored strings. Unlike a hash set of strings, a trie shares common prefixes, making prefix queries efficient.
- **TrieNode:** A node containing (1) a dictionary mapping characters to child TrieNodes (`children`), and (2) a boolean flag (`is_end` / `end`) indicating whether a complete word ends at this node.
- **Terminal/End Flag:** A boolean on each node indicating that the path from the root to this node forms a complete word. Without this, you can't distinguish between "app" being a prefix of "apple" vs. "app" being an actual stored word.
- **Prefix Query:** Checking whether any stored word starts with a given prefix. Tries answer this in O(L) time where L is the prefix length, regardless of how many words are stored.
- **Children Map:** Typically a dictionary (`{}`) or a fixed-size array (size 26 for lowercase English letters). The dictionary approach is more flexible; the array approach is faster for known alphabets.

#### 2) Subtopic Deep Dives

##### Trie
- **Definition:** A tree where each edge represents a character and each root-to-node path represents a prefix. Inserting "cat" and "car" creates a shared path c→a, then branches to t and r.
- **When you encounter it:** Problems involving (1) prefix matching across many strings, (2) autocomplete, (3) word search on a board with a dictionary, (4) finding longest common prefix, (5) replacing words with their shortest prefix from a dictionary.
- **Core implementation pattern:**
  - **Insert:** Walk through each character of the word. At each step, if the character isn't in the current node's children, create a new TrieNode. Move to the child. After the last character, set `end = True`.
  - **Search:** Walk through each character. If any character is missing from children, return False. After the last character, return `node.end` (True only if a complete word ends here).
  - **StartsWith:** Same as search, but return True after successfully walking through all prefix characters (don't check `end`).
- **Key insight:** A trie turns string comparison from O(L) per lookup in a hash set to O(L) per lookup with prefix-sharing — the same asymptotic cost, but the trie also supports prefix queries, wildcard matching, and lexicographic ordering that hash sets cannot. The real power is when you need to search for all words with a given prefix or prune a word search early.

#### 3) Key Insight / Mental Model
Think of a trie as a **decision tree for spelling**. At each node, you choose the next letter. If you're looking for words starting with "ca", you walk to c, then a, and everything below that point is a word starting with "ca" — you don't need to scan the whole dictionary.

The key "aha" for interview problems: a trie lets you **prune an exponential search**. In Word Search II (LeetCode 212), instead of running a separate DFS for each word in the dictionary, you build a trie of all words and run one DFS that simultaneously searches for all words. The trie prunes branches that can't lead to any dictionary word, cutting the search space dramatically.

#### 4) Fast Recognition Cues
- The problem involves **many strings** and repeated **prefix queries**.
- The words **"prefix"**, **"starts with"**, or **"autocomplete"** appear.
- You need to **search a dictionary efficiently** while exploring a grid or string.
- The problem asks for **wildcard matching** with `.` or `*` characters (trie + DFS for wildcard branches).
- You're given a list of words and need to find **common prefixes**, **shortest unique prefix**, or **replace words with prefixes**.
- Brute force involves checking every word in the dictionary for every query — trie amortizes this.
- The constraint mentions a **large dictionary** (10^4 to 10^5 words) combined with a search space (grid, string).

#### 5) When NOT to Use This Pattern
- **Single string lookups:** If you just need to check "is this word in the dictionary?" without prefix queries, a hash set is simpler and equally fast (O(L) per lookup).
- **Small dictionary:** If the dictionary has only a few words, the overhead of building a trie isn't worth it. Just iterate through the words.
- **Suffix queries:** If you need "does any word end with this suffix?" a trie on reversed strings works, but this is unusual enough that you should consider other approaches first.
- **Numeric data:** While tries can store numbers (using digits as characters), other structures like segment trees or binary indexed trees are usually more appropriate for numeric range queries.
- **Memory-constrained environments:** Tries can use significantly more memory than a hash set because each node has a children dictionary. For very large dictionaries with little prefix overlap, the overhead can be substantial.

#### 6) Universal Solve Framework
1. **Define the TrieNode:** Create a class with `children = {}` and `end = False`. If the problem needs extra data per node (e.g., the word itself, a count, a reference), add those fields.
2. **Build the trie:** Insert all dictionary words. This is O(N * L) where N is the number of words and L is the average word length.
3. **Implement the query operation:**
   - For simple search/prefix: walk the trie character by character.
   - For wildcard search (`.` matches any character): at a `.`, recurse into all children.
   - For board search: combine trie traversal with grid DFS. At each grid cell, check if the current character exists in the trie node's children. If not, prune this path.
4. **Optimize if needed:**
   - **Pruning:** In Word Search II, after finding a word, remove it from the trie (set `end = False`, prune empty branches) to avoid finding it again.
   - **Store the word at the terminal node:** Instead of reconstructing the word from the path, store `node.word = word` at insertion time, and read it directly when `node.end` is True.
5. **Return results.**

#### 7) Common Mistakes & Pitfalls
1. **Confusing search and startsWith:** `search("app")` should return False if only "apple" is stored (no word ends at "app"). `startsWith("app")` should return True. The difference is checking `node.end` vs. not checking it. Mixing these up is the most common trie bug.
2. **Mutating a shared reference:** In Python, writing `self.children = {}` in the class body (not in `__init__`) makes all nodes share the same dictionary. Always initialize `children` in `__init__`.
3. **Not pruning in board search:** In Word Search II, if you find a word but don't mark it as found (or remove it from the trie), you'll find duplicates. Always set `node.end = False` after collecting a found word.
4. **Using a list of 26 elements instead of a dict when the alphabet varies:** If the problem includes uppercase, digits, or special characters, a fixed-size array of 26 won't work. Use a dictionary for flexibility unless the problem guarantees lowercase-only.
5. **Forgetting that trie depth equals word length:** The space complexity is O(N * L) in the worst case (no shared prefixes). Don't assume the trie is small just because there are few words — long words mean deep tries.

#### 8) Worked Examples (Full Python)

##### Example: 208. Implement Trie (Prefix Tree)
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end = False


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        node = self.root
        for ch in word:
            if ch not in node.children:
                node.children[ch] = TrieNode()
            node = node.children[ch]
        node.end = True

    def search(self, word: str) -> bool:
        node = self.root
        for ch in word:
            if ch not in node.children:
                return False
            node = node.children[ch]
        return node.end

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for ch in prefix:
            if ch not in node.children:
                return False
            node = node.children[ch]
        return True
```

**Line-by-line explanation:**

**TrieNode class:**
- `class TrieNode:` — Define the building block of the trie. Each node represents a point in the prefix tree after some sequence of characters.
- `def __init__(self):` — Constructor for each node. Every node is initialized independently with its own state.
- `self.children = {}` — A dictionary mapping characters to child TrieNodes. Using a dict (rather than a fixed-size array) allows any alphabet and uses memory proportional to actual branching. An empty dict means no words continue through this node yet.
- `self.end = False` — A flag indicating whether a complete word ends at this node. This distinguishes "a prefix that happens to exist because a longer word passes through" from "an actual word that was inserted." For example, inserting "apple" creates nodes for a, p, p, l, e — but only the 'e' node has `end = True`.

**Trie class:**
- `class Trie:` — The main trie interface providing insert, search, and startsWith operations.
- `def __init__(self):` — Initialize an empty trie.
- `self.root = TrieNode()` — Create the root node. The root represents the empty prefix "". All words branch from here. The root itself never has `end = True` (unless you insert the empty string).

**insert method:**
- `def insert(self, word: str) -> None:` — Add a word to the trie. After this call, both `search(word)` and `startsWith(any prefix of word)` will return True.
- `node = self.root` — Start at the root. We'll walk down the trie, creating nodes as needed.
- `for ch in word:` — Process each character of the word in order. Each character corresponds to one level deeper in the trie.
- `if ch not in node.children:` — Check if a child for this character already exists. If another word with the same prefix was inserted before, the child will already be there.
- `node.children[ch] = TrieNode()` — Create a new node for this character. This extends the trie with a new branch. The new node starts with empty children and `end = False`.
- `node = node.children[ch]` — Move down to the child node. After this, `node` represents the prefix consisting of all characters processed so far.
- `node.end = True` — Mark the final node as a word endpoint. This is what makes `search` return True for this exact word. Without this line, insert would only create the prefix path but never mark any word as complete.

**search method:**
- `def search(self, word: str) -> bool:` — Check if the exact word (not just a prefix) exists in the trie.
- `node = self.root` — Start at the root, same as insert.
- `for ch in word:` — Walk through each character of the search word.
- `if ch not in node.children:` — If the next character doesn't exist in the trie, the word was never inserted (or any word with this prefix). Early return saves time.
- `return False` — The word is not in the trie. This is the power of the trie: we can reject a word as soon as we find a character mismatch, without checking the rest.
- `node = node.children[ch]` — Move to the child node. Continue walking the trie.
- `return node.end` — After processing all characters, check if a complete word ends here. If `end` is True, the word was inserted. If `end` is False, this path exists only as a prefix of some longer word (e.g., searching "app" when only "apple" was inserted). This is the critical difference between `search` and `startsWith`.

**startsWith method:**
- `def startsWith(self, prefix: str) -> bool:` — Check if any inserted word starts with the given prefix.
- `node = self.root` — Start at the root.
- `for ch in prefix:` — Walk through each character of the prefix.
- `if ch not in node.children:` — If any character is missing, no word with this prefix exists.
- `return False` — No inserted word has this prefix.
- `node = node.children[ch]` — Move deeper into the trie.
- `return True` — All prefix characters exist in the trie, so at least one word starts with this prefix. Notice we don't check `node.end` — we don't care whether a word ends here, only whether the prefix path exists. Any word that passes through this node has this prefix.

**Complexity:** O(L) time per operation, where L is the length of the word or prefix being processed. Each operation traverses at most L nodes, doing O(1) work per node (dictionary lookup/insert). O(N * L) space for the entire trie in the worst case, where N is the number of inserted words and L is the average length. In the best case (many shared prefixes), the space is much less. This is optimal for prefix operations because you must examine every character of the input at minimum.

#### 9) Additional Practice
- 211. Design Add and Search Words Data Structure
- 212. Word Search II
- 648. Replace Words



### Heap/Priority Queue
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** Heap Priorities, Push and Pop, Heapify, Two Heaps.
- **Connected structures:** min-heap/max-heap (negated values), tuples for priorities, arrays (heap is stored as a complete binary tree in an array), hash maps (for frequency counting before heap insertion).
- **Heap:** A complete binary tree stored in an array where every parent node satisfies the heap property (smaller than children for min-heap, larger for max-heap). Python's `heapq` module implements a min-heap.
- **Priority Queue:** An abstract data type where each element has a priority and the highest-priority element is always removed first. A heap is the standard implementation.
- **Complete Binary Tree:** A tree where every level is fully filled except possibly the last, which is filled left to right. This property allows array storage without pointers.

#### 2) Subtopic Deep Dives

**Heap Priorities**
- **Definition:** The ordering rule that determines which element sits at the top of the heap. In a min-heap, the smallest value has highest priority; in a max-heap, the largest.
- **When you encounter it:** Any time you need repeated access to the "best" element — smallest distance, highest frequency, earliest deadline.
- **Core pattern:** Use tuples `(priority, tiebreaker, value)` when you need composite ordering. Python compares tuples left to right.
- **Key insight:** Python only provides min-heap. Simulate max-heap by negating values: `heappush(h, -val)` then `ans = -heappop(h)`.

**Push and Pop**
- **Definition:** `heappush` adds an element and bubbles it up to restore the heap property. `heappop` removes the root (min element) and sifts the last element down.
- **When you encounter it:** Every heap problem uses these operations. Push is O(log n), pop is O(log n).
- **Core pattern:** Push all candidates, pop to extract the current best. For top-k, push then conditionally pop to keep the heap bounded.
- **Key insight:** `heappushpop(h, val)` is faster than separate push then pop — it avoids one sift operation.

**Heapify**
- **Definition:** `heapq.heapify(lst)` converts an existing list into a valid heap in-place in O(n) time, faster than n individual pushes at O(n log n).
- **When you encounter it:** When you already have all the data upfront and want to build the heap once rather than inserting one by one.
- **Core pattern:** `nums_copy = nums[:]; heapq.heapify(nums_copy)` — then pop k times for kth-smallest.
- **Key insight:** Heapify is O(n) because most nodes are near the bottom and need very few sift-down steps. The math works out to O(n) total swaps.

**Two Heaps**
- **Definition:** Maintain two heaps simultaneously — typically a max-heap for the lower half and a min-heap for the upper half of a data stream — to efficiently track the median.
- **When you encounter it:** Median from data stream, balancing two halves, sliding window median.
- **Core pattern:** After each insertion, rebalance so the heaps differ in size by at most 1. The median is the top of the larger heap (or average of both tops).
- **Key insight:** Two heaps give you O(log n) insert and O(1) median — you are maintaining a sorted partition without sorting.

#### 3) Key Insight / Mental Model
Think of a heap as a "lazy sorter." You do not need the entire collection sorted — you only need fast access to the current best element. A heap gives you O(log n) insert and O(log n) extract-min/max, which beats sorting (O(n log n)) when you are interleaving insertions and extractions. The mental model: imagine a funnel where the smallest item always rolls to the bottom opening. You can toss items in from the top at any time and always pull the smallest from the bottom.

#### 4) Fast Recognition Cues
- The problem says "kth largest," "kth smallest," or "top k."
- You need to repeatedly extract the minimum or maximum while inserting new elements.
- Streaming or online data — elements arrive one at a time and you need a running answer.
- Merging k sorted sequences (each pop gives the next global minimum).
- The problem involves scheduling by priority or deadline.
- You see "median" in a data stream context.
- A greedy approach needs the current best candidate at each step (e.g., Dijkstra's algorithm).

#### 5) When NOT to Use This Pattern
- **You need the kth element once from static data:** Quickselect gives O(n) average. A heap is O(n log k) — fine but not optimal.
- **You need all elements sorted:** Just sort. A heap-based sort has worse cache performance than Timsort.
- **You need to look up or delete arbitrary elements:** Heaps only give O(1) access to the root. Use a balanced BST or sorted container for arbitrary access.
- **The problem is about contiguous subarrays:** This is usually sliding window or prefix sums, not a heap (unless the window needs a running median).
- **Fixed-size data with a single min/max query:** Just use `min()` or `max()` in O(n). A heap adds unnecessary complexity.

#### 6) Universal Solve Framework
1. **Decide the heap invariant.** Ask: "Do I need the smallest or largest element on top?" For top-k-largest, use a min-heap of size k (the smallest of your k best sits on top so you can eject it when something better arrives). For top-k-smallest, use a max-heap of size k.
2. **Store tuples when tie-break keys are needed.** `(priority, sequence_number, value)` avoids comparison errors on unhashable or equal-priority items.
3. **Keep heap size bounded for top-k memory control.** After each push, check `if len(heap) > k: heappop(heap)`. This keeps space at O(k) and time per element at O(log k).
4. **For median problems, maintain two heaps and rebalance after each insertion.** Max-heap (negated) for lower half, min-heap for upper half. After inserting, move elements between heaps so sizes differ by at most 1.
5. **Consider heapify when all data is available upfront.** Building the heap in O(n) then popping k times gives O(n + k log n), which beats O(n log n) sorting when k is small.

#### 7) Common Mistakes & Pitfalls
1. **Forgetting Python's heapq is min-heap only.** People try to use it as a max-heap and get inverted results. Always negate values for max-heap behavior: `heappush(h, -val)`.
2. **Not using tuples for tie-breaking.** If two elements have the same priority and the value is not comparable (e.g., a list), Python raises a TypeError. Always include a unique tie-breaker like an index: `(priority, index, value)`.
3. **Popping from an empty heap.** Always check `if heap:` before `heappop`. In interview stress, this edge case is easy to forget.
4. **Confusing "kth largest" with "kth smallest."** Kth largest uses a min-heap of size k (the top is the kth largest). Kth smallest uses a max-heap of size k. Getting this backwards is a common interview error.
5. **Using a heap when a simple sort suffices.** If you process all data before needing results, sorting is simpler and often faster in practice. Heaps shine when data arrives incrementally or you only need k elements from n.

#### 8) Worked Examples (Full Python)
##### Example A: 215. Kth Largest Element in an Array
```python
import heapq

class Solution:
    def findKthLargest(self, nums: list[int], k: int) -> int:
        heap = []
        for x in nums:
            heapq.heappush(heap, x)
            if len(heap) > k:
                heapq.heappop(heap)
        return heap[0]
```

**Line-by-line explanation:**

- `import heapq` — Imports Python's heap module, which provides min-heap operations. You will use this in virtually every heap problem.
- `heap = []` — Initializes an empty list that will serve as our min-heap. Python heaps are just lists with the heap invariant maintained by the heapq functions.
- `for x in nums:` — Iterates through every number in the input. This is the streaming pattern: process elements one at a time, maintaining the heap invariant after each.
- `heapq.heappush(heap, x)` — Adds x to the heap and sifts it up to maintain the min-heap property. Cost: O(log k) since the heap is bounded to size k. This generalizes to any problem where you feed candidates into a bounded heap.
- `if len(heap) > k:` — Checks whether the heap has exceeded the desired size k. This is the bounded-heap guard that keeps only the k largest elements.
- `heapq.heappop(heap)` — Removes the smallest element from the heap. Since we want the k largest, the smallest of those k is the one we discard. After this, the heap contains exactly the k largest elements seen so far. This is the core insight: a min-heap of size k naturally retains the k largest values because it ejects the smallest.
- `return heap[0]` — Returns the root of the min-heap, which is the smallest among the k largest elements — i.e., the kth largest overall. `heap[0]` is always the minimum in a min-heap, accessible in O(1).

**Complexity:** O(n log k) time because each of n elements costs O(log k) for push/pop on a size-k heap. O(k) space for the heap. This is better than O(n log n) sorting when k is much smaller than n.

##### Example B: 973. K Closest Points to Origin
```python
import heapq

class Solution:
    def kClosest(self, points: list[list[int]], k: int) -> list[list[int]]:
        heap = []
        for x, y in points:
            dist = x * x + y * y
            heapq.heappush(heap, (-dist, x, y))
            if len(heap) > k:
                heapq.heappop(heap)
        return [[x, y] for _, x, y in heap]
```

**Line-by-line explanation:**

- `import heapq` — Imports the heap module. Same as every heap problem.
- `heap = []` — Empty list to hold our max-heap (simulated via negation). We use a max-heap here because we want the k smallest distances, so we eject the largest distance when the heap exceeds size k.
- `for x, y in points:` — Unpacks each point's coordinates. This is the streaming loop — process one candidate at a time.
- `dist = x * x + y * y` — Computes the squared Euclidean distance. We skip the square root because it is monotonic — comparing squared distances gives the same ordering. This is a common optimization you will see in any distance-based problem.
- `heapq.heappush(heap, (-dist, x, y))` — Pushes a tuple with negated distance. Negation turns the min-heap into a max-heap: the point with the largest distance (most negative value after negation) will NOT be at the top — actually, the point with the largest original distance corresponds to the most negative stored value, which the min-heap keeps deepest. Wait — the most negative value (smallest stored) corresponds to the largest distance, so `heappop` removes the largest-distance point. This is exactly what we want: eject the farthest point. The tuple includes (x, y) so we can reconstruct the answer.
- `if len(heap) > k:` — Bounded-heap guard. Same pattern as the kth-largest problem.
- `heapq.heappop(heap)` — Removes the element with the smallest stored value, which is the most negative, which is the largest distance. This ejects the farthest point, keeping only the k closest.
- `return [[x, y] for _, x, y in heap]` — Extracts coordinates from the remaining tuples, discarding the distance. The list comprehension unpacks each tuple, skipping the negated distance with `_`.

**Complexity:** O(n log k) time, O(k) space. Optimal because we never store more than k elements and each operation on the bounded heap costs O(log k).

#### 9) Additional Practice
- 347. Top K Frequent Elements
- 621. Task Scheduler
- 295. Find Median from Data Stream
- 23. Merge k Sorted Lists

---

### Backtracking
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** Tree Maze, Subsets, Combinations, Permutations.
- **Connected structures:** recursion stack (implicit call stack used to explore decisions), path list (accumulates the current partial solution), used-set or bitmask (tracks which elements have been chosen to avoid duplicates), result list (collects all valid complete solutions).
- **Backtracking:** A systematic way to explore all possible solutions by making a choice, recursing, then undoing that choice (backtracking) to try alternatives. It is essentially DFS on the decision tree.
- **Decision Tree:** A conceptual tree where each node represents a choice point. Branches represent the options at that point. Leaves represent complete solutions or dead ends.
- **Pruning:** Cutting off branches of the decision tree early when you can determine they will not lead to valid solutions, saving significant computation.

#### 2) Subtopic Deep Dives

**Tree Maze**
- **Definition:** A problem where you explore paths through a grid or tree structure, choosing directions at each step and backtracking when you hit a dead end or violate constraints.
- **When you encounter it:** Word search in a grid, finding paths in a maze, exploring all routes from source to target in a DAG.
- **Core pattern:** Mark the current cell as visited, recurse in all valid directions, unmark on return.
- **Key insight:** The "unmark on return" step is what makes it backtracking rather than plain DFS. You need the cell available for other paths.

**Subsets**
- **Definition:** Generate all possible subsets (the power set) of a given set. Each element has a binary choice: include or exclude.
- **When you encounter it:** Problems asking for "all subsets," "all subsequences," or any scenario with 2^n possible selections.
- **Core pattern:** At index i, branch into two recursive calls — one that skips nums[i] and one that includes it. The decision tree is a perfect binary tree of depth n.
- **Key insight:** There are exactly 2^n subsets because each of n elements is independently included or excluded. The output size itself is 2^n, so no algorithm can be faster.

**Combinations**
- **Definition:** Select k items from n items where order does not matter. Unlike subsets, you have a fixed target size.
- **When you encounter it:** "Choose k elements," "all groups of size k," combination sum problems.
- **Core pattern:** Same as subsets but add a constraint: only append to results when `len(path) == k`, and prune when remaining elements cannot fill the needed slots.
- **Key insight:** Pruning is critical for combinations. If you need k - len(path) more elements but only n - i remain, prune immediately. This dramatically reduces the search space.

**Permutations**
- **Definition:** Generate all orderings of a set. Unlike combinations, order matters: [1,2] and [2,1] are different permutations.
- **When you encounter it:** "All arrangements," "all orderings," scheduling all possible sequences.
- **Core pattern:** At each level of recursion, iterate over all elements not yet used (tracked by a used-set or by swapping). Each level picks one element for the current position.
- **Key insight:** There are n! permutations. The key structural difference from subsets is that at each step you can pick any unused element, not just "the next one." This means the branching factor decreases at each level: n choices, then n-1, then n-2, etc.

#### 3) Key Insight / Mental Model
Backtracking is "DFS on the decision tree with an undo button." At every node you make a choice (add an element to your path), explore everything downstream, then undo that choice (pop from the path) before trying the next option. The power of backtracking is that you explore all possibilities systematically without needing to store them all at once — the recursion stack holds only one path at a time. Think of it like navigating a maze with a ball of string: you go as far as you can, and when you hit a wall, you follow the string back and try a different turn.

#### 4) Fast Recognition Cues
- The problem asks for "all" combinations, permutations, subsets, or partitions.
- You need to generate every valid configuration that satisfies constraints.
- The solution space is a tree of decisions with branching choices at each level.
- Constraints allow pruning — not every branch needs full exploration.
- The expected output size is exponential or factorial (2^n, n!, C(n,k)).
- The problem says "return all possible..." or "find every way to..."
- Grid-based path finding where you must explore all routes.

#### 5) When NOT to Use This Pattern
- **You only need the count, not the actual configurations:** Use DP or combinatorial math instead. Backtracking generates all solutions, which is wasteful if you only need a count.
- **You need the optimal solution (min/max), not all solutions:** DP or greedy is usually better. Backtracking explores everything, which is overkill for optimization unless the search space is small.
- **The problem has overlapping subproblems:** If the same subproblem is solved repeatedly, memoization (DP) is more efficient. Backtracking with memoization becomes top-down DP.
- **Input size is large (n > 20 for subsets, n > 10 for permutations):** The exponential/factorial growth makes backtracking too slow. Look for polynomial-time algorithms.
- **A greedy approach provably works:** If a locally optimal choice always leads to a globally optimal solution, backtracking's exhaustive search is unnecessary.

#### 6) Universal Solve Framework
1. **Define the state.** What parameters does your recursive function need? Typically: current index `i`, current path `path`, and any remaining constraints (target sum, remaining slots, etc.).
2. **Define the base case.** When is a solution complete? For subsets: `i == len(nums)`. For combinations: `len(path) == k`. For permutations: `len(path) == len(nums)`. At the base case, append `path.copy()` to results.
3. **Add choose/unchoose transitions.** The core backtracking pattern: add an element to the path, recurse, then remove it. This is the "try and undo" step.
4. **Prune invalid branches early.** Before recursing, check constraints. If the remaining elements cannot possibly lead to a valid solution, return immediately. Good pruning is the difference between TLE and AC.
5. **Handle duplicates if needed.** Sort the input first, then skip consecutive duplicate elements at the same recursion level: `if i > start and nums[i] == nums[i-1]: continue`.
6. **Append a copy of path, not the path itself.** Since path is mutated throughout recursion, you must append `path.copy()` or `path[:]`. Appending the reference gives you a list of empty lists at the end.

#### 7) Common Mistakes & Pitfalls
1. **Forgetting to copy the path when appending to results.** `ans.append(path)` appends a reference. After backtracking, path will be empty, so all entries in ans will be empty. Always use `ans.append(path.copy())`.
2. **Not handling duplicates.** If the input has duplicate elements and you do not skip them, you get duplicate subsets/combinations. Sort first, then skip: `if i > start and nums[i] == nums[i-1]: continue`.
3. **Off-by-one in the start index.** For combinations (where each element is used at most once), the next recursive call should use `i + 1`. For combination sum with unlimited reuse, pass `i` (not `i + 1`). Getting this wrong either skips valid solutions or allows invalid reuse.
4. **Not pruning aggressively enough.** Backtracking without pruning is brute force. Always check: can this branch possibly lead to a valid solution? If not, return early.
5. **Modifying the input array without restoring it.** If you mark cells visited in a grid, you must unmark them when backtracking. Forgetting this blocks valid paths from being explored.

#### 8) Worked Examples (Full Python)
##### Example A: 78. Subsets
```python
class Solution:
    def subsets(self, nums: list[int]) -> list[list[int]]:
        ans = []
        path = []

        def dfs(i: int) -> None:
            if i == len(nums):
                ans.append(path.copy())
                return
            # skip
            dfs(i + 1)
            # take
            path.append(nums[i])
            dfs(i + 1)
            path.pop()

        dfs(0)
        return ans
```

**Line-by-line explanation:**

- `ans = []` — Initializes the result list that will hold all subsets. This accumulates complete solutions across the entire recursion. Every backtracking problem needs a results container.
- `path = []` — Initializes the current partial solution. This list is shared across all recursive calls and gets modified in place (append/pop). Using a single mutable list is memory-efficient — you only ever have one path in memory.
- `def dfs(i: int) -> None:` — Defines the recursive function. The parameter `i` represents the current index in `nums` — the decision point. At each call, we decide whether to include or exclude `nums[i]`. This pattern generalizes: your recursive function's parameters define the state of the decision tree.
- `if i == len(nums):` — Base case: we have made a decision for every element. There are no more elements to include or exclude, so the current path is a complete subset.
- `ans.append(path.copy())` — Saves a copy of the current path as a valid subset. The `.copy()` is critical — without it, you would store a reference to the same list that gets mutated by later recursive calls. This is the most common backtracking bug.
- `return` — Stops recursion at the base case. Without this, we would try to access `nums[i]` out of bounds.
- `dfs(i + 1)` — The "skip" branch: recurse to the next index without adding `nums[i]` to the path. This explores all subsets that do NOT contain `nums[i]`. In the decision tree, this is the left branch.
- `path.append(nums[i])` — The "choose" step: add `nums[i]` to the current path. This is the first half of the choose/unchoose pattern. We are now exploring all subsets that DO contain `nums[i]`.
- `dfs(i + 1)` — Recurse to the next index with `nums[i]` included. This explores the right branch of the decision tree.
- `path.pop()` — The "unchoose" step: remove `nums[i]` from the path, restoring the state for the parent call. This is the backtracking step. Without it, elements would accumulate and every subset would contain every element.
- `dfs(0)` — Starts the recursion at index 0, the first decision point.
- `return ans` — Returns all collected subsets.

**Complexity:** O(n * 2^n) time. There are 2^n subsets and copying each takes O(n). The recursion stack is O(n) deep. The output itself is 2^n subsets, so this is optimal — you cannot enumerate 2^n items faster than O(2^n).

##### Example B: 46. Permutations
```python
class Solution:
    def permute(self, nums: list[int]) -> list[list[int]]:
        ans = []
        path = []
        used = [False] * len(nums)

        def dfs() -> None:
            if len(path) == len(nums):
                ans.append(path.copy())
                return
            for i in range(len(nums)):
                if used[i]:
                    continue
                used[i] = True
                path.append(nums[i])
                dfs()
                path.pop()
                used[i] = False

        dfs()
        return ans
```

**Line-by-line explanation:**

- `ans = []` — Result list for all permutations. Same role as in subsets.
- `path = []` — Current partial permutation being built. Shared and mutated across recursive calls.
- `used = [False] * len(nums)` — Boolean array tracking which elements are currently in the path. This is necessary for permutations because, unlike subsets, you can pick any unused element at each step (not just "the next one"). A set would also work, but an array is faster for small n.
- `def dfs() -> None:` — No index parameter needed because permutations do not process elements in order. Instead, at each level we scan all elements and pick any unused one.
- `if len(path) == len(nums):` — Base case: the path contains all elements, so it is a complete permutation.
- `ans.append(path.copy())` — Save a copy. Same critical `.copy()` as in subsets.
- `return` — Stop recursion at a complete permutation.
- `for i in range(len(nums)):` — Try every element as the next choice. This is the key difference from subsets: the branching factor is "all unused elements," not "include or exclude the next element."
- `if used[i]: continue` — Skip elements already in the path. Without this check, we would reuse elements and get invalid permutations.
- `used[i] = True` — Mark element as used (choose step part 1).
- `path.append(nums[i])` — Add element to path (choose step part 2).
- `dfs()` — Recurse to fill the next position.
- `path.pop()` — Remove element from path (unchoose step part 1).
- `used[i] = False` — Unmark element as used (unchoose step part 2). The choose/unchoose is a pair of operations that must mirror each other exactly.

**Complexity:** O(n * n!) time. There are n! permutations, each of length n to copy. The recursion depth is n. This is optimal — you cannot enumerate n! items faster than O(n!).

#### 9) Additional Practice
- 39. Combination Sum
- 46. Permutations
- 17. Letter Combinations of a Phone Number
- 51. N-Queens

---

### Graphs
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** Intro to Graphs, Matrix DFS, Matrix BFS, Adjacency List.
- **Connected structures:** adjacency list (dict or list of lists mapping each node to its neighbors), adjacency matrix (2D array where `matrix[i][j]` indicates an edge), queue (for BFS traversal), stack/recursion (for DFS traversal), visited set (prevents revisiting nodes and infinite loops in cyclic graphs).
- **Graph:** A collection of nodes (vertices) connected by edges. Edges can be directed (one-way) or undirected (two-way), weighted or unweighted.
- **Connected Component:** A maximal set of nodes where every node is reachable from every other node. Counting components is a fundamental graph problem.
- **BFS (Breadth-First Search):** Explores nodes level by level using a queue. Guarantees shortest path in unweighted graphs.
- **DFS (Depth-First Search):** Explores as deep as possible before backtracking, using recursion or an explicit stack. Good for reachability, cycle detection, and topological sort.

#### 2) Subtopic Deep Dives

**Intro to Graphs**
- **Definition:** Graphs model relationships between objects. Unlike trees, graphs can have cycles, multiple components, and no designated root.
- **When you encounter it:** Any problem with connections, dependencies, networks, or relationships between entities.
- **Core pattern:** Represent the graph, then traverse it. The two representation choices (adjacency list vs. matrix) and two traversal choices (BFS vs. DFS) cover nearly all graph problems.
- **Key insight:** Most graph problems reduce to: build the graph, then do BFS or DFS with some bookkeeping.

**Matrix DFS**
- **Definition:** Treating a 2D grid as an implicit graph where each cell is a node and adjacent cells (up/down/left/right) are neighbors. DFS explores connected regions by recursing into adjacent valid cells.
- **When you encounter it:** Island problems, flood fill, connected regions in a grid, word search.
- **Core pattern:** Define a recursive function that checks bounds and validity, marks the cell visited (or modifies it), then recurses in 4 directions.
- **Key insight:** The grid IS the adjacency structure — you do not need to build a separate adjacency list. Each cell has at most 4 neighbors, so the implicit graph has O(mn) edges.

**Matrix BFS**
- **Definition:** BFS on a grid, using a queue to explore cells level by level. Each level represents one step/unit of distance.
- **When you encounter it:** Shortest path in an unweighted grid, "minimum steps to reach target," rotting oranges (multi-source BFS).
- **Core pattern:** Initialize the queue with all source cells, process level by level (track distance with a counter or by processing the queue in batches), mark visited when enqueueing (not when dequeueing, to avoid duplicates).
- **Key insight:** Mark cells as visited when you ADD them to the queue, not when you process them. This prevents the same cell from being added multiple times and is the most common BFS bug.

**Adjacency List**
- **Definition:** A graph representation where each node maps to a list of its neighbors. In Python: `graph = defaultdict(list)` then `graph[u].append(v)`.
- **When you encounter it:** Problems that give you edge lists, prerequisite pairs, or connection descriptions.
- **Core pattern:** Build the adjacency list from the edge list, then traverse with BFS or DFS.
- **Key insight:** Adjacency lists use O(V + E) space and allow O(degree) neighbor iteration. They are almost always preferred over adjacency matrices for sparse graphs, which most interview problems are.

#### 3) Key Insight / Mental Model
Every graph problem has two phases: **build** and **traverse**. In the build phase, you create the graph representation (adjacency list from edges, or use the grid directly). In the traverse phase, you walk the graph with BFS or DFS, maintaining a visited set to avoid cycles. The choice between BFS and DFS is usually simple: BFS for shortest unweighted path (because it explores level by level), DFS for everything else (components, reachability, cycle detection, topological sort). Think of BFS as ripples expanding from a stone dropped in water — each ring is one step farther. Think of DFS as exploring a cave system — go as deep as you can, then backtrack.

#### 4) Fast Recognition Cues
- Objects have explicit connections, links, edges, or dependencies.
- The problem involves a grid where you move between cells.
- You need to count connected regions or components.
- "Shortest path" in an unweighted context (BFS).
- "Can you reach X from Y?" (DFS or BFS).
- Prerequisite or dependency ordering (topological sort).
- "Minimum steps/moves to transform/reach" (BFS).
- The problem gives you edge pairs or an adjacency description.
- Clone, copy, or duplicate a linked structure.
- Multi-source problems: "spread from all X simultaneously" (multi-source BFS).

#### 5) When NOT to Use This Pattern
- **The problem involves a sorted array or linked list without branching connections:** This is a linear structure, not a graph. Use two pointers, binary search, or sliding window.
- **You need shortest path in a weighted graph:** Standard BFS does not handle weights. Use Dijkstra's (with a heap) or Bellman-Ford.
- **The problem is about sequences or subarrays without structural connections:** Even if you could model it as a graph, DP or greedy is usually simpler and faster.
- **The graph is dense and you need all-pairs shortest paths:** Use Floyd-Warshall (O(V^3)) rather than running BFS/DFS from every node.
- **The problem can be solved with Union-Find more efficiently:** Component counting and connectivity queries are sometimes better served by Union-Find, especially with dynamic edge additions.

#### 6) Universal Solve Framework
1. **Build the adjacency representation.** For explicit edges: `graph = defaultdict(list); for u, v in edges: graph[u].append(v)`. For grids: the grid itself is the implicit graph — define a directions array `[(0,1),(0,-1),(1,0),(-1,0)]`.
2. **Choose traversal: DFS or BFS.** BFS for shortest unweighted path or level-order processing. DFS for reachability, component counting, cycle detection, or when the problem naturally decomposes recursively.
3. **Initialize a visited structure.** Use a set for general graphs: `visited = set()`. For grids, you can modify the grid in place (set cell to a sentinel value) to save space, or use a separate visited matrix.
4. **Track visited to avoid repeats/cycles.** For BFS: mark visited when enqueueing. For DFS: mark visited before recursing into neighbors.
5. **Process per component/source and aggregate the answer.** For counting components: loop through all nodes, start a new traversal for each unvisited node, increment count. For shortest path: BFS from the source, return the distance when you reach the target.
6. **Handle edge cases.** Empty graph, single node, disconnected components, self-loops.

#### 7) Common Mistakes & Pitfalls
1. **Marking visited on dequeue instead of enqueue (BFS).** This causes the same node to be added to the queue multiple times, wasting time and potentially causing incorrect results. Always mark visited when you add to the queue.
2. **Forgetting to handle disconnected components.** If the graph is not guaranteed to be connected, you must loop through all nodes and start a traversal from each unvisited one.
3. **Not building bidirectional edges for undirected graphs.** When the problem says "undirected," you must add both `graph[u].append(v)` and `graph[v].append(u)`. Forgetting one direction makes the graph directed.
4. **Stack overflow on large grids with recursive DFS.** Python's default recursion limit is 1000. For large grids (1000x1000), use iterative DFS with an explicit stack or BFS instead. Set `sys.setrecursionlimit` as a last resort.
5. **Modifying the grid in-place when the problem needs the original.** If the problem requires the grid to be unchanged, use a separate visited set instead of overwriting grid cells.

#### 8) Worked Examples (Full Python)
##### Example A: 200. Number of Islands
```python
class Solution:
    def numIslands(self, grid: list[list[str]]) -> int:
        if not grid:
            return 0
        rows, cols = len(grid), len(grid[0])
        count = 0

        def dfs(r: int, c: int) -> None:
            if r < 0 or c < 0 or r >= rows or c >= cols or grid[r][c] != '1':
                return
            grid[r][c] = '0'
            dfs(r + 1, c)
            dfs(r - 1, c)
            dfs(r, c + 1)
            dfs(r, c - 1)

        for r in range(rows):
            for c in range(cols):
                if grid[r][c] == '1':
                    count += 1
                    dfs(r, c)

        return count
```

**Line-by-line explanation:**

- `if not grid:` — Edge case: if the grid is empty (no rows), return 0. Always handle empty input in graph/grid problems.
- `rows, cols = len(grid), len(grid[0])` — Store grid dimensions for boundary checking. You will reference these in the DFS to ensure you do not go out of bounds. This pattern is universal for grid problems.
- `count = 0` — Counter for the number of islands (connected components of '1's).
- `def dfs(r: int, c: int) -> None:` — Recursive DFS function. Parameters are row and column indices — the "current node" in the implicit grid graph.
- `if r < 0 or c < 0 or r >= rows or c >= cols or grid[r][c] != '1':` — Combined boundary check and validity check. If out of bounds or not a land cell, stop. This is the standard grid DFS guard clause — memorize this pattern. Checking bounds first prevents index errors; checking the cell value prevents revisiting water or already-visited cells.
- `grid[r][c] = '0'` — Mark the cell as visited by changing it to '0' (water). This is an in-place visited mechanism — no extra space needed. This prevents infinite loops and double-counting. The cell is permanently modified, which is fine because we only need to count components.
- `dfs(r + 1, c)` — Recurse downward (next row, same column). Explores the south neighbor.
- `dfs(r - 1, c)` — Recurse upward. Explores the north neighbor.
- `dfs(r, c + 1)` — Recurse rightward. Explores the east neighbor.
- `dfs(r, c - 1)` — Recurse leftward. Explores the west neighbor. These four calls together explore all 4-directional neighbors, which is the standard for grid problems (8-directional is used when diagonals count).
- `for r in range(rows):` — Outer loop over all rows. Combined with the inner loop, this visits every cell in the grid.
- `for c in range(cols):` — Inner loop over all columns.
- `if grid[r][c] == '1':` — If this cell is unvisited land, it is the start of a new island.
- `count += 1` — Increment the island count. Each time we find an unvisited '1', we have discovered a new connected component.
- `dfs(r, c)` — Flood-fill (DFS) from this cell, marking all connected land cells as visited. After this call, the entire island is marked as '0'.
- `return count` — Return the total number of islands found.

**Complexity:** O(mn) time where m and n are grid dimensions — each cell is visited at most once. O(mn) space in the worst case for the recursion stack (a grid that is entirely land forms a single-path DFS). For grids larger than ~1000x1000, consider iterative BFS to avoid stack overflow.

##### Example B: 133. Clone Graph
```python
from collections import deque

class Solution:
    def cloneGraph(self, node):
        if not node:
            return None
        clones = {node: Node(node.val)}
        q = deque([node])

        while q:
            cur = q.popleft()
            for nei in cur.neighbors:
                if nei not in clones:
                    clones[nei] = Node(nei.val)
                    q.append(nei)
                clones[cur].neighbors.append(clones[nei])

        return clones[node]
```

**Line-by-line explanation:**

- `from collections import deque` — Imports deque for O(1) popleft BFS operations. Using a list with `pop(0)` would be O(n) per dequeue.
- `if not node:` — Edge case: if the input is None (empty graph), return None. Always handle null input.
- `clones = {node: Node(node.val)}` — Creates a dictionary mapping original nodes to their clones. This serves double duty: it is both the visited set (if a node is in `clones`, it has been visited) and the clone registry (maps old nodes to new nodes). Initializes with the starting node already cloned. This dual-purpose dictionary is a common pattern in graph cloning problems.
- `q = deque([node])` — Initialize the BFS queue with the starting node. We will BFS through the original graph, cloning as we go.
- `while q:` — Standard BFS loop: continue until all reachable nodes have been processed.
- `cur = q.popleft()` — Dequeue the next node to process. BFS processes nodes in the order they were discovered (FIFO).
- `for nei in cur.neighbors:` — Iterate over all neighbors of the current original node. This is the "explore edges" step of BFS.
- `if nei not in clones:` — If this neighbor has not been cloned yet (i.e., not visited), we need to create its clone and add it to the queue. This check also serves as the visited check, preventing infinite loops in cyclic graphs.
- `clones[nei] = Node(nei.val)` — Create the clone of the neighbor. We copy the value but not the neighbor list — neighbor connections are established separately.
- `q.append(nei)` — Add the original neighbor to the queue so we can process its neighbors later. Note: we add to the queue immediately after cloning (i.e., when we first discover it), which is the correct BFS pattern.
- `clones[cur].neighbors.append(clones[nei])` — Connect the cloned current node to the cloned neighbor. This line runs for every neighbor, whether newly discovered or previously cloned. This is how we replicate the edge structure in the cloned graph.
- `return clones[node]` — Return the clone of the starting node, which is the entry point to the fully cloned graph.

**Complexity:** O(V + E) time — each node is dequeued once (V operations), each edge is traversed once (E operations). O(V) space for the clones dictionary and BFS queue. This is optimal because you must visit every node and edge at least once to clone the graph.

#### 9) Additional Practice
- 994. Rotting Oranges
- 695. Max Area of Island
- 417. Pacific Atlantic Water Flow
- 207. Course Schedule

---

### 1-D DP
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics:** 1-Dimension DP, Palindromes.
- **Connected structures:** DP arrays (store solutions to subproblems indexed by a single parameter), rolling variables (when only the last 1-2 states are needed, replace the array with variables to achieve O(1) space), hash maps (for DP with non-contiguous or negative indices).
- **Dynamic Programming (DP):** A technique for solving problems with overlapping subproblems and optimal substructure by storing solutions to subproblems and building up to the final answer. Avoids redundant computation by trading space for time.
- **Optimal Substructure:** The optimal solution to the problem contains optimal solutions to its subproblems. This property is what makes DP correct.
- **Overlapping Subproblems:** The same subproblem is solved multiple times in a naive recursive approach. DP solves each subproblem once and caches the result.
- **State Transition (Recurrence):** The formula that defines how to compute `dp[i]` from previously computed values. This is the core of any DP solution.

#### 2) Subtopic Deep Dives

**1-Dimension DP**
- **Definition:** DP where the state is defined by a single index — typically `dp[i]` represents the answer for the first i elements, or the answer ending at index i, or the answer using amount i.
- **When you encounter it:** Problems where you make sequential decisions along a linear structure (array, string, number line) and each decision depends on earlier decisions. Keywords: "minimum cost," "number of ways," "maximum profit," with overlapping choices.
- **Core pattern:** Define `dp[i]`, write the recurrence `dp[i] = f(dp[i-1], dp[i-2], ...)`, set base cases, fill left to right.
- **Key insight:** The hardest part is defining what `dp[i]` means. Once you nail the definition, the recurrence usually writes itself. Ask: "If I knew the answer for all smaller subproblems, how would I compute the answer for size i?"

**Palindromes**
- **Definition:** A string that reads the same forward and backward. Palindrome DP problems ask you to find the longest palindromic substring, count palindromic substrings, or compute the minimum cuts to partition into palindromes.
- **When you encounter it:** Any problem mentioning "palindrome" with strings longer than ~20 characters (where brute force is too slow).
- **Core pattern:** For longest palindromic substring, expand from center: try each index (and each pair of adjacent indices) as the center, expand outward while characters match. This is O(n^2) time, O(1) space. Alternatively, use DP: `dp[i][j] = True` if `s[i:j+1]` is a palindrome.
- **Key insight:** Expanding from center is usually simpler and more space-efficient than 2D DP for palindromic substring problems. The key observation is that every palindrome has a center (single character for odd length, pair for even length), and you can find the longest one by trying all possible centers.

#### 3) Key Insight / Mental Model
1-D DP is about standing at position i and asking: "What is the best I can do here, given that I already know the best answers for all positions before me?" You are building a chain of decisions where each link depends on previous links. The mental model: imagine filling in a row of boxes from left to right, where each box's value is computed from the boxes to its left. Once all boxes are filled, the answer is in the last box (or the maximum across all boxes). The key leap is recognizing that a problem that looks like it requires exploring all possibilities can be decomposed into a sequence of local decisions that build on cached subresults.

#### 4) Fast Recognition Cues
- The problem asks for "minimum cost," "maximum profit," "number of ways," or "is it possible."
- A greedy/local approach fails because future decisions affect the value of current decisions.
- The input is a linear structure (array, string, number) and you process it sequentially.
- You can phrase the problem as "the answer for n depends on the answer for n-1, n-2, etc."
- The problem has a recursive solution with repeated subproblems (e.g., Fibonacci-like recursion).
- Keywords like "climbing," "robbing," "jumping," "partitioning" along a sequence.
- The naive recursive solution has exponential time but the number of unique subproblems is polynomial.
- You see constraints like n <= 10^4 or n <= 10^5 (suggesting O(n) or O(n^2) DP).

#### 5) When NOT to Use This Pattern
- **A greedy approach is provably correct:** If making the locally optimal choice always leads to the global optimum (e.g., activity selection, fractional knapsack), DP adds unnecessary complexity. Verify by checking if greedy fails on any counterexample.
- **The problem requires 2D state:** If the answer depends on two independent parameters (e.g., "using first i items with capacity j"), you need 2-D DP, not 1-D. However, sometimes 2-D problems can be compressed to 1-D by processing one row at a time.
- **There are no overlapping subproblems:** If each subproblem is solved only once in the recursion tree (e.g., merge sort), DP gives no speedup. You just need divide and conquer.
- **The problem is asking for all solutions, not just the count or optimum:** DP counts or optimizes. If you need to enumerate all solutions, use backtracking.
- **Input size is very small (n < 15):** Bitmask DP or brute force may be simpler and fast enough.

#### 6) Universal Solve Framework
1. **Define `dp[i]` precisely.** Write it in plain English. Example: "`dp[i]` = the maximum money achievable considering houses 0 through i." Ambiguity in the definition leads to wrong recurrences. Common definitions: "answer for first i elements," "answer ending at index i," "answer using exactly amount i."
2. **Write the transition (recurrence) from smaller states.** For each state i, identify all possible last actions and express dp[i] in terms of earlier states. Example for House Robber: "At house i, I either rob it (getting `nums[i] + dp[i-2]`) or skip it (getting `dp[i-1]`). So `dp[i] = max(nums[i] + dp[i-2], dp[i-1])`."
3. **Set base cases correctly.** These are the smallest subproblems you can solve directly, without the recurrence. Typically `dp[0]` and possibly `dp[1]`. Getting base cases wrong cascades errors through the entire DP table.
4. **Determine the fill order.** Fill the DP table in an order such that when you compute `dp[i]`, all states it depends on are already computed. For 1-D DP, this is almost always left to right.
5. **Optimize space if only recent states are needed.** If `dp[i]` depends only on `dp[i-1]` and `dp[i-2]`, you do not need an array — two variables suffice. This reduces space from O(n) to O(1).
6. **Return the correct final answer.** Sometimes it is `dp[n]`, sometimes `dp[n-1]`, sometimes `max(dp)`. This depends on your definition of dp[i].

#### 7) Common Mistakes & Pitfalls
1. **Vague or incorrect dp[i] definition.** If you are not crystal clear on what dp[i] represents, your recurrence will be wrong. Write it down explicitly before coding.
2. **Wrong base cases.** Off-by-one errors in base cases are the most common DP bug. Test your base cases manually: does dp[0] give the right answer for an input of size 0 or 1?
3. **Forgetting to handle the "skip" option.** In problems like House Robber, the transition is `dp[i] = max(take, skip)`. Forgetting the skip option (or the take option) gives wrong answers.
4. **Not recognizing when space can be optimized.** If `dp[i]` only depends on `dp[i-1]` and `dp[i-2]`, using a full array wastes O(n) space. Interviewers expect the O(1) space optimization for Fibonacci-type problems.
5. **Returning dp[n] vs dp[n-1].** Whether the answer is at index n or n-1 depends on whether your DP is 0-indexed or 1-indexed and how you defined the state. Always trace through a small example to verify.

#### 8) Worked Examples (Full Python)
##### Example A: 70. Climbing Stairs
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n <= 2:
            return n
        a, b = 1, 2
        for _ in range(3, n + 1):
            a, b = b, a + b
        return b
```

**Line-by-line explanation:**

- `if n <= 2:` — Base cases: if there are 1 or 2 stairs, the answer is 1 or 2 respectively (1 stair: one way [1 step]; 2 stairs: two ways [1+1 or 2]). Handling these upfront avoids issues with the loop below.
- `return n` — For n=1 return 1, for n=2 return 2. These are the base cases of the Fibonacci-like recurrence.
- `a, b = 1, 2` — Initialize rolling variables. `a` represents `dp[i-2]` and `b` represents `dp[i-1]`. We start with `a = dp[1] = 1` and `b = dp[2] = 2`. Using two variables instead of an array gives O(1) space — this is the space optimization step. This pattern applies whenever the recurrence only looks back a fixed number of steps.
- `for _ in range(3, n + 1):` — Iterate from stair 3 to stair n. We use `_` because we do not need the loop variable — we only need to advance the rolling variables n-2 times. The range starts at 3 because stairs 1 and 2 are already handled.
- `a, b = b, a + b` — The state transition. `dp[i] = dp[i-1] + dp[i-2]` because to reach stair i, you either took 1 step from stair i-1 or 2 steps from stair i-2. The number of ways to reach stair i is the sum of ways to reach those two predecessor stairs. Python's simultaneous assignment ensures we use the old values of both a and b before updating. After this line, `a` holds what was `b` (the new dp[i-2] for the next iteration) and `b` holds `a + b` (the new dp[i-1]).
- `return b` — After the loop, `b` holds `dp[n]`, the number of ways to climb n stairs.

**Complexity:** O(n) time because we iterate once from 3 to n. O(1) space because we use only two variables regardless of n. This is optimal — you must consider at least n states, and you cannot compute dp[n] without knowing dp[n-1] and dp[n-2], so O(n) time is a lower bound.

##### Example B: 198. House Robber
```python
class Solution:
    def rob(self, nums: list[int]) -> int:
        rob_prev = 0
        skip_prev = 0
        for x in nums:
            new_rob = skip_prev + x
            new_skip = max(skip_prev, rob_prev)
            rob_prev, skip_prev = new_rob, new_skip
        return max(rob_prev, skip_prev)
```

**Line-by-line explanation:**

- `rob_prev = 0` — Maximum money if the previous house was robbed. Starts at 0 because before processing any house, no money has been collected by robbing. This is one of two rolling variables that replace a full DP array.
- `skip_prev = 0` — Maximum money if the previous house was skipped. Also starts at 0. Together, `rob_prev` and `skip_prev` encode the complete state after processing each house.
- `for x in nums:` — Process each house in order. `x` is the value of the current house. This left-to-right scan mirrors filling a DP table from index 0 to n-1.
- `new_rob = skip_prev + x` — If we rob the current house, we gain its value `x`, but we must have skipped the previous house (to avoid robbing two adjacent houses). So the total is `skip_prev + x`. This is the core constraint of the problem: no two adjacent houses can be robbed.
- `new_skip = max(skip_prev, rob_prev)` — If we skip the current house, our money is the better of the two previous outcomes: either we robbed the previous house or skipped it. We take the max because we want the optimal strategy.
- `rob_prev, skip_prev = new_rob, new_skip` — Advance the rolling variables. The "current" states become the "previous" states for the next iteration. This simultaneous assignment prevents the new values from corrupting the old values mid-update.
- `return max(rob_prev, skip_prev)` — After processing all houses, the answer is the better of robbing or skipping the last house. We take the max because the optimal strategy might end with either action.

**Complexity:** O(n) time — one pass through the array. O(1) space — only four variables regardless of input size. This is optimal because you must examine every house at least once (O(n) lower bound), and the space optimization from a full DP array to rolling variables is the standard technique for recurrences with constant lookback.

##### Example C: 5. Longest Palindromic Substring
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        res = ""

        def expand(l: int, r: int) -> None:
            nonlocal res
            while l >= 0 and r < len(s) and s[l] == s[r]:
                l -= 1
                r += 1
            candidate = s[l + 1:r]
            if len(candidate) > len(res):
                res = candidate

        for i in range(len(s)):
            expand(i, i)
            expand(i, i + 1)

        return res
```

**Line-by-line explanation:**

- `res = ""` — Tracks the longest palindromic substring found so far. Initialized to empty string. Updated whenever we find a longer palindrome.
- `def expand(l: int, r: int) -> None:` — Helper function that expands outward from a center defined by indices l and r. This is the "expand from center" technique, which is the most intuitive approach for palindromic substrings.
- `nonlocal res` — Allows the nested function to modify `res` in the enclosing scope. Without this, assigning to `res` inside `expand` would create a local variable.
- `while l >= 0 and r < len(s) and s[l] == s[r]:` — Expand outward as long as: (1) left index is in bounds, (2) right index is in bounds, and (3) the characters at both ends match. When any condition fails, we have found the boundary of the palindrome. The palindrome is `s[l+1:r]` because l and r have moved one step past the matching region.
- `l -= 1` — Move left pointer outward (leftward).
- `r += 1` — Move right pointer outward (rightward). Together, these extend the window symmetrically.
- `candidate = s[l + 1:r]` — Extract the palindrome. We use `l + 1` because `l` was decremented one step past the last matching character. Similarly, Python slicing `s[a:b]` excludes index b, and `r` is already one past the last match.
- `if len(candidate) > len(res):` — Update result if this palindrome is longer than the current best.
- `res = candidate` — Store the new longest palindrome.
- `for i in range(len(s)):` — Try every index as a potential palindrome center.
- `expand(i, i)` — Expand from a single character center (odd-length palindromes like "aba"). Every single character is a palindrome of length 1.
- `expand(i, i + 1)` — Expand from a pair of adjacent characters (even-length palindromes like "abba"). This only produces a palindrome if `s[i] == s[i+1]`.
- `return res` — Return the longest palindromic substring found.

**Complexity:** O(n^2) time — n centers, each expansion takes up to O(n) in the worst case. O(1) space (excluding the output string) because we only use pointers and a single result variable. This is practical for interview purposes. Manacher's algorithm achieves O(n) but is rarely expected in interviews.

#### 9) Additional Practice
- 746. Min Cost Climbing Stairs
- 322. Coin Change
- 5. Longest Palindromic Substring
- 300. Longest Increasing Subsequence



### Intervals
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics**: Interval processing (merging, splitting, intersection, scheduling).
- **Connected structures**:
  - **Sorted arrays**: Intervals are almost always sorted by start (or end) time as a first step, turning an unordered collection into a scannable sequence.
  - **Sweep events (line sweep)**: A technique where you decompose each interval into a "start" event and an "end" event, sort all events, then sweep left-to-right to track how many intervals are active at any point.
  - **Min-heaps (priority queues)**: Used when you need to track the earliest-ending active interval (e.g., meeting room scheduling) so you can efficiently decide whether a new interval conflicts or can reuse a resource.

#### 2) Subtopic Deep Dives

**Interval Merging**
- **Definition**: Combining overlapping or touching intervals into a single contiguous interval.
- **When you encounter it**: "Given a list of intervals, return a list where all overlapping intervals have been merged."
- **Core implementation pattern**: Sort by start time, then iterate. If the current interval's start is within the previous interval's range, extend the previous interval's end. Otherwise, start a new merged interval.
- **Key insight**: After sorting by start, overlaps can only happen with the most recent merged interval — you never need to look further back.

**Interval Intersection**
- **Definition**: Finding the overlapping portions between two sets of intervals.
- **When you encounter it**: "Given two lists of intervals, find all regions where both have coverage."
- **Core implementation pattern**: Use two pointers, one per list. At each step, the intersection (if any) is `[max(a_start, b_start), min(a_end, b_end)]`. Advance the pointer whose interval ends first.
- **Key insight**: The interval that ends first can never intersect with anything beyond the other pointer's current interval.

**Interval Scheduling / Greedy Selection**
- **Definition**: Selecting the maximum number of non-overlapping intervals, or finding the minimum number to remove to eliminate all overlaps.
- **When you encounter it**: "What is the maximum number of meetings one person can attend?" or "Remove the minimum number of intervals so none overlap."
- **Core implementation pattern**: Sort by end time. Greedily pick the interval that ends earliest and skip all intervals that conflict with it.
- **Key insight**: Choosing the earliest-ending interval always leaves the most room for future intervals — this is the classic "activity selection" proof.

**Sweep Line / Event-Based Counting**
- **Definition**: Converting intervals into discrete events (+1 at start, -1 at end) and scanning in order to answer questions about concurrent overlap counts.
- **When you encounter it**: "How many meeting rooms are needed?" or "What is the maximum number of overlapping intervals at any point?"
- **Core implementation pattern**: Create events `(time, +1)` for starts and `(time, -1)` for ends. Sort events (break ties with ends before starts if intervals are closed). Scan and maintain a running count.
- **Key insight**: You reduce a 2D problem (ranges on a timeline) to a 1D scan of sorted points.

#### 3) Key Insight / Mental Model
**Think of intervals as segments on a number line.** Sorting them lines them up left-to-right, and then every interval problem becomes a single left-to-right scan where you maintain some small state about the "current situation" — the last merged interval, the earliest ending active interval, or a running overlap count. The core aha: once sorted, you only ever need to compare the current interval against the most recent state, never against all previous intervals.

#### 4) Fast Recognition Cues
- Input contains many `[start, end]` pairs or ranges.
- Problem asks to merge, insert, intersect, or count overlapping intervals.
- Scheduling language: "meetings," "rooms," "conflicts," "booking."
- Need to find the maximum number of non-overlapping intervals (activity selection).
- Need to find minimum removals to eliminate overlaps.
- "At any point in time, how many X are active?"
- A problem about ranges on a timeline or coordinate axis.
- The phrase "overlapping" or "intersecting" appears in the problem statement.

#### 5) When NOT to Use This Pattern
- **Intervals with dependencies or ordering constraints**: If intervals must be processed in a specific non-time order (e.g., a DAG dependency), interval sorting won't help — you likely need topological sort.
- **Point queries, not range queries**: If the problem is about individual points rather than ranges, you may need a hash map or binary search, not interval processing.
- **Dynamic interval updates**: If intervals are being added and removed in real time and you need to query overlap counts dynamically, a static sweep line won't work — you need a segment tree or interval tree.
- **When intervals encode a graph**: Sometimes intervals represent edges or relationships; the problem may actually be a graph problem in disguise.

#### 6) Universal Solve Framework
1. **Sort the intervals.** By start time for merge/insert problems. By end time for greedy selection (max non-overlapping / min removals). This is almost always the first step.
2. **Choose your tracking state:**
   - *Merging*: Track the last merged interval's end.
   - *Scheduling (room count)*: Use a min-heap of end times to track the earliest available resource.
   - *Greedy selection*: Track the end time of the last selected interval.
   - *Intersection*: Use two pointers, one per sorted list.
3. **Single-pass scan.** Iterate through sorted intervals, updating your state with each new interval. The decision at each step is always local: does this interval overlap with my current state?
4. **Return accumulated result** — merged list, count, or boolean.

#### 7) Common Mistakes & Pitfalls
1. **Forgetting to sort**: The entire pattern depends on sorted order. Skipping this step leads to incorrect merges or missed overlaps.
2. **Sorting by wrong key**: Merge problems need sort-by-start; greedy selection (min removals) needs sort-by-end. Mixing these up gives wrong answers.
3. **Off-by-one on touching intervals**: Is `[1,3]` and `[3,5]` overlapping or not? The problem statement defines this. For merge problems, touching intervals (`end == start`) usually merge. For scheduling, they usually don't conflict. Read carefully.
4. **Mutating input during iteration**: When merging, build a new list rather than trying to modify the input list in place, which leads to index bugs.
5. **Using the wrong end-time update**: When merging, you must take `max(current_end, new_end)` — not just replace with the new end. An interval entirely contained within another can have a smaller end.

#### 8) Worked Examples (Full Python)

##### Example A: 56. Merge Intervals
```python
class Solution:
    def merge(self, intervals: list[list[int]]) -> list[list[int]]:
        intervals.sort(key=lambda x: x[0])
        merged = []
        for s, e in intervals:
            if not merged or merged[-1][1] < s:
                merged.append([s, e])
            else:
                merged[-1][1] = max(merged[-1][1], e)
        return merged
```

**Line-by-line explanation:**

- `intervals.sort(key=lambda x: x[0])` — Sorts all intervals by their start time. This is essential because it guarantees that once we pass an interval, no future interval can start before it. After sorting, overlapping intervals are always adjacent, so a single scan suffices. This generalizes to nearly every interval problem.

- `merged = []` — Initializes the result list that will hold merged intervals. We build a new list rather than modifying in place to avoid index corruption. This is the "accumulator" pattern common in merge-style problems.

- `for s, e in intervals:` — Iterates through each interval's start and end. Because we sorted, `s` values are non-decreasing. This single pass is what makes the algorithm O(n) after sorting.

- `if not merged or merged[-1][1] < s:` — Two checks: (1) if `merged` is empty, we must add the first interval; (2) if the last merged interval's end is strictly less than the current start, there is no overlap, so this is a new disjoint interval. This is the "gap detection" step.

- `merged.append([s, e])` — Adds the current interval as a new, separate merged interval. This happens when no overlap exists with the previous merged interval.

- `else:` — We reach here when the current interval overlaps with the last merged interval (i.e., `merged[-1][1] >= s`).

- `merged[-1][1] = max(merged[-1][1], e)` — Extends the last merged interval's end to cover the current interval. We use `max` because the current interval might end before the last merged interval (it could be entirely contained). This is a critical detail — simply assigning `e` would be wrong for contained intervals.

- `return merged` — Returns the final list of non-overlapping, merged intervals.

**Complexity**: O(n log n) time due to sorting; the scan is O(n). O(n) space for the output list.

##### Example B: 435. Non-overlapping Intervals
```python
class Solution:
    def eraseOverlapIntervals(self, intervals: list[list[int]]) -> int:
        intervals.sort(key=lambda x: x[1])
        end = float('-inf')
        kept = 0
        for s, e in intervals:
            if s >= end:
                kept += 1
                end = e
        return len(intervals) - kept
```

**Line-by-line explanation:**

- `intervals.sort(key=lambda x: x[1])` — Sorts by end time, not start time. This is the key to the greedy activity selection algorithm. By considering intervals that end earliest first, we leave maximum room for subsequent intervals. Sorting by start time would not yield an optimal greedy solution here.

- `end = float('-inf')` — Initializes the end of the "last kept" interval to negative infinity, meaning any interval's start will be >= this value. This avoids a special case for the first interval.

- `kept = 0` — Counter for how many intervals we keep (don't remove). We count kept rather than removed because it's simpler to reason about; we derive removals at the end.

- `for s, e in intervals:` — Scans intervals in order of increasing end time. Each interval is considered exactly once.

- `if s >= end:` — Checks whether the current interval starts at or after the last kept interval ends. If so, there is no overlap, and we can keep this interval. The `>=` (not `>`) is because two intervals `[1,2]` and `[2,3]` are considered non-overlapping (they touch but don't overlap).

- `kept += 1` — Increments the count of kept intervals.

- `end = e` — Updates the boundary to the current interval's end. Since we sorted by end time, `e` is always >= the previous `end`, so this is monotonically non-decreasing.

- `return len(intervals) - kept` — The number of removals is total intervals minus the maximum set of non-overlapping intervals we kept. This is the classic "total minus optimal" inversion.

**Complexity**: O(n log n) time for sorting; O(1) extra space (ignoring sort internals). This is optimal because any comparison-based solution needs to examine all intervals and sorting is a lower bound.

#### 9) Additional Practice
- 57. Insert Interval
- 252. Meeting Rooms
- 253. Meeting Rooms II
- 986. Interval List Intersections
- 1288. Remove Covered Intervals
- 759. Employee Free Time


### Greedy
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics**:
  - **Kadane's Algorithm**: A specific greedy/DP hybrid for finding the maximum sum contiguous subarray in O(n) time. It maintains a running sum and resets when the sum drops below zero.
- **Connected structures**:
  - **Arrays**: Most greedy problems operate on arrays or sequences, scanning linearly while maintaining minimal state.
  - **Running states**: Greedy algorithms compress complex state into one or two variables (e.g., current max reach, running sum, last used resource).
  - **Sorting by key**: Many greedy problems require sorting by a strategic key first (earliest deadline, smallest weight, etc.) before making local choices.
  - **Heaps / Priority queues**: Sometimes the "best local choice" requires efficiently finding the min or max among candidates.

#### 2) Subtopic Deep Dives

**Kadane's Algorithm**
- **Definition**: An algorithm that finds the maximum sum subarray in O(n) by maintaining a running sum. At each element, you either extend the current subarray or start fresh from the current element — whichever gives a larger sum.
- **When you encounter it**: "Find the contiguous subarray with the largest sum," or any variant (maximum product subarray, circular subarray).
- **Core implementation pattern**: `current_sum = max(nums[i], current_sum + nums[i])` at each step, tracking the global maximum across all steps.
- **Key insight**: A negative running sum can never help a future subarray — it's always better to restart. This local decision yields the global optimum.

**Exchange Argument**
- **Definition**: A proof technique for greedy algorithms. You assume an optimal solution that differs from the greedy solution, then show you can "exchange" a choice to match the greedy solution without worsening the result.
- **When you encounter it**: Whenever you need to convince yourself (or an interviewer) that a greedy approach is correct.
- **Core pattern**: "Suppose optimal solution picks X instead of our greedy pick Y. Swapping X for Y doesn't worsen the solution because..."
- **Key insight**: If you can always swap to match greedy without losing optimality, greedy is correct.

**Greedy Stays Ahead**
- **Definition**: Another proof technique where you show that after each step, the greedy solution is at least as good as any other solution. The greedy "stays ahead" at every point.
- **When you encounter it**: Activity selection, job scheduling, interval problems.
- **Core pattern**: By induction, after k steps, greedy has achieved at least as much as any alternative after k steps.
- **Key insight**: If greedy is never behind, it must be optimal at the end.

#### 3) Key Insight / Mental Model
**Greedy = "I can commit to this choice right now without ever regretting it."** The core question for any greedy problem is: can I prove that the locally best choice at each step won't prevent me from reaching the globally best answer? If yes, you can avoid the overhead of DP or backtracking. Think of greedy as DP where the optimal substructure is so strong that you never need to revisit a decision.

#### 4) Fast Recognition Cues
- The problem asks for a single optimal value (max, min, boolean reachability) over a sequence.
- A local decision rule exists that preserves global optimality — you never need to "go back."
- DP is possible but the state space is really just one or two variables.
- Problem involves scheduling, assignment, or resource allocation with a natural ordering.
- Sorting the input by some attribute immediately simplifies the problem.
- The problem asks "is it possible" (feasibility) rather than "enumerate all ways."
- Keywords like "minimum number of," "maximum number of," "can you reach," "farthest."
- You notice that the optimal solution for subproblem [0..i] can be extended to [0..i+1] without reconsidering choices made for [0..i].

#### 5) When NOT to Use This Pattern
- **When local choices can paint you into a corner**: If choosing the locally best option now could block a globally better option later, greedy fails. Example: coin change with arbitrary denominations — greedy (pick largest coin) doesn't always work.
- **When you need to count all solutions, not just the optimal one**: Greedy finds one optimal answer but can't enumerate or count alternatives.
- **When the problem has overlapping subproblems with no greedy property**: If you can construct a counterexample where greedy gives a wrong answer, you need DP or another approach.
- **When the problem requires backtracking**: If you must explore multiple branches and can't commit early, greedy won't suffice (e.g., Sudoku, N-Queens).
- **0/1 Knapsack**: Greedy (by value-to-weight ratio) doesn't work for 0/1 knapsack; you need DP. (Fractional knapsack, however, is greedy.)

#### 6) Universal Solve Framework
1. **Propose a local choice rule.** What single criterion do you use to make each decision? Examples: "take the interval that ends earliest," "extend the farthest reachable position," "keep running sum if positive, reset if negative."
2. **Justify correctness.** Use an exchange argument or "greedy stays ahead" reasoning. Try to construct a counterexample — if you can't, the greedy is likely correct.
3. **Determine if sorting is needed.** Many greedy problems require sorting by a key (end time, deadline, size) to make the local rule work.
4. **Track minimal state.** Greedy algorithms typically maintain only 1-3 variables. Identify exactly what you need to track (e.g., farthest reach, current sum, last end time).
5. **Single pass.** Iterate through the input once, applying the local rule and updating state.
6. **Return accumulated result.**

#### 7) Common Mistakes & Pitfalls
1. **Assuming greedy works without proof**: The most dangerous mistake. Always verify with a counterexample or argument. Many problems look greedy but are actually DP (e.g., coin change with arbitrary denominations).
2. **Sorting by the wrong key**: For interval scheduling, sorting by start time instead of end time gives incorrect results. The sorting key is critical and problem-specific.
3. **Forgetting edge cases with empty input or single element**: Greedy loops often assume at least one element exists. Handle empty arrays explicitly.
4. **Confusing Kadane's reset condition**: In Kadane's, you restart when `current_sum + nums[i] < nums[i]`, i.e., when the running sum is negative. A common bug is resetting to 0 instead of to `nums[i]`, which fails for all-negative arrays.
5. **Not recognizing when greedy gives a correct answer but not the only answer**: Greedy may produce one valid optimal solution, but if the problem asks for a specific one (lexicographically smallest, etc.), you may need to modify the greedy rule.

#### 8) Worked Examples (Full Python)

##### Example A: 55. Jump Game
```python
class Solution:
    def canJump(self, nums: list[int]) -> bool:
        farthest = 0
        for i, jump in enumerate(nums):
            if i > farthest:
                return False
            farthest = max(farthest, i + jump)
        return True
```

**Line-by-line explanation:**

- `farthest = 0` — Initializes the farthest reachable index to 0 (the starting position). This single variable is the entire state of the greedy algorithm. It represents the frontier of positions we know we can reach.

- `for i, jump in enumerate(nums):` — Iterates through each position `i` with its jump value. `enumerate` gives both the index and the value, which we need to compute how far we can jump from this position.

- `if i > farthest:` — If the current index is beyond the farthest reachable position, we've hit a gap we cannot cross. This means some earlier segment had all zeros (or too-small values) and we're stranded. This is the greedy "failure" check.

- `return False` — We cannot reach the end because we're stuck at a position we couldn't reach in the first place.

- `farthest = max(farthest, i + jump)` — Updates the frontier. From position `i`, we can jump to `i + jump`. If this extends our frontier, we update. The `max` is essential because a previous position might have given us a farther reach than the current one.

- `return True` — If we scan through all positions without getting stuck, we can reach the end. Note: we don't even need to check `farthest >= len(nums) - 1` explicitly because completing the loop means we visited every index up to the last one.

**Complexity**: O(n) time — single pass. O(1) space — one variable. This is optimal because you must examine each position at least once to determine reachability.

##### Example B: 53. Maximum Subarray (Kadane's Algorithm)
```python
class Solution:
    def maxSubArray(self, nums: list[int]) -> int:
        current_sum = nums[0]
        max_sum = nums[0]
        for i in range(1, len(nums)):
            current_sum = max(nums[i], current_sum + nums[i])
            max_sum = max(max_sum, current_sum)
        return max_sum
```

**Line-by-line explanation:**

- `current_sum = nums[0]` — Initializes the running subarray sum with the first element. We start at index 0 rather than using 0 as initial value because the array could be all negative — starting with 0 would incorrectly return 0 as the max subarray sum.

- `max_sum = nums[0]` — Tracks the best subarray sum seen so far. Initialized to the first element for the same reason: the answer could be a single negative number.

- `for i in range(1, len(nums)):` — Starts from index 1 since index 0 is already accounted for in initialization. We consider each element as a potential extension or start of a new subarray.

- `current_sum = max(nums[i], current_sum + nums[i])` — The core of Kadane's algorithm. We decide: is it better to extend the existing subarray by adding `nums[i]`, or to start a brand new subarray beginning at `nums[i]`? If `current_sum` is negative, extending would make `nums[i]` smaller, so we start fresh. This is equivalent to: "if `current_sum < 0`, reset to `nums[i]`."

- `max_sum = max(max_sum, current_sum)` — After each decision, check if the current subarray sum is the best we've ever seen. The global answer is the maximum across all positions.

- `return max_sum` — Returns the maximum contiguous subarray sum.

**Complexity**: O(n) time — one pass through the array. O(1) space — two variables. This is optimal because any algorithm must inspect every element (a single unseen element could be the entire answer).

#### 9) Additional Practice
- 134. Gas Station
- 452. Minimum Number of Arrows to Burst Balloons
- 763. Partition Labels
- 45. Jump Game II
- 846. Hand of Straights
- 1899. Merge Triplets to Form Target Triplet


### 2-D DP
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics**:
  - **2-Dimension DP**: Dynamic programming where the state is defined by two parameters (e.g., `dp[i][j]`), forming a 2D table. Each cell represents the answer to a subproblem defined by those two parameters.
  - **0/1 Knapsack**: A problem pattern where you have items with weights and values, and for each item you decide to either take it (1) or leave it (0). State: `dp[i][w]` = best value using first `i` items with capacity `w`.
  - **Unbounded Knapsack**: Like 0/1 knapsack but each item can be used unlimited times. Classic example: Coin Change II (count ways to make amount using coins).
  - **LCS (Longest Common Subsequence)**: Finding the longest sequence of characters that appears in both strings (not necessarily contiguous). State: `dp[i][j]` = LCS length of `text1[0..i]` and `text2[0..j]`.
- **Connected structures**:
  - **2D tables**: The standard representation, where rows and columns correspond to the two state dimensions.
  - **Rolling rows**: Space optimization where you only keep the current and previous rows (or even just one row), reducing O(mn) space to O(min(m,n)).
  - **Memoized recursion (top-down)**: An alternative to bottom-up tabulation; uses `@lru_cache` or a dictionary to cache results of recursive subproblems.

#### 2) Subtopic Deep Dives

**0/1 Knapsack**
- **Definition**: Given `n` items each with a weight and value, and a knapsack of capacity `W`, find the maximum value you can carry. Each item is either fully taken or not taken.
- **When you encounter it**: "Given items with costs and benefits, pick a subset within a budget to maximize benefit." Also: subset sum, partition equal subset sum, target sum.
- **Core implementation pattern**: `dp[i][w] = max(dp[i-1][w], dp[i-1][w - weight[i]] + value[i])`. First term = skip item `i`; second term = take item `i` (if it fits).
- **Key insight**: The "take or skip" binary choice at each item, combined with a capacity constraint, creates the 2D state space. You can often reduce to 1D by iterating capacity in reverse.

**Unbounded Knapsack**
- **Definition**: Same as 0/1 knapsack but items can be reused any number of times.
- **When you encounter it**: Coin change (number of ways), rod cutting, ribbon cutting.
- **Core implementation pattern**: `dp[i][w] = dp[i-1][w] + dp[i][w - weight[i]]`. Note the second term uses `dp[i]` (same row), not `dp[i-1]`, because we can take item `i` again.
- **Key insight**: The difference from 0/1 knapsack is one index: `dp[i]` vs `dp[i-1]` in the "take" transition. In 1D, iterate capacity forward (not reverse).

**Longest Common Subsequence (LCS)**
- **Definition**: The longest sequence of characters present in both strings in order, but not necessarily contiguously.
- **When you encounter it**: String comparison, diff algorithms, edit distance (which extends LCS with insertions/deletions/substitutions).
- **Core implementation pattern**: If `text1[i] == text2[j]`, then `dp[i][j] = 1 + dp[i+1][j+1]`. Otherwise, `dp[i][j] = max(dp[i+1][j], dp[i][j+1])`.
- **Key insight**: When characters match, both strings "advance" together. When they don't, you try advancing each string independently and take the better result.

**Grid DP (Unique Paths / Min Path Sum)**
- **Definition**: DP on a 2D grid where movement is restricted (typically right and down only). State is the grid cell itself.
- **When you encounter it**: "How many ways to reach bottom-right?" or "Find minimum cost path in a grid."
- **Core implementation pattern**: `dp[i][j] = dp[i-1][j] + dp[i][j-1]` (paths) or `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])` (min cost).
- **Key insight**: Each cell depends only on its top and left neighbors, so a single row of DP state suffices.

#### 3) Key Insight / Mental Model
**2D DP is "two nested choices producing a table."** Every cell `dp[i][j]` answers: "What's the optimal answer if I've considered the first `i` units of dimension 1 and the first `j` units of dimension 2?" The two dimensions might be two string indices, an item index and a capacity, or row and column in a grid. The mental model: imagine filling in a spreadsheet cell by cell, where each cell's formula references only cells you've already computed (above, to the left, or diagonally).

#### 4) Fast Recognition Cues
- State depends on two indices, dimensions, or parameters (i and j, index and capacity, row and col).
- Problem involves two strings and asks for their relationship (LCS, edit distance, interleaving).
- Problem involves items with a "take or skip" choice under a capacity/budget constraint.
- Grid traversal with restricted movement (right/down only).
- You can express the answer as: "best/count for subproblem defined by (X, Y)" where X and Y are independent dimensions.
- The problem has "optimal substructure" — the answer for (i, j) can be built from answers for smaller (i, j) values.
- DP recurrence references `dp[i-1][j]`, `dp[i][j-1]`, or `dp[i-1][j-1]`.

#### 5) When NOT to Use This Pattern
- **State depends on more than two dimensions and can't be reduced**: If you need `dp[i][j][k]` and can't eliminate a dimension, you're in 3D DP territory (different pattern, different complexity).
- **The "two dimensions" are actually a graph**: If transitions aren't just up/left/diagonal but can go to arbitrary states, you need graph algorithms (BFS, Dijkstra), not table DP.
- **Greedy works**: If you can prove a greedy choice property, you can avoid the O(mn) table entirely. Always check if greedy applies first.
- **The dimensions are too large**: If `m` and `n` are both > 10^4, an O(mn) table may be too slow or too large. Look for mathematical shortcuts or different state representations.
- **The problem asks for the actual subsequence/path, not just its length**: You can still use 2D DP, but you'll need to add backtracking through the table, which is an important additional step.

#### 6) Universal Solve Framework
1. **Define `dp[i][j]` precisely.** Write a one-sentence English definition. Examples: "dp[i][j] = LCS length of text1[i:] and text2[j:]", "dp[i][w] = max value using items 0..i with capacity w." Ambiguity here causes bugs.
2. **Determine transitions.** For each cell, what cells does it depend on? Common patterns:
   - *Match/no-match*: `dp[i][j] = 1 + dp[i+1][j+1]` if match, else `max(dp[i+1][j], dp[i][j+1])`.
   - *Take/skip*: `dp[i][w] = max(dp[i-1][w], dp[i-1][w-wt] + val)`.
   - *Grid*: `dp[i][j] = f(dp[i-1][j], dp[i][j-1])`.
3. **Initialize base cases.** Row 0, column 0, or the last row/column depending on iteration direction. For LCS bottom-up starting from end: last row and last column are all 0.
4. **Choose iteration direction.** Bottom-up (fill table iteratively) is usually more cache-friendly and avoids recursion limits. Top-down (memoized recursion) is easier to write for complex recurrences.
5. **Optimize space if needed.** If `dp[i]` only depends on `dp[i-1]`, use two rows or a single row with careful iteration order.
6. **Extract the answer** from `dp[0][0]`, `dp[m][n]`, or wherever your definition places the final answer.

#### 7) Common Mistakes & Pitfalls
1. **Wrong iteration direction**: If you fill the table top-to-bottom but your recurrence references `dp[i+1]`, you'll read uninitialized cells. Match iteration direction to dependencies — if you need `dp[i+1]`, iterate `i` from bottom to top.
2. **Off-by-one in table dimensions**: For strings of length `m` and `n`, the table is `(m+1) x (n+1)` to accommodate the empty-string base case. Forgetting the `+1` causes index errors.
3. **Confusing 0/1 knapsack with unbounded**: In 0/1, the "take" transition uses `dp[i-1]` (previous row); in unbounded, it uses `dp[i]` (same row). In 1D space optimization, this means reverse vs. forward iteration over capacity.
4. **Not initializing base cases correctly**: For unique paths, `dp[0][j] = 1` and `dp[i][0] = 1` (one way to reach any cell in the first row/column). Forgetting these gives all zeros.
5. **Returning from wrong cell**: The answer's location depends on your definition. If `dp[i][j]` represents the subproblem for suffixes, the answer is `dp[0][0]`. If it represents prefixes, the answer is `dp[m][n]`.

#### 8) Worked Examples (Full Python)

##### Example A: 1143. Longest Common Subsequence
```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [[0] * (n + 1) for _ in range(m + 1)]

        for i in range(m - 1, -1, -1):
            for j in range(n - 1, -1, -1):
                if text1[i] == text2[j]:
                    dp[i][j] = 1 + dp[i + 1][j + 1]
                else:
                    dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])

        return dp[0][0]
```

**Line-by-line explanation:**

- `m, n = len(text1), len(text2)` — Stores the lengths of both strings. These define the dimensions of our DP table. We need them to set up the table and control loop bounds.

- `dp = [[0] * (n + 1) for _ in range(m + 1)]` — Creates a 2D table of size `(m+1) x (n+1)`, initialized to 0. The extra row and column represent the base case where one string is "empty" (index past the end). `dp[i][j]` means "LCS length of `text1[i:]` and `text2[j:]`." When either suffix is empty, LCS is 0 — which is exactly what our initialization provides.

- `for i in range(m - 1, -1, -1):` — Iterates `i` from `m-1` down to 0. We go bottom-to-top because `dp[i][j]` depends on `dp[i+1][...]`, so row `i+1` must be computed before row `i`.

- `for j in range(n - 1, -1, -1):` — Iterates `j` from `n-1` down to 0, for the same reason: `dp[i][j]` depends on `dp[i][j+1]`.

- `if text1[i] == text2[j]:` — Checks if the current characters match. This is the branch point of the LCS recurrence.

- `dp[i][j] = 1 + dp[i + 1][j + 1]` — When characters match, this character is part of the LCS. We take 1 (for this matching character) plus the LCS of the remaining suffixes `text1[i+1:]` and `text2[j+1:]`. Both indices advance because we "use" both characters.

- `else:` — Characters don't match, so at least one of them is not in the LCS.

- `dp[i][j] = max(dp[i + 1][j], dp[i][j + 1])` — We try two options: skip `text1[i]` (use `dp[i+1][j]`) or skip `text2[j]` (use `dp[i][j+1]`), and take the better result. This ensures we don't miss any possible LCS.

- `return dp[0][0]` — The answer for the full strings `text1[0:]` and `text2[0:]` is stored at `dp[0][0]`.

**Complexity**: O(mn) time — we fill every cell exactly once, each in O(1). O(mn) space — the full table. Can be optimized to O(min(m,n)) space using a rolling row since each row only depends on the row below it.

##### Example B: 62. Unique Paths
```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1] * n for _ in range(m)]

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]

        return dp[m - 1][n - 1]
```

**Line-by-line explanation:**

- `dp = [[1] * n for _ in range(m)]` — Creates an `m x n` table initialized to 1. This simultaneously handles the base cases: the first row and first column are all 1 because there's exactly one way to reach any cell in the top row (go right) or left column (go down). Initializing the entire table to 1 is a clean shortcut.

- `for i in range(1, m):` — Starts from row 1 (row 0 is the base case, already set to 1). We go top-to-bottom because `dp[i][j]` depends on `dp[i-1][j]`.

- `for j in range(1, n):` — Starts from column 1 (column 0 is the base case). We go left-to-right because `dp[i][j]` depends on `dp[i][j-1]`.

- `dp[i][j] = dp[i - 1][j] + dp[i][j - 1]` — The number of paths to cell `(i, j)` is the sum of paths from above (came from `(i-1, j)`) and from the left (came from `(i, j-1)`). These are the only two directions we can arrive from. This is the Pascal's triangle recurrence applied to a grid.

- `return dp[m - 1][n - 1]` — The bottom-right corner holds the total number of unique paths from top-left to bottom-right.

**Complexity**: O(mn) time — one pass through the grid. O(mn) space, reducible to O(n) with a single row since each row only depends on the row above.

#### 9) Additional Practice
- 72. Edit Distance
- 518. Coin Change II
- 494. Target Sum
- 97. Interleaving String
- 309. Best Time to Buy and Sell Stock with Cooldown
- 1049. Last Stone Weight II


### Bit Manipulation
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics**:
  - **Bit Operations**: The fundamental operations on individual bits within integers — AND (`&`), OR (`|`), XOR (`^`), NOT (`~`), left shift (`<<`), and right shift (`>>`). These operate in O(1) time and are the building blocks of all bit manipulation.
- **Connected structures**:
  - **Integers as bitsets**: An integer's binary representation can encode a set. Bit `k` being 1 means element `k` is in the set. Union = OR, intersection = AND, toggle = XOR, membership check = AND with mask.
  - **XOR masks**: XOR has the property `x ^ x = 0` and `x ^ 0 = x`, making it useful for finding unpaired elements, toggling states, and creating invertible transformations.
  - **Bitmask DP**: Using integers as compact set representations in DP states, e.g., `dp[mask]` where `mask` is a bitmask of visited nodes (Traveling Salesman, Hamiltonian Path).

#### 2) Subtopic Deep Dives

**Core Bit Operations and Identities**
- **Definition**: The six basic operations and their key identities that recur in problems.
- **When you encounter it**: Virtually every bit manipulation problem uses a combination of these.
- **Core identities**:
  - `x ^ x = 0` — any number XOR'd with itself is zero (cancellation).
  - `x ^ 0 = x` — XOR with zero is identity.
  - `x & (x - 1)` — clears the lowest set bit of `x`. Used to count bits or detect powers of 2.
  - `x & (-x)` — isolates the lowest set bit of `x`.
  - `x | (1 << k)` — sets bit `k`.
  - `x & ~(1 << k)` — clears bit `k`.
  - `(x >> k) & 1` — reads bit `k`.
- **Key insight**: These operations are O(1) and let you perform set operations on up to 32 or 64 elements with a single integer.

**XOR for Finding Unique Elements**
- **Definition**: Using XOR's cancellation property to find elements that appear an odd number of times.
- **When you encounter it**: "Every element appears twice except one — find the unique element." Variants include two unique elements or elements appearing three times.
- **Core implementation pattern**: XOR all elements together. Pairs cancel to 0, leaving only the unique element.
- **Key insight**: XOR is both commutative and associative, so order doesn't matter. It's essentially counting parity of each bit position across all numbers.

**Counting Set Bits (Brian Kernighan's Algorithm)**
- **Definition**: Counting the number of 1-bits in an integer by repeatedly clearing the lowest set bit.
- **When you encounter it**: "Count the number of 1 bits" (Hamming weight), "counting bits for all numbers 0 to n."
- **Core implementation pattern**: `while n: count += 1; n &= (n - 1)`. Each iteration removes exactly one set bit.
- **Key insight**: `n & (n - 1)` always clears the lowest set bit because subtracting 1 flips all bits from the lowest set bit downward.

**Bitmask as Set Representation**
- **Definition**: Encoding a subset of `n` elements as an `n`-bit integer, where bit `i` = 1 means element `i` is included.
- **When you encounter it**: Problems with `n <= 20` where you need to enumerate or DP over all subsets (Traveling Salesman, assignment problems).
- **Core implementation pattern**: Iterate over all `2^n` masks. For each mask, iterate over set bits to determine which elements are included.
- **Key insight**: This converts exponential-space set operations into O(1) bitwise operations, making bitmask DP feasible for small `n`.

#### 3) Key Insight / Mental Model
**Think of integers as arrays of boolean flags.** Every integer is already a compact array of bits. Bit manipulation is just array operations (read, write, toggle, scan) performed in O(1) instead of O(n). When you see a problem involving pairs, parity, toggling, or small sets, ask: "Can I encode this in the bits of an integer?" If yes, you get constant-time operations for free.

#### 4) Fast Recognition Cues
- The problem involves finding a unique/unpaired element among duplicates.
- Very small memory or state constraints hint at bit-level encoding.
- Parity, toggling, or on/off switches.
- The problem mentions binary representation, powers of 2, or Hamming distance.
- `n` is small enough (≤ 20-25) that `2^n` subsets are feasible — bitmask DP.
- Need to implement addition/subtraction/multiplication without arithmetic operators.
- Problem asks about properties of binary representation (number of 1-bits, highest bit, etc.).
- Keywords: "XOR," "bit," "binary," "single number," "missing number."

#### 5) When NOT to Use This Pattern
- **Large sets (n > 25-30)**: Bitmask representations become infeasible because `2^n` states explode. Use other set representations.
- **Floating-point numbers**: Bit manipulation operates on integers. If the problem involves floats or decimals, bit tricks don't apply directly.
- **When a simpler math formula exists**: For "missing number," XOR works but so does the sum formula `n*(n+1)/2 - sum(nums)`. Choose the clearest approach.
- **When the problem is about bit patterns in strings, not integers**: If "bits" are characters in a string, you need string operations, not bitwise operations.

#### 6) Universal Solve Framework
1. **Identify the bit-level property** the problem exploits. Is it cancellation (XOR), bit counting, set membership, or arithmetic?
2. **Choose the right identity:**
   - Finding unique among duplicates → XOR all elements.
   - Counting set bits → Brian Kernighan (`n & (n-1)` loop).
   - Power of 2 check → `n > 0 and n & (n-1) == 0`.
   - Subset enumeration → iterate `mask` from 0 to `2^n - 1`.
3. **Map problem entities to bit positions.** Element `k` → bit `k`. Set inclusion → bit is 1.
4. **Use masks for transitions/checks.** Build masks with shifts and combine with AND/OR/XOR.
5. **Handle edge cases:** negative numbers (two's complement), zero, integer overflow in languages with fixed-width integers (Python handles arbitrary precision).

#### 7) Common Mistakes & Pitfalls
1. **Operator precedence**: In most languages, bitwise operators (`&`, `|`, `^`) have lower precedence than comparison operators (`==`, `<`). Always use parentheses: `if (x & mask) == 0` not `if x & mask == 0`.
2. **Signed vs. unsigned confusion**: In languages like Java/C++, right shift on negative numbers can be arithmetic (sign-extending) vs. logical. Python integers are arbitrary precision, so `~x = -(x+1)`, which can surprise you.
3. **Off-by-one in bit positions**: Bit 0 is the least significant bit. Setting the k-th bit is `1 << k`, not `1 << (k-1)`.
4. **Forgetting XOR is its own inverse**: `a ^ b ^ b = a`. This is the reason XOR works for finding unique elements, but also means applying XOR twice undoes the operation — useful for encoding/decoding but a bug if done accidentally.
5. **Using bit tricks when a readable solution exists**: Bit manipulation can obscure intent. In an interview, clarity matters. Use bit tricks when they provide a genuine advantage (O(1) space, O(1) time), not just to show off.

#### 8) Worked Examples (Full Python)

##### Example A: 136. Single Number
```python
class Solution:
    def singleNumber(self, nums: list[int]) -> int:
        ans = 0
        for x in nums:
            ans ^= x
        return ans
```

**Line-by-line explanation:**

- `ans = 0` — Initializes the accumulator to 0. We use 0 because it is the identity element for XOR: `0 ^ x = x`. This means the first XOR simply sets `ans` to the first element. This pattern of starting with the identity element generalizes to any fold/reduce operation.

- `for x in nums:` — Iterates through every number in the array. Order doesn't matter because XOR is commutative and associative. Every element gets XOR'd into the accumulator exactly once.

- `ans ^= x` — XOR's the current number into the accumulator. For any number that appears twice, the two occurrences will cancel: `a ^ a = 0`. After processing all elements, only the number that appears once remains. This works because XOR is essentially independent parity counting for each bit position.

- `return ans` — Returns the single number that wasn't cancelled out.

**Complexity**: O(n) time — one pass. O(1) space — one variable. This is optimal: you must read every element, and no data structure is needed.

##### Example B: 191. Number of 1 Bits
```python
class Solution:
    def hammingWeight(self, n: int) -> int:
        count = 0
        while n:
            n &= (n - 1)
            count += 1
        return count
```

**Line-by-line explanation:**

- `count = 0` — Initializes the bit counter. We'll increment this once for each set bit.

- `while n:` — Continues as long as `n` has any set bits (is nonzero). When all bits are cleared, `n` becomes 0 and the loop exits. The number of iterations equals the number of set bits, not the total number of bits — this is the efficiency advantage of Brian Kernighan's method.

- `n &= (n - 1)` — Clears the lowest set bit of `n`. Here's why: subtracting 1 from `n` flips the lowest set bit to 0 and all lower bits to 1. AND-ing with the original `n` keeps all higher bits unchanged and zeros out the lowest set bit and below. Example: `n = 12 (1100)`, `n-1 = 11 (1011)`, `n & (n-1) = 8 (1000)`.

- `count += 1` — Each iteration removes exactly one set bit, so we count one.

- `return count` — Returns the total number of 1-bits (Hamming weight).

**Complexity**: O(k) time where `k` is the number of set bits (at most 32 for 32-bit integers). O(1) space. This is better than the naive approach of checking all 32 bits when the number has few set bits.

#### 9) Additional Practice
- 338. Counting Bits
- 268. Missing Number
- 371. Sum of Two Integers
- 190. Reverse Bits
- 201. Bitwise AND of Numbers Range
- 421. Maximum XOR of Two Numbers in an Array


### Advanced Graphs
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics**:
  - **Dijkstra's Algorithm**: Finds the shortest path from a single source to all other nodes in a graph with non-negative edge weights. Uses a min-heap to always process the node with the smallest known distance next.
  - **Prim's Algorithm**: Builds a Minimum Spanning Tree (MST) by greedily adding the cheapest edge that connects a visited node to an unvisited node. Uses a min-heap of edges.
  - **Kruskal's Algorithm**: Builds an MST by sorting all edges by weight and greedily adding the cheapest edge that doesn't form a cycle. Uses a Disjoint Set Union (DSU/Union-Find) to detect cycles.
  - **Topological Sort**: Produces a linear ordering of nodes in a Directed Acyclic Graph (DAG) such that for every edge u→v, u comes before v. Used for dependency resolution, build systems, course scheduling.
- **Connected structures**:
  - **Adjacency list**: The standard graph representation — a dictionary or array of lists mapping each node to its neighbors (with weights for weighted graphs).
  - **Min-heap (priority queue)**: Essential for Dijkstra and Prim. Provides O(log n) extraction of the minimum element.
  - **DSU (Disjoint Set Union / Union-Find)**: A data structure that tracks which elements belong to which sets, with near-O(1) union and find operations (via path compression and union by rank). Used in Kruskal's.
  - **Indegree array + queue**: For Kahn's algorithm (BFS-based topological sort). The indegree of a node is how many edges point to it. Nodes with indegree 0 have no unmet dependencies and can be processed.

#### 2) Subtopic Deep Dives

**Dijkstra's Algorithm**
- **Definition**: A greedy shortest-path algorithm for graphs with non-negative edge weights. It processes nodes in order of their distance from the source, guaranteeing that once a node is popped from the heap, its shortest distance is finalized.
- **When you encounter it**: "Find the shortest path/time/cost from source to destination (or to all nodes) in a weighted graph with non-negative weights."
- **Core implementation pattern**: Initialize `dist[source] = 0`, all others infinity. Push `(0, source)` to min-heap. Pop minimum, skip if already processed at a shorter distance, then relax all neighbors.
- **Key insight**: Non-negative weights guarantee that once you pop a node, no future path can be shorter — this is why it's greedy and why it fails with negative edges.

**Prim's Algorithm**
- **Definition**: Grows an MST one edge at a time, always adding the cheapest edge from the "tree so far" to a node not yet in the tree.
- **When you encounter it**: "Find the minimum cost to connect all points/nodes." The graph is undirected and you want a spanning tree.
- **Core implementation pattern**: Start from any node, add it to the MST set. Push all its edges to a min-heap. Pop the cheapest edge; if the destination is unvisited, add it to the MST and push its edges. Repeat until all nodes are in the MST.
- **Key insight**: Prim's is essentially Dijkstra but for MST — instead of tracking shortest distance from source, you track cheapest single-edge connection to the growing tree.

**Kruskal's Algorithm**
- **Definition**: Sorts all edges by weight and greedily adds them to the MST if they connect two different components (don't form a cycle).
- **When you encounter it**: Same as Prim — MST problems. Kruskal is often preferred when edges are given as a list (rather than adjacency list) or when the graph is sparse.
- **Core implementation pattern**: Sort edges by weight. Initialize DSU with each node as its own component. For each edge, if `find(u) != find(v)`, union them and add the edge to MST.
- **Key insight**: The DSU makes cycle detection O(α(n)) ≈ O(1) per operation, so the bottleneck is sorting edges: O(E log E).

**Topological Sort (Kahn's Algorithm / BFS)**
- **Definition**: Produces a valid ordering of nodes in a DAG such that all dependencies come before dependents. Kahn's algorithm uses BFS with an indegree array.
- **When you encounter it**: "Find an order to complete courses given prerequisites," "determine build order," "detect if a valid ordering exists (i.e., graph is a DAG)."
- **Core implementation pattern**: Compute indegree for all nodes. Enqueue all nodes with indegree 0. Dequeue a node, add to result, decrement indegree of its neighbors. Enqueue neighbors whose indegree becomes 0. If result length < n, a cycle exists.
- **Key insight**: A node with indegree 0 has no unmet dependencies — it's safe to process. Removing it may free up other nodes (their indegree drops to 0). Cycle detection is free: if you can't process all nodes, there's a cycle.

#### 3) Key Insight / Mental Model
**Advanced graph algorithms are about choosing the right "processing order."** Dijkstra processes nodes by distance (nearest first). Prim/Kruskal process edges by weight (cheapest first). Topological sort processes nodes by dependency (free nodes first). The algorithm is determined by the question: "What does 'next' mean for this problem?" Once you identify the ordering criterion, the data structure follows naturally — min-heap for weighted ordering, queue for dependency ordering, sorted edge list for global weight ordering.

#### 4) Fast Recognition Cues
- **Dijkstra**: Weighted graph + shortest path + non-negative weights. Keywords: "minimum time," "shortest distance," "cheapest route."
- **Bellman-Ford**: Same as Dijkstra but with negative weights or a constraint on number of edges/stops (e.g., "at most K stops").
- **Prim/Kruskal (MST)**: "Minimum total cost to connect all nodes." Undirected graph, want a spanning tree.
- **Topological sort**: DAG + ordering requirement. Keywords: "prerequisites," "dependencies," "build order," "course schedule."
- The graph is explicitly weighted (not just unit weights).
- The problem involves connectivity cost optimization (MST) or path cost optimization (shortest path).
- Cycle detection in a directed graph — topological sort doubles as a cycle detector.

#### 5) When NOT to Use This Pattern
- **Unweighted shortest path**: Use BFS, not Dijkstra. BFS is O(V+E); Dijkstra with a heap is O((V+E) log V) — unnecessary overhead for unit weights.
- **Negative edge weights without negative cycles**: Use Bellman-Ford, not Dijkstra. Dijkstra's greedy assumption breaks with negative edges.
- **All-pairs shortest paths on dense graphs**: Use Floyd-Warshall O(V^3) instead of running Dijkstra V times.
- **Simple connectivity or component counting**: Use BFS/DFS or basic Union-Find, not advanced graph algorithms.
- **Undirected graph ordering**: Topological sort only works on DAGs. For undirected graphs, there's no topological order.

#### 6) Universal Solve Framework
1. **Identify the graph objective:**
   - Shortest path from single source → **Dijkstra** (non-negative weights) or **Bellman-Ford** (negative weights / limited stops).
   - Minimum cost to connect all nodes → **MST** (Prim or Kruskal).
   - Valid dependency ordering → **Topological sort**.
2. **Build the graph representation:**
   - Adjacency list for Dijkstra/Prim/Topo sort.
   - Edge list for Kruskal (natural input format for sorting).
3. **Choose the supporting data structure:**
   - Dijkstra/Prim → min-heap.
   - Kruskal → DSU (Union-Find).
   - Topo sort → indegree array + deque/queue.
4. **Guard against revisits:**
   - Dijkstra: skip if popped distance > recorded distance (`if d > dist[node]: continue`).
   - Prim: skip if node already in MST set.
   - Kruskal: skip if `find(u) == find(v)` (same component = cycle).
   - Topo sort: no revisit issue (each node dequeued once when indegree reaches 0).
5. **Handle edge cases:** disconnected graphs (check if all nodes reached), self-loops, parallel edges.

#### 7) Common Mistakes & Pitfalls
1. **Using Dijkstra with negative edges**: Dijkstra assumes that once a node is finalized, no shorter path exists. Negative edges violate this. Use Bellman-Ford instead.
2. **Not using the lazy deletion pattern in Dijkstra**: Without `if d > dist[node]: continue`, you process stale heap entries and the algorithm is correct but slow (potentially O(V·E)).
3. **Forgetting to initialize distances to infinity**: If you initialize to 0, every node looks reachable at zero cost. Only the source should start at 0.
4. **Topological sort on a graph with cycles**: If the graph has cycles, topo sort cannot produce a valid ordering. Always check: if the result has fewer nodes than the graph, a cycle exists.
5. **Confusing Prim and Dijkstra**: They look similar (both use min-heaps on graphs) but optimize different things. Dijkstra minimizes total path cost from source; Prim minimizes individual edge cost to the growing tree. Using Dijkstra's relaxation logic for MST gives wrong results.

#### 8) Worked Examples (Full Python)

##### Example A: 743. Network Delay Time (Dijkstra)
```python
import heapq
from collections import defaultdict

class Solution:
    def networkDelayTime(self, times: list[list[int]], n: int, k: int) -> int:
        graph = defaultdict(list)
        for u, v, w in times:
            graph[u].append((v, w))

        dist = {i: float('inf') for i in range(1, n + 1)}
        dist[k] = 0
        heap = [(0, k)]

        while heap:
            d, node = heapq.heappop(heap)
            if d > dist[node]:
                continue
            for nei, w in graph[node]:
                nd = d + w
                if nd < dist[nei]:
                    dist[nei] = nd
                    heapq.heappush(heap, (nd, nei))

        ans = max(dist.values())
        return ans if ans < float('inf') else -1
```

**Line-by-line explanation:**

- `import heapq` — Imports Python's heap module, which provides a min-heap implementation. Dijkstra requires efficient extraction of the minimum-distance node, which a min-heap provides in O(log V).

- `from collections import defaultdict` — Imports `defaultdict` for convenient graph construction. Using `defaultdict(list)` means accessing a missing key automatically creates an empty list, avoiding `KeyError`.

- `graph = defaultdict(list)` — Initializes the adjacency list representation. Each key is a node, each value is a list of `(neighbor, weight)` tuples. Adjacency lists are preferred for sparse graphs (O(V+E) space vs. O(V^2) for matrices).

- `for u, v, w in times:` — Builds the graph from the edge list. Each entry `[u, v, w]` represents a directed edge from `u` to `v` with weight `w`.

- `graph[u].append((v, w))` — Adds the directed edge. Note: this is a directed graph (only u→v, not v→u). For undirected graphs, you'd add both directions.

- `dist = {i: float('inf') for i in range(1, n + 1)}` — Initializes shortest distances for all nodes to infinity. Nodes are labeled 1 to n. Infinity means "not yet reachable." This dictionary serves as both the distance tracker and the "visited" check (via the lazy deletion pattern).

- `dist[k] = 0` — Sets the source node's distance to 0. The shortest path from the source to itself is zero.

- `heap = [(0, k)]` — Seeds the min-heap with the source node at distance 0. The heap stores `(distance, node)` tuples; Python's `heapq` is a min-heap, so the smallest distance is always popped first.

- `while heap:` — Processes nodes in order of their tentative distance. The loop continues until the heap is empty (all reachable nodes processed). In the worst case, we push O(E) entries to the heap.

- `d, node = heapq.heappop(heap)` — Pops the node with the smallest tentative distance. This is the greedy choice: the node closest to the source that hasn't been finalized yet.

- `if d > dist[node]:` — **Lazy deletion check.** The heap may contain stale entries for `node` with outdated (larger) distances. If `d` exceeds the current best distance for `node`, this entry is obsolete — skip it. This avoids the need for a `decrease-key` operation (which Python's heapq doesn't support).

- `continue` — Skips processing this stale entry. Without this guard, we'd redundantly relax neighbors, making the algorithm slower.

- `for nei, w in graph[node]:` — Iterates over all neighbors of the current node with their edge weights. This is the "relaxation" step of Dijkstra.

- `nd = d + w` — Calculates the tentative distance to the neighbor via the current node. `d` is the finalized shortest distance to `node`; `w` is the edge weight from `node` to `nei`.

- `if nd < dist[nei]:` — Checks if this new path is shorter than the best known path to `nei`. If so, we've found a better route.

- `dist[nei] = nd` — Updates the best known distance to `nei`. This is the "relaxation" that gives Dijkstra its correctness.

- `heapq.heappush(heap, (nd, nei))` — Pushes the updated distance for `nei` onto the heap. The old entry for `nei` (if any) remains in the heap but will be skipped by the lazy deletion check.

- `ans = max(dist.values())` — The network delay time is the time it takes for the signal to reach the farthest node. This is the maximum shortest-path distance across all nodes.

- `return ans if ans < float('inf') else -1` — If any node remains at infinity, it's unreachable from `k`, so we return -1. Otherwise, return the maximum delay.

**Complexity**: O((V + E) log V) time. Each node is popped from the heap at most once (due to lazy deletion check), and each edge causes at most one heap push. Each heap operation is O(log V). Space is O(V + E) for the graph and distance dictionary.

##### Example B: 210. Course Schedule II (Topological Sort)
```python
from collections import deque, defaultdict

class Solution:
    def findOrder(self, numCourses: int, prerequisites: list[list[int]]) -> list[int]:
        graph = defaultdict(list)
        indegree = [0] * numCourses

        for course, prereq in prerequisites:
            graph[prereq].append(course)
            indegree[course] += 1

        queue = deque()
        for i in range(numCourses):
            if indegree[i] == 0:
                queue.append(i)

        order = []
        while queue:
            node = queue.popleft()
            order.append(node)
            for nei in graph[node]:
                indegree[nei] -= 1
                if indegree[nei] == 0:
                    queue.append(nei)

        return order if len(order) == numCourses else []
```

**Line-by-line explanation:**

- `from collections import deque, defaultdict` — `deque` provides O(1) popleft for BFS; `defaultdict` simplifies graph construction.

- `graph = defaultdict(list)` — Adjacency list: `graph[prereq]` lists all courses that depend on `prereq`. The edge direction is prereq → course ("prereq must come first").

- `indegree = [0] * numCourses` — Tracks how many prerequisites each course still has unmet. A course with indegree 0 can be taken immediately.

- `for course, prereq in prerequisites:` — Each prerequisite pair `[course, prereq]` means "to take `course`, you must first take `prereq`."

- `graph[prereq].append(course)` — Adds directed edge from prereq to course. When we "complete" prereq, we can decrement the indegree of course.

- `indegree[course] += 1` — Course has one more prerequisite to satisfy.

- `queue = deque()` — Initializes the BFS queue for Kahn's algorithm.

- `for i in range(numCourses):` / `if indegree[i] == 0:` / `queue.append(i)` — Seeds the queue with all courses that have no prerequisites. These are the starting points — courses you can take immediately.

- `order = []` — Will hold the topological ordering (valid course sequence).

- `while queue:` — Processes courses in BFS order. Each iteration handles one course with all prerequisites met.

- `node = queue.popleft()` — Takes the next course with indegree 0. This course is "safe" to take now.

- `order.append(node)` — Adds it to the result ordering.

- `for nei in graph[node]:` — Iterates over all courses that depend on `node`.

- `indegree[nei] -= 1` — Completing `node` satisfies one prerequisite of `nei`.

- `if indegree[nei] == 0:` / `queue.append(nei)` — If all of `nei`'s prerequisites are now met, it becomes available to take.

- `return order if len(order) == numCourses else []` — If we processed all courses, `order` is a valid topological sort. If not, a cycle exists (some courses have unresolvable dependencies), so no valid order exists — return empty list.

**Complexity**: O(V + E) time — each node and edge is processed exactly once. O(V + E) space for graph, indegree array, and queue.

#### 9) Additional Practice
- 787. Cheapest Flights Within K Stops
- 1584. Min Cost to Connect All Points
- 1135. Connecting Cities With Minimum Cost
- 332. Reconstruct Itinerary
- 1514. Path with Maximum Probability
- 778. Swim in Rising Water


### Math & Geometry
---
#### 1) Connected Topics + Data Structures
- **Frontmatter subtopics**: Math & Geometry (also referenced as Math & Geography in some metadata — the section covers mathematical reasoning and geometric transformations).
- **Connected structures**:
  - **Matrices**: 2D arrays representing grids, images, or linear transformations. Many geometry problems (rotation, spiral traversal) operate on matrices.
  - **Coordinate transforms**: Operations that map coordinates to new positions — rotation, reflection, translation. Understanding these as mathematical functions helps avoid off-by-one errors.
  - **Modular arithmetic helpers**: For problems involving large numbers, modular arithmetic (`% MOD`) prevents overflow and is needed for combinatorics (factorials, combinations, Fermat's little theorem for modular inverse).
  - **Hash maps for slope representation**: When computing slopes between points, use a canonical fraction representation (reduced by GCD) to avoid floating-point precision issues.

#### 2) Subtopic Deep Dives

**Matrix Rotation**
- **Definition**: Rotating a 2D matrix 90° clockwise in place. The standard technique decomposes this into two simpler operations: transpose (swap rows and columns) then reverse each row.
- **When you encounter it**: "Rotate the image 90 degrees clockwise," "rotate a 2D matrix in place."
- **Core implementation pattern**: Transpose: `matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]` for `j > i`. Then reverse each row.
- **Key insight**: A 90° clockwise rotation = transpose + horizontal flip. A 90° counter-clockwise rotation = transpose + vertical flip. Memorize the decomposition, not the index math.

**Spiral Matrix Traversal**
- **Definition**: Traversing a matrix in spiral order (right → down → left → up, shrinking boundaries).
- **When you encounter it**: "Return all elements of the matrix in spiral order," "fill a matrix in spiral order."
- **Core implementation pattern**: Maintain four boundaries (top, bottom, left, right). Traverse one edge at a time, then shrink the corresponding boundary. Check boundary validity between each direction.
- **Key insight**: After completing each direction, one boundary moves inward. The traversal ends when boundaries cross.

**Fast Exponentiation (Binary Exponentiation)**
- **Definition**: Computing `x^n` in O(log n) time by squaring the base and halving the exponent at each step, using the binary representation of the exponent.
- **When you encounter it**: "Implement `pow(x, n)`," any problem requiring large exponents, modular exponentiation for cryptography or combinatorics.
- **Core implementation pattern**: If `n` is even, `x^n = (x^(n/2))^2`. If `n` is odd, `x^n = x * x^(n-1)`. Handle negative `n` by computing `1 / x^(-n)`.
- **Key insight**: The exponent has O(log n) bits. Each bit corresponds to either squaring or squaring-and-multiplying, giving O(log n) multiplications total.

**GCD and Number Theory**
- **Definition**: The Greatest Common Divisor (GCD) of two numbers is the largest number that divides both. Computed efficiently with Euclid's algorithm: `gcd(a, b) = gcd(b, a % b)`.
- **When you encounter it**: Reducing fractions, determining coprimality, slope computation for geometry problems, LCM computation (`lcm(a,b) = a * b / gcd(a,b)`).
- **Core implementation pattern**: `math.gcd(a, b)` in Python (handles it for you).
- **Key insight**: GCD reduces by at least half each step, so Euclid's algorithm is O(log(min(a,b))).

**Coordinate Geometry Formulas**
- **Definition**: Standard formulas for distance, midpoint, area, slope, and collinearity in 2D space.
- **When you encounter it**: "Find if points are collinear," "compute area of polygon," "detect if a point is inside a rectangle."
- **Key formulas**:
  - Distance: `sqrt((x2-x1)^2 + (y2-y1)^2)`. Use squared distance to avoid floating point when possible.
  - Slope: `(y2-y1)/(x2-x1)` — represent as reduced fraction `(dy/g, dx/g)` to avoid float issues.
  - Cross product (2D): `(x2-x1)*(y3-y1) - (y2-y1)*(x3-x1)` — zero means collinear, sign determines left/right turn.

#### 3) Key Insight / Mental Model
**Math & Geometry problems are about translating a visual/mathematical intuition into code without getting lost in index arithmetic.** The key: always decompose complex transformations into simpler, well-understood steps. Don't try to derive the rotation formula from scratch — decompose it into transpose + reverse. Don't traverse a spiral with complex index math — use shrinking boundaries. The aha: most "geometry" problems in interviews are really "can you carefully manage indices and boundaries without bugs?"

#### 4) Fast Recognition Cues
- The problem involves a 2D matrix and spatial transformations (rotate, reflect, spiral).
- Coordinate geometry: slopes, distances, areas, collinearity.
- Large exponentiation or modular arithmetic requirements.
- The problem has a mathematical formula-based solution (sieve, prime factorization, combinatorics).
- "In-place" matrix modification is required.
- Keywords: "rotate," "spiral," "pow," "GCD," "modulo," "coordinates," "geometry."
- The problem feels like it doesn't fit any "standard" algorithmic pattern — it might be a pure math problem.
- Happy Number, Ugly Number, or other number-theory classification problems.

#### 5) When NOT to Use This Pattern
- **When the problem looks mathematical but is actually DP or graph**: "Minimum path in a grid" looks geometric but is DP or BFS. Don't force geometry when algorithmic patterns apply.
- **When floating-point precision will cause issues**: If you need exact comparisons (slopes, intersections), use integer arithmetic, reduced fractions, or cross products instead of floats.
- **When brute force is fast enough**: For small inputs, directly computing rather than applying clever math formulas may be clearer and sufficient.
- **When the "math trick" is too obscure**: In interviews, if a problem has both a clean algorithmic solution and a mathematical trick, prefer the algorithmic solution unless you can explain the math clearly.

#### 6) Universal Solve Framework
1. **Translate the problem into mathematical terms.** What are the inputs (points, matrices, numbers)? What operation is being asked for (rotation, distance, exponentiation)?
2. **Decompose complex operations into simpler steps.** Rotation = transpose + reverse. Spiral = 4 directional traversals with shrinking bounds. Power = repeated squaring.
3. **Use integer-safe operations where possible.** Avoid floating point for slope comparison (use cross products or reduced fractions). Avoid floating point for distance comparison (compare squared distances).
4. **Validate with tiny manual examples before coding.** Draw a 3x3 matrix, manually rotate it, verify your decomposition works. Trace through your spiral on a 3x4 matrix.
5. **Handle edge cases:** empty matrix, single row/column, negative exponents, division by zero in slopes, `n=0`.
6. **Optimize with symmetry or fast exponentiation when needed.** Many geometry problems have symmetry (rotation has 4-fold symmetry). Exponentiation can be O(log n) instead of O(n).

#### 7) Common Mistakes & Pitfalls
1. **Transpose bounds error**: When transposing, iterate `j` from `i+1` to `n`, not from `0`. Otherwise you swap every pair twice, undoing the transpose.
2. **Spiral boundary check omission**: After traversing right and then down, you must check `top <= bottom` before traversing left, and `left <= right` before traversing up. Skipping these checks leads to duplicated elements.
3. **Floating-point slope comparison**: Comparing slopes as floats (`(y2-y1)/(x2-x1) == (y3-y1)/(x3-x1)`) fails due to precision. Use cross product: `(y2-y1)*(x3-x1) == (y3-y1)*(x2-x1)`.
4. **Negative exponent handling in pow**: `pow(x, -n)` should be computed as `1.0 / pow(x, n)`. But if `n = -2^31`, negating it overflows in some languages (not Python, but be aware in Java/C++).
5. **Not reducing fractions for slope hashing**: If you hash slopes as `(dy, dx)` without reducing by GCD and normalizing the sign, `(2, 4)` and `(1, 2)` hash differently despite representing the same slope.

#### 8) Worked Examples (Full Python)

##### Example A: 48. Rotate Image
```python
class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        n = len(matrix)
        # transpose
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        # reverse each row
        for row in matrix:
            row.reverse()
```

**Line-by-line explanation:**

- `n = len(matrix)` — Gets the matrix dimension. The matrix is n×n (square). We need `n` for loop bounds.

- `for i in range(n):` — Outer loop for the transpose step. Iterates over each row index.

- `for j in range(i + 1, n):` — Inner loop starts at `i + 1`, not `0`. This ensures we only swap each pair `(i, j)` once. If we iterated `j` from `0`, we'd swap each pair twice (at `(i,j)` and at `(j,i)`), undoing the transpose entirely. This is the most common bug in this problem.

- `matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]` — Swaps the element at position `(i, j)` with the element at `(j, i)`. This is the transpose operation: rows become columns. Python's simultaneous assignment avoids needing a temporary variable.

- `for row in matrix:` — After transposing, we reverse each row to complete the 90° clockwise rotation.

- `row.reverse()` — Reverses the row in place. The combination of transpose + row reversal produces a 90° clockwise rotation. To see why: transpose maps `(i, j) → (j, i)`, and reversing the row maps `(j, i) → (j, n-1-i)`. The composition `(i, j) → (j, n-1-i)` is exactly the formula for 90° clockwise rotation.

**Complexity**: O(n^2) time — we visit every element twice (once for transpose, once for reverse). O(1) extra space — all operations are in place. This is optimal because every element must move.

##### Example B: 54. Spiral Matrix
```python
class Solution:
    def spiralOrder(self, matrix: list[list[int]]) -> list[int]:
        result = []
        top, bottom = 0, len(matrix) - 1
        left, right = 0, len(matrix[0]) - 1

        while top <= bottom and left <= right:
            for j in range(left, right + 1):
                result.append(matrix[top][j])
            top += 1

            for i in range(top, bottom + 1):
                result.append(matrix[i][right])
            right -= 1

            if top <= bottom:
                for j in range(right, left - 1, -1):
                    result.append(matrix[bottom][j])
                bottom -= 1

            if left <= right:
                for i in range(bottom, top - 1, -1):
                    result.append(matrix[i][left])
                left += 1

        return result
```

**Line-by-line explanation:**

- `result = []` — Accumulates elements in spiral order.

- `top, bottom = 0, len(matrix) - 1` — Initializes vertical boundaries. `top` is the first unprocessed row (starts at 0); `bottom` is the last unprocessed row (starts at the last row). These boundaries shrink inward as we complete each horizontal traversal.

- `left, right = 0, len(matrix[0]) - 1` — Initializes horizontal boundaries. Same concept: they shrink inward after each vertical traversal.

- `while top <= bottom and left <= right:` — Continues as long as there are unprocessed rows and columns. When boundaries cross, we've covered everything.

- `for j in range(left, right + 1):` / `result.append(matrix[top][j])` — Traverses the top row from left to right. This is the "right" direction of the spiral. We traverse the entire current top row within the current left/right bounds.

- `top += 1` — The top row is now processed; shrink the boundary inward.

- `for i in range(top, bottom + 1):` / `result.append(matrix[i][right])` — Traverses the right column from top to bottom. Note `top` has already been incremented, so we don't revisit the corner element.

- `right -= 1` — The right column is processed; shrink inward.

- `if top <= bottom:` — **Critical boundary check.** After processing the top row and right column, the remaining matrix might have no rows left (single-row case). Without this check, we'd traverse a row we already visited.

- `for j in range(right, left - 1, -1):` / `result.append(matrix[bottom][j])` — Traverses the bottom row from right to left (reverse direction).

- `bottom -= 1` — Bottom row processed; shrink inward.

- `if left <= right:` — Another boundary check. After processing the bottom row, there might be no columns left (single-column case).

- `for i in range(bottom, top - 1, -1):` / `result.append(matrix[i][left])` — Traverses the left column from bottom to top (reverse direction).

- `left += 1` — Left column processed; shrink inward.

- `return result` — Returns all elements in spiral order.

**Complexity**: O(m × n) time — every element is visited exactly once. O(1) extra space (excluding the output list) — only four boundary variables. This is optimal because you must visit every element.

#### 9) Additional Practice
- 50. Pow(x, n)
- 73. Set Matrix Zeroes
- 202. Happy Number
- 149. Max Points on a Line
- 43. Multiply Strings
- 168. Excel Sheet Column Title


## Appendix: Additional Topic Families (Missing in Main Properties)

### Union-Find / Connectivity
- Connected to: Graphs, Advanced Graphs.
- Quick diagnosis: repeated connectivity checks while edges are added.
- Canonical approach: DSU with path compression + union by rank.
- Starter problems: 684, 547, 1319, 1579.

### Monotonic Structures
- Connected to: Stack, Sliding Window.
- Quick diagnosis: next greater/smaller or window max/min in linear time.
- Canonical approach: maintain monotonic invariant; pop while violated.
- Starter problems: 739, 84, 239, 901.

### Segment/Fenwick Trees
- Connected to: Arrays and Hashing, 2-D DP (state query mindset).
- Quick diagnosis: many range queries mixed with updates.
- Canonical approach: tree over indices with O(log n) update/query.
- Starter problems: 307, 315, 327.

### Topological Thinking as Standalone
- Connected to: Advanced Graphs.
- Quick diagnosis: prerequisites/dependency DAG.
- Canonical approach: indegree + queue (Kahn) or DFS postorder.
- Starter problems: 207, 210, 1203.

### Line Sweep / Events
- Connected to: Intervals.
- Quick diagnosis: overlap peaks, active intervals over time.
- Canonical approach: sort start/end events, track active count/heap.
- Starter problems: 253, 759, 732.



## Interview Study Guide
---

### 1) 60-90 Second Diagnosis Checklist
1. Classify problem shape: array/string, linked list, tree, graph, interval, DP.
2. Extract constraints: `n`, value ranges, sorted/unsorted, weighted/unweighted, mutability.
3. Identify required output: boolean, count, min/max, actual path/structure.
4. Ask "Can brute force pass?" If no, identify bottleneck and target complexity.
5. Map clues to pattern quickly:
   - contiguous -> sliding window/prefix
   - sorted + find threshold -> binary search
   - dependencies -> topological sort
   - repeated best candidate -> heap
   - all combinations -> backtracking

### 2) Constraint-to-Complexity Targeting Rules
- `n <= 20`: exponential/backtracking/bitmask may be valid.
- `n <= 10^3`: O(n^2) sometimes okay.
- `n >= 10^5`: usually O(n) or O(n log n) required.
- Dense graph with `V <= 200`: O(V^2) may pass.
- Weighted shortest path (non-negative): Dijkstra preferred over BFS.

### 3) Pattern Selection Decision Tree (Clues -> Technique)
1. Is data hierarchical tree? -> DFS/BFS tree recursion.
2. Is graph relationship with edges?
   - Unweighted shortest path -> BFS
   - Weighted shortest path -> Dijkstra
   - DAG order -> Topological sort
3. Is sequence contiguous constraint? -> Sliding window / prefix sums.
4. Is sorted + boundary/feasibility search? -> Binary search.
5. Is "all possible choices" required? -> Backtracking / DP.
6. Is repeated min/max/top-k extraction? -> Heap.
7. Is overlap by ranges/time? -> Sort intervals / sweep line.

### 4) Brute-Force to Optimal Transition Script
1. State naive method and complexity clearly.
2. Name bottleneck operation (nested scan, repeated recompute, duplicate subproblems).
3. Replace bottleneck with structure/pattern:
   - repeated lookup -> hash map/set
   - repeated range sum -> prefix sums
   - repeated nearest greater -> monotonic stack
   - repeated shortest unweighted path -> BFS
   - repeated subproblems -> DP memo/table
4. Recompute complexity and verify improvement against constraints.

### 5) Edge-Case Checklist + Test Generation Routine
- Edge sizes: empty, single element/node, two elements.
- Value extremes: negatives, zeros, duplicates, large numbers.
- Structural extremes: skewed tree, disconnected graph, all-overlap/no-overlap intervals.
- Pointer boundaries: left/right crossing, off-by-one on windows/ranges.
- Test routine:
  1. Minimal valid case.
  2. Typical case.
  3. Worst-shape case.
  4. Adversarial case that breaks naive assumptions.

### 6) Interview Communication Template
1. Restate problem and assumptions.
2. Propose brute force in one sentence and reject by complexity.
3. Present chosen pattern and invariant.
4. Walk through algorithm on a small example.
5. Implement while narrating key boundary conditions.
6. Conclude with time/space complexity and one edge-case verification.
