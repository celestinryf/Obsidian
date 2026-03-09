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

#### 2) Fast Recognition Cues
- You need O(1) membership/count while scanning array/string.
- Pair/grouping/dedup language appears.
- Brute force is O(n^2), but one-pass state can reduce to O(n).

#### 3) Universal Solve Framework
1. Identify if order matters or only counts/membership matter.
2. Choose map key: value, index, frequency tuple, prefix sum.
3. Write one-pass invariant (`state before/after processing i`).
4. Confirm collisions/duplicates/negative numbers are handled.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n) time, O(n) space.
- Why optimal: single pass with O(1) average complement lookup.

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
- Complexity: O(n * k) time, O(n * k) space.
- Why optimal: canonical signature removes pairwise string comparisons.

#### 5) Additional Practice
- 128. Longest Consecutive Sequence
- 238. Product of Array Except Self
- 36. Valid Sudoku
- 560. Subarray Sum Equals K
- 347. Top K Frequent Elements

### Two Pointers
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: (empty; inferred pointer movement patterns).
- Connected structures: arrays/strings, sorted arrays, sometimes linked lists.

#### 2) Fast Recognition Cues
- Ask for pair/triplet conditions in sorted data.
- Need in-place compaction or opposite-end scanning.
- Brute force nested loops can be replaced by coordinated pointer moves.

#### 3) Universal Solve Framework
1. Decide pointer direction: same direction (fast/slow) or opposite ends.
2. Define movement rule from comparison outcome.
3. Prove each move discards impossible candidates.
4. Handle duplicates/boundaries explicitly.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n) time, O(1) space.
- Why optimal: each character processed at most once.

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
- Complexity: O(n) time, O(1) space.
- Why optimal: moving taller line cannot improve area when shorter line limits height.

#### 5) Additional Practice
- 15. 3Sum
- 167. Two Sum II - Input Array Is Sorted
- 42. Trapping Rain Water
- 283. Move Zeroes

### Stack
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Stacks.
- Connected structures: list-as-stack, monotonic stack.

#### 2) Fast Recognition Cues
- Nested structure matching (`()[]{}`).
- Next greater/smaller element or nearest boundary.
- Need to process while preserving unresolved candidates.

#### 3) Universal Solve Framework
1. Define what each stack element stores (index/value/pair).
2. Define pop condition (while invalid by current item).
3. On pop, finalize answer for popped item.
4. Push current as unresolved candidate.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n) time, O(n) space.
- Why optimal: one pass and each char pushed/popped once.

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
- Complexity: O(n) time, O(n) space.
- Why optimal: monotonic stack avoids repeated forward scans.

#### 5) Additional Practice
- 84. Largest Rectangle in Histogram
- 155. Min Stack
- 150. Evaluate Reverse Polish Notation
- 853. Car Fleet

### Binary Search
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Search Array, Search Range.
- Connected structures: sorted arrays, implicit monotonic answer space.

#### 2) Fast Recognition Cues
- Sorted input and O(log n) target.
- Condition flips from false -> true (monotonic predicate).
- Asking for first/last valid position or minimum feasible value.

#### 3) Universal Solve Framework
1. Define search domain (indices or numeric answer range).
2. Define monotonic predicate `can(mid)`.
3. Use boundary pattern (`while l <= r` or lower-bound form).
4. Prove correctness on edge cases (all false/all true).

#### 4) Worked Examples (Full Python)
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
- Complexity: O(log n) time, O(1) space.

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
- Complexity: O(n log M) time, O(1) space (`M = max(piles)`).
- Why optimal: monotonic feasibility over speed.

#### 5) Additional Practice
- 34. Find First and Last Position of Element in Sorted Array
- 153. Find Minimum in Rotated Sorted Array
- 33. Search in Rotated Sorted Array
- 1011. Capacity To Ship Packages Within D Days

### Sliding Window
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Sliding Window Fixed Size, Variable Size.
- Connected structures: two pointers, hash map/set, deque (for monotonic windows).

#### 2) Fast Recognition Cues
- Contiguous subarray/substring constraints.
- Need max/min length/value over all windows.
- Recomputing each window from scratch is too slow.

#### 3) Universal Solve Framework
1. Expand right pointer to include new element.
2. Update window state (counts/sum/max deque).
3. While invalid, shrink from left and repair state.
4. Record answer when window meets objective.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n) time, O(k) space.

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
- Complexity: O(n) time, O(k) space.
- Why optimal: each pointer moves at most n times.

#### 5) Additional Practice
- 209. Minimum Size Subarray Sum
- 567. Permutation in String
- 424. Longest Repeating Character Replacement
- 239. Sliding Window Maximum

### Linked List
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Singly Linked Lists, Doubly Linked Lists, Fast and Slow Pointers.
- Connected structures: `ListNode`, dummy nodes, fast/slow pointers.

#### 2) Fast Recognition Cues
- Input/output is linked list.
- Need pointer rewiring, cycle checks, midpoint, or in-place transforms.

#### 3) Universal Solve Framework
1. Use dummy head when deleting/inserting near head.
2. Draw pointer transitions before coding.
3. Store next pointer before rewiring.
4. Prefer fast/slow for cycle/middle detection.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n) time, O(1) space.

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
- Complexity: O(n) time, O(1) space.
- Why optimal: Floyd's cycle detection avoids extra memory.

#### 5) Additional Practice
- 21. Merge Two Sorted Lists
- 19. Remove Nth Node From End of List
- 143. Reorder List
- 2. Add Two Numbers

### Trees
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: BST Insert and Remove, Depth-First Search, Breadth-First Search, BST Sets and Maps, Iterative DFS.
- Connected structures: `TreeNode`, recursion stack, queue for BFS, explicit stack for iterative DFS.

#### 2) Fast Recognition Cues
- Hierarchical parent-child structure.
- Path/depth/subtree/ancestor language.
- Need aggregate from children to parent.

#### 3) Universal Solve Framework
1. Decide traversal order: preorder/inorder/postorder/level order.
2. Define recursive return meaning at each node.
3. Combine left/right results into current result.
4. For BST, leverage ordering to prune search.

#### 4) Worked Examples (Full Python)
##### Example A: 104. Maximum Depth of Binary Tree
```python
class Solution:
    def maxDepth(self, root) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```
- Complexity: O(n) time, O(h) space.

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
- Complexity: O(n) time, O(h) space.
- Why optimal: single traversal with bounds.

#### 5) Additional Practice
- 226. Invert Binary Tree
- 230. Kth Smallest Element in a BST
- 199. Binary Tree Right Side View
- 236. Lowest Common Ancestor of a Binary Tree

### Tries
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Trie.
- Connected structures: trie node with children map and terminal flag.

#### 2) Fast Recognition Cues
- Many strings, repeated prefix queries.
- Need `startsWith` or wildcard prefix branching.

#### 3) Universal Solve Framework
1. Define node fields: `children`, `is_end`.
2. Implement insert/search/prefix traversal.
3. For board search, combine trie with DFS and pruning.

#### 4) Worked Example (Full Python)
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
- Complexity: O(L) per operation.
- Why optimal: direct prefix traversal, no full dictionary scans.

#### 5) Additional Practice
- 211. Design Add and Search Words Data Structure
- 212. Word Search II
- 648. Replace Words

### Heap/Priority Queue
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Heap Priorities, Push and Pop, Heapify, Two Heaps.
- Connected structures: min-heap/max-heap (negated values), tuples for priorities.

#### 2) Fast Recognition Cues
- Need repeated min/max extraction with updates.
- Top-k / kth problems.
- Streaming data with rolling best candidates.

#### 3) Universal Solve Framework
1. Decide heap invariant (min of kept items or max frontier).
2. Store tuples when tie-break keys needed.
3. Keep heap size bounded for top-k memory control.
4. For median, rebalance two heaps each insertion.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n log k) time, O(k) space.

##### Example B: 973. K Closest Points to Origin
```python
import heapq

class Solution:
    def kClosest(self, points: list[list[int]], k: int) -> list[list[int]]:
        heap = []  # max-heap using negative distance
        for x, y in points:
            dist = x * x + y * y
            heapq.heappush(heap, (-dist, x, y))
            if len(heap) > k:
                heapq.heappop(heap)
        return [[x, y] for _, x, y in heap]
```
- Complexity: O(n log k) time, O(k) space.
- Why optimal: tracks only k best candidates.

#### 5) Additional Practice
- 347. Top K Frequent Elements
- 621. Task Scheduler
- 295. Find Median from Data Stream
- 23. Merge k Sorted Lists

### Backtracking
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Tree Maze, Subsets, Combinations, Permutations.
- Connected structures: recursion stack, path list, used-set/bitmask.

#### 2) Fast Recognition Cues
- Need all combinations/permutations/partitions.
- Decision tree with constraints and pruning.

#### 3) Universal Solve Framework
1. Define state (`index`, `path`, remaining constraints).
2. Add choose/unchoose transitions.
3. Prune invalid branches early.
4. Append copy of path at terminal states.

#### 4) Worked Example (Full Python)
##### Example: 78. Subsets
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
- Complexity: O(n * 2^n) time, O(n) recursion stack.
- Why optimal: output size itself is 2^n.

#### 5) Additional Practice
- 39. Combination Sum
- 46. Permutations
- 17. Letter Combinations of a Phone Number
- 51. N-Queens

### Graphs
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Intro to Graphs, Matrix DFS, Matrix BFS, Adjacency List.
- Connected structures: adjacency list, queue, stack/recursion, visited set.

#### 2) Fast Recognition Cues
- Objects with links/edges.
- Need component counting, reachability, shortest unweighted steps.
- Grid traversal (cells as graph nodes).

#### 3) Universal Solve Framework
1. Build adjacency representation (explicit or implicit in grid).
2. Choose traversal: DFS for exploration, BFS for shortest unweighted path.
3. Track visited to avoid repeats/cycles.
4. Process per component/source and aggregate answer.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(mn) time, O(mn) worst-case recursion stack.

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
- Complexity: O(V + E) time, O(V) space.
- Why optimal: each node/edge visited once.

#### 5) Additional Practice
- 994. Rotting Oranges
- 695. Max Area of Island
- 417. Pacific Atlantic Water Flow
- 207. Course Schedule

### 1-D DP
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: 1-Dimension DP, Palindromes.
- Connected structures: DP arrays, rolling variables.

#### 2) Fast Recognition Cues
- "Best/count/ways" with overlapping subproblems on linear index.
- Greedy/local choice fails due to future dependency.

#### 3) Universal Solve Framework
1. Define `dp[i]` meaning clearly.
2. Write transition from smaller states.
3. Set base cases correctly.
4. Optimize space if only recent states are needed.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n) time, O(1) space.

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
- Complexity: O(n) time, O(1) space.
- Why optimal: DP captures "take vs skip" at each house.

#### 5) Additional Practice
- 746. Min Cost Climbing Stairs
- 322. Coin Change
- 5. Longest Palindromic Substring
- 300. Longest Increasing Subsequence

### Intervals
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: (empty; inferred interval processing).
- Connected structures: sorted arrays, sweep events, min-heaps.

#### 2) Fast Recognition Cues
- Input contains many `[start, end]` ranges.
- Need merge, overlap count, or scheduling with conflicts.

#### 3) Universal Solve Framework
1. Sort by start time (or end time for greedy deletions).
2. Track current active interval and decide merge/conflict.
3. For room count, track smallest ending time via min-heap.

#### 4) Worked Examples (Full Python)
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
- Complexity: O(n log n) time, O(n) space.

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
- Complexity: O(n log n) time, O(1) extra space (ignoring sort).
- Why optimal: earliest-end greedy leaves maximum room for future intervals.

#### 5) Additional Practice
- 57. Insert Interval
- 252. Meeting Rooms
- 253. Meeting Rooms II
- 986. Interval List Intersections

### Greedy
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Kadane's Algorithm.
- Connected structures: arrays, running states, sorting by key.

#### 2) Fast Recognition Cues
- Need local decision that preserves global optimality.
- DP is possible but greedy offers simpler O(n) or O(n log n).

#### 3) Universal Solve Framework
1. Propose local choice rule.
2. Justify with exchange argument or invariant.
3. Track minimal state proving correctness.

#### 4) Worked Example (Full Python)
##### Example: 55. Jump Game
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
- Complexity: O(n) time, O(1) space.
- Why optimal: track reachable frontier only; no need to explore paths.

#### 5) Additional Practice
- 53. Maximum Subarray (Kadane)
- 134. Gas Station
- 452. Minimum Number of Arrows to Burst Balloons
- 763. Partition Labels

### 2-D DP
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: 2-Dimension DP, 0/1 Knapsack, Unbounded Knapsack, LCS.
- Connected structures: 2D tables, rolling rows, memoized recursion.

#### 2) Fast Recognition Cues
- State depends on two indices or dimensions (i, j / capacity, index).
- Need optimal value/count across grid-style state space.

#### 3) Universal Solve Framework
1. Define `dp[i][j]` meaning.
2. Determine transitions from up/left/diag or take/skip.
3. Initialize row 0/col 0 base states.
4. Choose bottom-up or top-down memoization.

#### 4) Worked Example (Full Python)
##### Example: 1143. Longest Common Subsequence
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
- Complexity: O(mn) time, O(mn) space.
- Why optimal: explores each 2D state once.

#### 5) Additional Practice
- 62. Unique Paths
- 72. Edit Distance
- 518. Coin Change II
- 494. Target Sum

### Bit Manipulation
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Bit Operations.
- Connected structures: integers as bitsets, XOR masks.

#### 2) Fast Recognition Cues
- Very small memory/state, parity, toggle, single odd occurrence.
- Need subset compression or fast set operations.

#### 3) Universal Solve Framework
1. Identify bit-level identity (`x ^ x = 0`, `x & (x - 1)` drops lowest set bit).
2. Map problem entities to bit positions.
3. Use masks for state transitions/checks.

#### 4) Worked Example (Full Python)
##### Example: 136. Single Number
```python
class Solution:
    def singleNumber(self, nums: list[int]) -> int:
        ans = 0
        for x in nums:
            ans ^= x
        return ans
```
- Complexity: O(n) time, O(1) space.
- Why optimal: XOR cancels duplicates pairwise.

#### 5) Additional Practice
- 191. Number of 1 Bits
- 338. Counting Bits
- 268. Missing Number
- 371. Sum of Two Integers

### Advanced Graphs
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: Djikstra's, Prim's, Kruskal's, Topological Sort.
- Connected structures: adjacency list, min-heap, DSU, indegree array + queue.

#### 2) Fast Recognition Cues
- Weighted graph shortest path (non-negative): Dijkstra.
- Minimum total connection cost: MST (Prim/Kruskal).
- Dependency ordering in DAG: topological sort.

#### 3) Universal Solve Framework
1. Pick algorithm by graph objective:
   - shortest path -> Dijkstra/Bellman-Ford
   - MST -> Prim/Kruskal
   - ordering -> topo sort
2. Choose supporting DS (heap/DSU/indegree queue).
3. Guard against revisits with distance checks or visited set.

#### 4) Worked Example (Full Python)
##### Example: 743. Network Delay Time (Dijkstra)
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
- Complexity: O((V + E) log V) time, O(V + E) space.
- Why optimal: standard non-negative shortest path solution.

#### 5) Additional Practice
- 787. Cheapest Flights Within K Stops
- 1584. Min Cost to Connect All Points
- 1135. Connecting Cities With Minimum Cost
- 210. Course Schedule II

### Math & Geometry
---
#### 1) Connected Topics + Data Structures
- Frontmatter subtopics: (property name is `Math & Geography`, section kept as `Math & Geometry`).
- Connected structures: matrices, coordinate transforms, modular arithmetic helpers.

#### 2) Fast Recognition Cues
- Coordinate transforms, rotations, slopes, area/perimeter.
- Large exponentiation/division constraints needing number-theory tricks.

#### 3) Universal Solve Framework
1. Translate geometry/math statement into formulas/invariants.
2. Use integer-safe operations where possible.
3. Validate with tiny manual examples before coding.
4. Optimize with symmetry or fast exponentiation when needed.

#### 4) Worked Example (Full Python)
##### Example: 48. Rotate Image
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
- Complexity: O(n^2) time, O(1) extra space.
- Why optimal: in-place transform via transpose + reverse.

#### 5) Additional Practice
- 50. Pow(x, n)
- 54. Spiral Matrix
- 73. Set Matrix Zeroes
- 202. Happy Number

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
