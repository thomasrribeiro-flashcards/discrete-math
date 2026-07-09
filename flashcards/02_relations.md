+++
order = 2
subject = "Mathematics"
tags = ["math", "discrete-math", "relations", "equivalence", "partial-order", "reflexive", "transitive"]
+++

# Discrete Math — Relations

## 2.1 Why Relations

Q: Why do we study relations as a separate object after sets?
A: Because many mathematical and computational structures aren't "which elements are collected" but "how elements pair up": $x$ divides $y$, $u$ is a friend of $v$, state $s$ transitions to $s'$. A relation captures this pairing structure directly; many later concepts (functions, orderings, graphs) are built as special kinds of relations.

## 2.2 Binary Relations

C: A [binary relation] from $A$ to $B$ is a subset $R \subseteq A \times B$; we write $a\,R\,b$ or $(a, b) \in R$ to mean "$a$ is related to $b$."

C: A [relation on $A$] is a binary relation from $A$ to itself — a subset $R \subseteq A \times A$.

Q: Give three examples of relations on $\mathbb{Z}$.
A: (i) Divisibility: $a\,R\,b \Leftrightarrow a \mid b$. (ii) Congruence mod $n$: $a \sim_n b \Leftrightarrow n \mid (a - b)$. (iii) Strict inequality: $a\,R\,b \Leftrightarrow a < b$. Each is a specific subset of $\mathbb{Z} \times \mathbb{Z}$.

Q: How many relations are there on a finite set $A$ with $|A| = n$?
A: $2^{n^2}$. A relation is a subset of $A \times A$, which has $n^2$ elements, and each subset corresponds to an independent yes/no choice for each pair.

## 2.3 Properties of Relations

C: A relation $R$ on $A$ is [reflexive] if $\forall a \in A\, (a\,R\,a)$.

C: $R$ is [symmetric] if $\forall a, b \in A\, (a\,R\,b \rightarrow b\,R\,a)$.

C: $R$ is [antisymmetric] if $\forall a, b \in A\, ((a\,R\,b \land b\,R\,a) \rightarrow a = b)$.

C: $R$ is [transitive] if $\forall a, b, c \in A\, ((a\,R\,b \land b\,R\,c) \rightarrow a\,R\,c)$.

Q: Which properties does the "$\leq$" relation on $\mathbb{R}$ satisfy?
A: Reflexive ($a \leq a$), antisymmetric ($a \leq b$ and $b \leq a$ imply $a = b$), and transitive ($a \leq b$ and $b \leq c$ imply $a \leq c$). Not symmetric: $2 \leq 3$ but not $3 \leq 2$.

Q: Why are symmetric and antisymmetric NOT opposites?
A: Because a relation can be both (the equality relation satisfies both: $a = b$ iff $b = a$, and $a = b$ and $b = a$ trivially imply $a = b$). Symmetric says "if related, then so is the reverse"; antisymmetric says "if related both ways, the elements are equal." They can coexist; they are not negations of each other.

## 2.4 Checking Properties

P: Determine which of reflexive, symmetric, antisymmetric, and transitive are satisfied by the relation $R$ on $\mathbb{Z}$ defined by: $a\,R\,b$ iff $a + b$ is even.

S:
**IDENTIFY**: Classify a relation by its properties.

**PLAN**: Check each property against the definition.

**EXECUTE**:
- Reflexive: $a + a = 2a$ is even for every $a \in \mathbb{Z}$. Yes.
- Symmetric: If $a + b$ is even, so is $b + a$ (same number). Yes.
- Transitive: If $a + b$ even and $b + c$ even, then $(a + b) + (b + c) = a + 2b + c$ is even, so $a + c$ is even. Yes.
- Antisymmetric: $2 + 4$ even and $4 + 2$ even, but $2 \neq 4$. NO.

**EVALUATE**: The relation is reflexive, symmetric, and transitive — an equivalence relation (next section). "Same parity" partitions $\mathbb{Z}$ into two classes: evens and odds.

## 2.5 Equivalence Relations

C: A relation $R$ on $A$ is an [equivalence relation] if it is reflexive, symmetric, and transitive.

Q: What do equivalence relations formalize?
A: The notion of "sameness in some respect." Equality is an equivalence relation, but so are "has the same birthday," "is congruent mod $n$," "has the same remainder when divided by $3$." The three axioms — reflexive (things are same as themselves), symmetric (sameness is directionless), transitive (same chains) — capture exactly the structure of "being equivalent under some criterion."

C: The [equivalence class] of $a \in A$ under $R$ is $\lbrack a\rbrack  = \{x \in A : x\,R\,a\}$.

Q: What is the equivalence class of $2$ under congruence mod $5$ on $\mathbb{Z}$?
A: $[2]_5 = \{x \in \mathbb{Z} : x \equiv 2 \pmod 5\} = \{\dots, -8, -3, 2, 7, 12, 17, \dots\}$. All integers with remainder $2$ when divided by $5$.

## 2.6 Equivalence Classes Partition

Q: Why do equivalence classes partition $A$?
A: Because (i) every $a \in A$ lies in $[a]$ (reflexive, so $a\,R\,a$), making the classes cover $A$; (ii) if $[a] \cap [b] \neq \emptyset$, then there's a common element $c$ with $c\,R\,a$ and $c\,R\,b$, so by symmetry and transitivity $a\,R\,b$ and $[a] = [b]$ — distinct classes are disjoint. Together: classes are a partition of $A$.

Q: Why is the converse — every partition induces an equivalence relation — also true?
A: Given a partition $\{A_i\}$, define $a\,R\,b$ iff $a$ and $b$ are in the same block. This is reflexive (every element shares a block with itself), symmetric (being in the same block is symmetric), transitive (three elements in pairwise same blocks all share one block). Equivalence relations and partitions are two sides of the same coin.

## 2.7 Partial Orders

C: A relation $R$ on $A$ is a [partial order] if it is reflexive, antisymmetric, and transitive; the pair $(A, R)$ is a [poset] (partially ordered set).

Q: Why is the divisibility relation $\mid$ on $\mathbb{Z}^+$ a partial order?
A: (i) Reflexive: $a \mid a$ for every positive $a$. (ii) Antisymmetric: $a \mid b$ and $b \mid a$ for positive integers force $a = b$. (iii) Transitive: $a \mid b$ and $b \mid c$ give $a \mid c$. So $(\mathbb{Z}^+, \mid)$ is a poset.

Q: How does a partial order differ from a total order?
A: A total order additionally satisfies: $\forall a, b\, (a\,R\,b \lor b\,R\,a)$ — every pair is comparable. In a partial order, some pairs may be incomparable. Example: under divisibility on $\mathbb{Z}^+$, $2$ and $3$ are incomparable ($2 \nmid 3$ and $3 \nmid 2$). Under $\leq$ on $\mathbb{Z}$, every pair is comparable — a total order.

## 2.8 Comparable and Chain

C: Two elements $a, b$ in a poset are [comparable] if $a \leq b$ or $b \leq a$; otherwise they are [incomparable].

C: A [chain] in a poset is a subset in which every pair is comparable — a totally ordered sub-poset.

C: An [antichain] is a subset in which every pair is incomparable.

Q: In $(\mathcal{P}(\{1,2,3\}), \subseteq)$, give a chain of length $3$ and an antichain of size $3$.
A: Chain: $\emptyset \subseteq \{1\} \subseteq \{1, 2\}$ — three sets, each a subset of the next. Antichain: $\{\{1\}, \{2\}, \{3\}\}$ — three singletons, none a subset of another.

## 2.9 Hasse Diagrams

Q: What is a Hasse diagram?
A: A drawing of a finite poset where elements are vertices, and an edge is drawn from $a$ up to $b$ when $a \leq b$ and there is no intermediate $c$ with $a < c < b$ ($b$ "covers" $a$). Reflexive loops and transitive edges are omitted for clarity. Hasse diagrams visualize a poset's structure without drawing every comparison.

## 2.10 Extremal Elements

C: In a poset $(A, \leq)$, $m \in A$ is a [maximal element] if no element is strictly greater: no $a \in A$ has $m < a$.

C: $M \in A$ is the [maximum] (greatest element) if $a \leq M$ for every $a \in A$.

Q: Why can a poset have multiple maximal elements but never multiple maxima?
A: Multiple maximal elements arise when incomparable elements each have nothing above them. Multiple maxima are impossible — a maximum must dominate everything, so two maxima would have to dominate each other, and antisymmetry would force them equal.

## 2.11 Closures of Relations

C: The [reflexive closure] of $R$ adds all pairs $(a, a)$ to produce the smallest reflexive relation containing $R$.

C: The [symmetric closure] of $R$ adds all pairs $(b, a)$ for each $(a, b) \in R$ to produce the smallest symmetric relation containing $R$.

C: The [transitive closure] $R^*$ of $R$ is the smallest transitive relation containing $R$; equivalently, $(a, b) \in R^*$ iff there is a finite sequence $a = x_0, x_1, \dots, x_k = b$ with $(x_{i-1}, x_i) \in R$ for each step.

Q: Why is transitive closure of a "can reach in one step" relation the same as "can reach in some number of steps"?
A: Because $(a, b) \in R$ means "$a$ reaches $b$ in one step," and transitivity forces $(a, c) \in R^*$ whenever any chain connects $a$ to $c$. Transitive closure turns a step relation into a reachability relation — a computation that graph algorithms implement directly.

## 2.12 Composition of Relations

C: The [composition] of $R \subseteq A \times B$ with $S \subseteq B \times C$ is $S \circ R \subseteq A \times C$ defined by $(a, c) \in S \circ R$ iff there exists $b \in B$ with $(a, b) \in R$ and $(b, c) \in S$.

Q: How does relation composition relate to composition of "one-step" reachability?
A: If $R$ means "one step via red edge" and $S$ means "one step via blue edge," then $S \circ R$ means "red then blue" — one red step followed by one blue. $R^n = R \circ R \circ \dots \circ R$ ($n$ copies) means "reachable in exactly $n$ red steps." Transitive closure is $\bigcup_{n \geq 1} R^n$.

## 2.13 Congruence Modulo $n$

C: For $n \geq 1$, [$a \equiv b \pmod n$] iff $n \mid (a - b)$.

Q: Why is $\equiv \pmod n$ an equivalence relation on $\mathbb{Z}$?
A: (i) Reflexive: $n \mid 0 = (a - a)$. (ii) Symmetric: $n \mid (a - b) \Rightarrow n \mid -(a - b) = (b - a)$. (iii) Transitive: $n \mid (a - b)$ and $n \mid (b - c)$ give $n \mid ((a-b) + (b-c)) = (a - c)$. The three axioms match the structure of divisibility.

Q: What are the equivalence classes of $\mathbb{Z}$ modulo $3$?
A: Three classes: $[0] = \{\dots, -3, 0, 3, 6, \dots\}$, $[1] = \{\dots, -2, 1, 4, 7, \dots\}$, $[2] = \{\dots, -1, 2, 5, 8, \dots\}$. Every integer is in exactly one class, determined by its remainder on division by $3$. The quotient set $\mathbb{Z}/3\mathbb{Z} = \{[0], [1], [2]\}$ is the "integers mod 3," used throughout number theory and cryptography.
