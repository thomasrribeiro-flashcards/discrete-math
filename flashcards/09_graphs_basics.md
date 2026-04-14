+++
order = 9
subject = "Math"
tags = ["math", "discrete-math", "graphs", "degree", "paths", "connectivity", "bipartite", "isomorphism"]
+++

# Discrete Math — Graph Theory Basics

## 9.1 What Is a Graph?

C: A [graph] $G = (V, E)$ consists of a set $V$ of [vertices] and a set $E$ of [edges], where each edge is an unordered pair $\{u, v\} \subseteq V$ (for a simple undirected graph).

Q: Why are graphs one of the most important structures in computer science?
A: Because they model relationships: networks, road maps, web links, social connections, dependency graphs, state spaces, circuit diagrams, control flow. A huge swath of algorithms operates on graphs — shortest paths, search, coloring, flow, matching, partitioning. Mastering graphs is mastering an entire algorithmic vocabulary.

## 9.2 Kinds of Graphs

C: A graph is [simple] if it has no loops (edges from a vertex to itself) and no multi-edges (two edges between the same pair).

C: A [directed graph] (digraph) has edges that are ordered pairs $(u, v)$ — direction from $u$ to $v$.

C: A [weighted graph] assigns a real number (weight) to each edge.

Q: Why distinguish directed from undirected graphs?
A: Because direction matters in many applications (web links go one way, flights may not be symmetric, inheritance is asymmetric). Algorithms and properties often differ: strongly connected vs. connected, DAGs vs. cyclic, etc. Always check which model the problem calls for.

## 9.3 Degree

C: The [degree] of a vertex $v$ in an undirected graph, $\deg(v)$, is the number of edges incident to $v$ (with a loop counted twice).

C: In a digraph, the [in-degree] $\deg^-(v)$ is the number of edges ending at $v$, and the [out-degree] $\deg^+(v)$ is the number starting at $v$.

## 9.4 Handshake Lemma

C: [Handshake lemma]: in any undirected graph, $\sum_{v \in V} \deg(v) = 2|E|$.

Q: Why is the handshake lemma true?
A: Because each edge $\{u, v\}$ contributes exactly $1$ to $\deg(u)$ and $1$ to $\deg(v)$ — total $2$. Summing over all edges gives $2|E|$; summing degrees vertex-by-vertex gives the same value. Two ways to count edge-endpoints.

Q: What is an immediate corollary of the handshake lemma?
A: The number of vertices with ODD degree is even. Because the degree sum $\sum \deg(v) = 2|E|$ is even, and an even total with odd summands requires an even count of odd summands. Consequence: you can't have exactly one "odd person out" in a handshaking party.

## 9.5 Common Graph Families

C: A [complete graph] $K_n$ has $n$ vertices and all $\binom{n}{2}$ possible edges — every pair connected.

C: A [cycle] $C_n$ ($n \geq 3$) has $n$ vertices arranged in a cycle: $v_1 v_2 \dots v_n v_1$.

C: A [path graph] $P_n$ has $n$ vertices in a linear chain: $v_1 v_2 \dots v_n$.

Q: How many edges does $K_n$ have?
A: $\binom{n}{2} = n(n-1)/2$. Each of $n$ vertices connects to every other vertex; dividing by $2$ removes double-counting (edge $\{u,v\}$ same as $\{v,u\}$).

## 9.6 Bipartite Graphs

C: A graph is [bipartite] if its vertex set splits into two disjoint sets $V = A \sqcup B$ such that every edge has one endpoint in $A$ and one in $B$.

Q: Why are bipartite graphs common in applications?
A: They model two-sided relationships: people↔events, jobs↔workers, documents↔terms, students↔courses. Maximum matching (assigning workers to jobs) and vertex cover have clean algorithms on bipartite graphs (König's theorem, Hopcroft–Karp).

Q: Characterize bipartite graphs.
A: A graph is bipartite iff it contains NO odd cycle. Proof sketch: if bipartite with bipartition $(A, B)$, any cycle alternates sides, so has even length. Conversely, if no odd cycles, a BFS-based $2$-coloring succeeds. This is the fastest bipartiteness test: $2$-color via BFS and check consistency.

## 9.7 Paths, Cycles, and Connectivity

C: A [path] in a graph is a sequence of distinct vertices $v_0, v_1, \dots, v_k$ with $\{v_{i-1}, v_i\} \in E$ for each $i$; its [length] is $k$ (number of edges).

C: A [cycle] is a path $v_0, v_1, \dots, v_k$ with $v_0 = v_k$ and $k \geq 3$, with all intermediate vertices distinct.

C: A graph is [connected] if there is a path between every pair of vertices.

C: A [connected component] is a maximal connected subgraph.

Q: How does BFS find connected components?
A: Start BFS from any unvisited vertex; all vertices it reaches form one component. Repeat until all vertices are visited. Each BFS run finds one component; the total work is $O(|V| + |E|)$. Same idea with DFS.

## 9.8 Distance and Diameter

C: The [distance] $d(u, v)$ between two vertices is the length of the shortest path from $u$ to $v$ (or $\infty$ if none exists).

C: The [diameter] $\text{diam}(G) = \max_{u, v} d(u, v)$ is the longest shortest path in $G$.

Q: Why does BFS compute single-source shortest paths in unweighted graphs?
A: Because BFS visits vertices in order of increasing distance from the source (layer $0$ first, then distance-$1$ neighbors, then distance-$2$, …). When BFS first reaches a vertex, the path traced is shortest — no earlier-discovered path can be shorter. Running time $O(|V| + |E|)$.

## 9.9 Adjacency Representations

Q: What are the two main ways to represent a graph in memory?
A: (i) [Adjacency matrix]: an $n \times n$ matrix $A$ with $A_{ij} = 1$ iff $\{i, j\}$ is an edge. Space $O(n^2)$, edge-lookup $O(1)$. (ii) [Adjacency list]: for each vertex, a list of its neighbors. Space $O(n + m)$, iteration over neighbors is $O(\deg(v))$.

Q: When do you choose adjacency matrix over adjacency list?
A: When the graph is DENSE (many edges, close to $n^2$), or when frequent edge-lookup queries dominate. Matrices also shine for matrix-based algorithms (Floyd–Warshall, transitive closure via matrix powers). For sparse graphs (most real-world graphs), adjacency lists are far cheaper.

## 9.10 Graph Isomorphism

C: Two graphs $G_1 = (V_1, E_1)$ and $G_2 = (V_2, E_2)$ are [isomorphic] if there is a bijection $\varphi : V_1 \to V_2$ such that $\{u, v\} \in E_1 \Leftrightarrow \{\varphi(u), \varphi(v)\} \in E_2$.

Q: Why is graph isomorphism a subtle problem?
A: Because two graphs can "look different" (different labelings, different drawings) while being structurally identical. No polynomial algorithm is known for general graph isomorphism (though a quasi-polynomial algorithm exists — Babai 2016). Cheap necessary checks: same vertex count, same edge count, same degree sequence — but these are not sufficient.

Q: Are $K_{3,3}$ and $K_6$ isomorphic?
A: No. $K_6$ has $\binom{6}{2} = 15$ edges; $K_{3,3}$ (complete bipartite) has $3 \cdot 3 = 9$ edges. Different edge counts ⇒ not isomorphic. This is the easy direction — one counterexample to a necessary condition rules out isomorphism instantly.

## 9.11 Subgraphs

C: A [subgraph] of $G = (V, E)$ is a graph $H = (V', E')$ with $V' \subseteq V$ and $E' \subseteq E$; edges of $E'$ have both endpoints in $V'$.

C: An [induced subgraph] on $V' \subseteq V$ contains all edges of $E$ with both endpoints in $V'$.

Q: What's the difference between a subgraph and an induced subgraph?
A: A subgraph can drop edges between $V'$-vertices; an induced subgraph includes every edge of $G$ whose endpoints are in $V'$. "Subgraph" is permissive (any subset of edges), "induced" is rigid (exactly the edges the original graph put there).

## 9.12 Graph Coloring (Preview)

C: A [proper $k$-coloring] of a graph $G$ assigns each vertex one of $k$ colors so that adjacent vertices get different colors; the [chromatic number] $\chi(G)$ is the smallest $k$ admitting a proper $k$-coloring.

Q: What is the chromatic number of a bipartite graph?
A: Exactly $2$ (if it has at least one edge) — the bipartition gives a valid $2$-coloring; a graph with an edge needs at least $2$ colors. Thus "bipartite" and "$2$-colorable" are the same thing for graphs with at least one edge. Chromatic number will be explored further in the next chapter.
