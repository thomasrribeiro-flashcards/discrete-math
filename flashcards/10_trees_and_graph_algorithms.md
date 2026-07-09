+++
order = 10
subject = "Mathematics"
tags = ["math", "discrete-math", "trees", "spanning-tree", "euler", "hamiltonian", "planar", "coloring"]
+++

# Discrete Math — Trees and Graph Algorithms

## 10.1 Trees

C: A [tree] is a connected, undirected, acyclic graph.

C: A [forest] is an acyclic graph (possibly disconnected) — each connected component is a tree.

Q: A tree is defined as connected and acyclic. Which two edge-count conditions on an $n$-vertex graph are each equivalent to being a tree?
A: (i) connected with exactly $n-1$ edges; (ii) acyclic with exactly $n-1$ edges. Either can serve as the definition; the others become theorems.

Q: A tree is defined as connected and acyclic. Which path-uniqueness condition on a graph is equivalent to being a tree?
A: Between every pair of vertices there is exactly one path.

Q: Why does a tree have exactly $n - 1$ edges?
A: Build the tree by adding edges one at a time. Start with $n$ isolated vertices ($n$ components). Each new edge that doesn't create a cycle joins two components into one, decreasing the component count by $1$. To reach $1$ component (connectedness) without cycles, we need exactly $n - 1$ edges.

## 10.2 Leaves and Internal Vertices

C: A [leaf] of a tree is a vertex of degree $1$; a non-leaf is an [internal vertex].

Q: Why does every tree with at least $2$ vertices have at least $2$ leaves?
A: If $T$ has $n \geq 2$ vertices, $\sum \deg(v) = 2(n-1) < 2n$. If fewer than $2$ leaves existed, at least $n-1$ vertices would have degree $\geq 2$, forcing $\sum \deg(v) \geq 2(n-1) + 1 > 2(n-1)$ — contradiction. Intuition: a tree must "end somewhere," on both ends.

## 10.3 Rooted Trees

C: A [rooted tree] designates one vertex as the root; every other vertex has a unique path to the root.

C: In a rooted tree, the vertices on the unique path from a vertex to the root are its [ancestors]; its [children] are its neighbors further from the root.

Q: Why are rooted trees the natural structure for hierarchical data?
A: Because many data structures (file systems, parse trees, syntax trees, decision trees, heaps) naturally have a "top" with children beneath. Rooting a tree establishes parent/child direction, enables recursion on subtrees, and makes algorithms (tree traversal, DP on trees) straightforward.

## 10.4 Spanning Trees

C: A [spanning tree] of a connected graph $G$ is a subgraph that is a tree and contains all vertices of $G$.

Q: Why does every connected graph have a spanning tree?
A: Remove edges one at a time while preserving connectedness. Each removed edge must lie on a cycle (otherwise its removal would disconnect). When no cycles remain, we have a connected acyclic subgraph spanning all vertices — a spanning tree. Alternatively, BFS or DFS from any vertex produces one constructively.

C: A [minimum spanning tree] (MST) of a weighted connected graph is a spanning tree of minimum total edge weight.

Q: What are two classic MST algorithms?
A: (i) [Kruskal's]: sort edges by weight; add each edge if it doesn't form a cycle (use union-find). (ii) [Prim's]: start from a vertex; repeatedly add the cheapest edge crossing the current tree to a new vertex. Both run in $O(m \log n)$ with appropriate data structures.

P: Describe Kruskal's algorithm on the weighted graph with edges AB(1), BC(2), CD(3), DA(4), AC(5).
S:
**IDENTIFY**: MST via Kruskal.

**PLAN**: Sort edges, union-find for cycle detection.

**EXECUTE**:
1. Sort: AB(1), BC(2), CD(3), DA(4), AC(5).
2. Take AB (components: {A,B}, {C}, {D}).
3. Take BC (components: {A,B,C}, {D}).
4. Take CD (components: {A,B,C,D}) — done.
5. Skip DA and AC (would form cycles).

MST: AB + BC + CD, total weight $1 + 2 + 3 = 6$.

**EVALUATE**: $n - 1 = 3$ edges in the MST on $4$ vertices ✓. Kruskal builds greedily; correctness follows from the "cut property": the cheapest edge crossing a vertex partition always lies in some MST.

## 10.5 Tree Traversals

Q: Name three traversal orders for a rooted binary tree and their uses.
A: (i) [Pre-order] (root, left, right): used for copying a tree, expression prefix-notation. (ii) [In-order] (left, root, right): sorts a BST in ascending order. (iii) [Post-order] (left, right, root): used for deletion (children freed first), postfix-notation. All three are DFS variants with different visit timings.

## 10.6 Eulerian Paths and Circuits

C: An [Eulerian circuit] is a closed walk visiting every EDGE exactly once. An [Eulerian path] is an open walk with the same property.

Q: When does a connected graph have an Eulerian circuit?
A: Iff every vertex has even degree. Proof: enter-and-leave pairing at each vertex means each visit uses two edges; for a closed walk, each vertex must pair up all its incident edges into "enter + leave" pairs — requiring even degree. Converse is also true (Euler–Hierholzer).

Q: When does a connected graph have an Eulerian path (not circuit)?
A: Iff exactly two vertices have odd degree (these are the path's endpoints). All other vertices must have even degree. The classic [Seven Bridges of Königsberg] failure: four odd-degree landmasses means no Eulerian path.

## 10.7 Hamiltonian Paths and Cycles

C: A [Hamiltonian path] visits every VERTEX exactly once; a [Hamiltonian cycle] does the same and returns to its start.

Q: Why is finding a Hamiltonian cycle hard?
A: Because HAMILTONIAN CYCLE is NP-complete — no known polynomial algorithm. Contrast with EULERIAN CIRCUIT, solvable in linear time. The degree characterization for Euler doesn't have an analogue for Hamilton; only sufficient conditions exist (Dirac's theorem: $\deg(v) \geq n/2$ for all $v$ suffices). TSP is the weighted-optimization version.

Q: Contrast Eulerian and Hamiltonian problems.
A: Eulerian = visit every EDGE once (easy — degree check). Hamiltonian = visit every VERTEX once (hard — NP-complete). The one-letter problem (edge vs. vertex) produces a massive complexity gap — an instance of hidden combinatorial difficulty.

## 10.8 Planar Graphs

C: A graph is [planar] if it can be drawn in the plane with no edges crossing (except at shared endpoints).

Q: What is Euler's formula for connected planar graphs?
A: $V - E + F = 2$, where $V$ = vertices, $E$ = edges, $F$ = faces (including the unbounded outer face). Proof by induction on $E$: start with a spanning tree ($F = 1$, $E = V - 1$, check), and each added edge creates one face and preserves the formula.

Q: Why can't $K_5$ or $K_{3,3}$ be drawn in the plane?
A: Euler's formula combined with degree bounds forces $E \leq 3V - 6$ for simple planar graphs (or $E \leq 2V - 4$ for bipartite planar). $K_5$: $V = 5, E = 10$; but $3 \cdot 5 - 6 = 9 < 10$ — contradiction. $K_{3,3}$: $V = 6, E = 9$; but $2 \cdot 6 - 4 = 8 < 9$ — contradiction.

Q: What does Kuratowski's theorem say?
A: A graph is planar iff it does NOT contain a subdivision of $K_5$ or $K_{3,3}$. The two "forbidden minors" $K_5$ and $K_{3,3}$ completely characterize non-planarity — a beautiful structural theorem.

## 10.9 Graph Coloring

C: A [proper $k$-coloring] assigns colors $\{1, \dots, k\}$ to vertices with no two adjacent vertices sharing a color; the [chromatic number] $\chi(G)$ is the minimum $k$ for which this is possible.

Q: What is the chromatic number of $K_n$?
A: $n$. Every pair of vertices is adjacent, so each needs a distinct color — $n$ is a lower bound, and giving each vertex its own color works. No $(n-1)$-coloring exists.

Q: What does the [four color theorem] state?
A: Every planar graph can be properly colored with at most $4$ colors. Hence no map (which corresponds to a planar graph with regions as vertices) needs more than $4$ colors for adjacent regions to differ. Proved by Appel and Haken (1976) — the first major theorem proved with significant computer assistance.

## 10.10 Shortest Path Algorithms

Q: Which algorithm computes single-source shortest paths in an UNWEIGHTED graph, and in what time?
A: BFS, in $O(|V| + |E|)$.

Q: What is the scope and running time of Dijkstra's algorithm?
A: Single-source shortest paths with nonnegative edge weights; $O((|V| + |E|) \log |V|)$ with a heap.

Q: When is Bellman–Ford needed instead of Dijkstra for shortest paths, and what is its running time?
A: When edge weights can be negative (it also detects negative cycles); single-source, $O(|V| \cdot |E|)$.

Q: Which classic algorithm computes ALL-PAIRS shortest paths, and in what time?
A: Floyd–Warshall, in $\Theta(|V|^3)$.

## 10.11 Graph Traversal Decisions

Q: When do you choose DFS over BFS?
A: Use [DFS] for problems needing to probe deep structure — cycle detection, topological sort, strongly-connected components (Tarjan/Kosaraju), articulation points and bridges, backtracking / constraint satisfaction. Use [BFS] for shortest paths in unweighted graphs, level-order traversal, bipartiteness testing, and "nearest-first" explorations. Same $O(|V| + |E|)$ time; different structural views.

## 10.12 Looking Back and Forward

Q: Why is discrete math the right foundation for computer science?
A: Because CS is about manipulating discrete structures — bits, trees, graphs, states — using finite procedures. Induction proves algorithm correctness; counting analyzes running times; graph theory underlies networks, databases, and algorithmic problems; number theory enables cryptography; logic underpins types and verification. Everything in this deck recurs in upper-division CS courses.

Q: What's next after this deck?
A: Depth in three directions: [algorithms] (Cormen-style design and analysis, amortized analysis, randomization, approximation), [theory of computation] (automata, Turing machines, complexity classes), and [advanced combinatorics / probability] (generating functions, random graphs, extremal combinatorics). Each builds on the vocabulary introduced here — so this deck's atoms remain tools throughout.
