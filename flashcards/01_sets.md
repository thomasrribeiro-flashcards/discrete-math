+++
order = 1
subject = "Mathematics"
tags = ["math", "discrete-math", "sets", "cardinality", "power-set", "cartesian-product"]
+++

# Discrete Math — Sets

## 1.1 Why Discrete Mathematics

Q: Why do computer scientists study discrete mathematics rather than continuous mathematics first?
A: Because computation is fundamentally discrete: bits, memory cells, instructions, and program states are all finite or countable. Graphs, counting arguments, recurrences, and modular arithmetic model algorithms and data structures directly. Continuous math (analysis, calculus) models continuous phenomena; discrete math models the structures computation actually runs on.

Q: What distinguishes discrete mathematics from the logic and proofs material that precedes it?
A: Logic provides the language of proof; discrete math applies that language to specific kinds of objects — sets, functions, graphs, integers. Logic tells you how to argue; discrete math gives you the things you argue about. Every proof in this deck assumes fluency with induction, direct proof, and quantifiers from the logic deck.

## 1.2 Set Basics (Review)

C: A [set] is an unordered collection of distinct objects, written with braces: $\{1, 2, 3\}$ or $\{x : P(x)\}$.

C: The [membership] relation $x \in A$ means "$x$ is an element of $A$"; $x \notin A$ means it is not.

Q: Why are $\{1, 2, 2, 3\}$ and $\{1, 2, 3\}$ the same set?
A: Because sets are collections of DISTINCT objects — repeated listings don't create duplicate elements. The shorthand $\{1, 2, 2, 3\}$ denotes exactly the same set as $\{1, 2, 3\}$, namely the set whose elements are $1$, $2$, and $3$. For counting multiplicities, you need multisets, which are a different structure.

Q: Why is the ORDER of elements irrelevant in a set?
A: Because set equality is determined purely by membership: $A = B$ iff $\forall x\, (x \in A \leftrightarrow x \in B)$. Since this condition is symmetric in how elements are listed, $\{1, 2, 3\}$, $\{3, 1, 2\}$, and $\{2, 3, 1\}$ are all the same set. For ordered collections, you use tuples or sequences instead.

## 1.3 Set-Builder Notation

C: [Set-builder notation] $\{x \in A : P(x)\}$ denotes the subset of $A$ consisting of those elements that satisfy $P(x)$.

Q: Write in set-builder notation: "the set of positive even integers less than 20."
A: $\{n \in \mathbb{Z} : n > 0 \land n < 20 \land 2 \mid n\}$, equivalently $\{2k : k \in \mathbb{Z}, 1 \leq k \leq 9\} = \{2, 4, 6, 8, 10, 12, 14, 16, 18\}$. The first form filters integers; the second parametrizes the set — both define it unambiguously.

## 1.4 Common Number Sets

C: [Natural numbers] $\mathbb{N} = \{0, 1, 2, \dots\}$ (some authors start at $1$).

C: [Integers] $\mathbb{Z} = \{\dots, -2, -1, 0, 1, 2, \dots\}$.

C: [Rationals] $\mathbb{Q} = \{p/q : p, q \in \mathbb{Z}, q \neq 0\}$.

C: [Reals] $\mathbb{R}$ — the completion of $\mathbb{Q}$.

Q: Why is the convention "$\mathbb{N}$ starts at $0$ or $1$" a source of confusion?
A: Because different textbooks and traditions choose differently. Computer science usually includes $0$ (indices start at $0$, counting arrays starts with $0$ elements); classical mathematics often excludes it. Always check a book's definition before assuming. In this deck $\mathbb{N}$ includes $0$.

## 1.5 Subset, Equality, Proper Subset

C: $A \subseteq B$ (A is a [subset] of B) iff $\forall x\, (x \in A \rightarrow x \in B)$.

C: $A = B$ iff $A \subseteq B$ and [$B \subseteq A$].

C: $A \subsetneq B$ ($A$ is a [proper subset]) iff $A \subseteq B$ and $A \neq B$.

Q: Why is $\emptyset \subseteq A$ for every set $A$?
A: Because the defining condition $\forall x\, (x \in \emptyset \rightarrow x \in A)$ is vacuously true — no element $x$ is in $\emptyset$, so the implication holds trivially for all $x$.

## 1.6 Set Operations

C: [Union]: $A \cup B = \{x : x \in A \lor x \in B\}$.

C: [Intersection]: $A \cap B = \{x : x \in A \land x \in B\}$.

C: [Difference]: $A \setminus B = \{x : x \in A \land x \notin B\}$.

C: [Symmetric difference]: $A \triangle B = (A \setminus B) \cup (B \setminus A) = \{x : x \in A \oplus x \in B\}$.

Q: Why does each set operation mirror a propositional connective?
A: Because "$x \in \cdot$" is a predicate, and set operations are built by applying propositional connectives to membership predicates: $\cup \leftrightarrow \lor$, $\cap \leftrightarrow \land$, $\setminus \leftrightarrow \land \neg$, $\triangle \leftrightarrow \oplus$. Every set identity is a propositional identity one level up.

## 1.7 Cardinality of Finite Sets

C: The [cardinality] of a finite set $A$, written $|A|$, is the number of elements in $A$.

Q: If $A = \{a, b, c\}$ and $B = \{b, c, d, e\}$, compute $|A|$, $|B|$, $|A \cup B|$, $|A \cap B|$.
A: $|A| = 3$, $|B| = 4$. $A \cup B = \{a, b, c, d, e\}$, so $|A \cup B| = 5$. $A \cap B = \{b, c\}$, so $|A \cap B| = 2$. Note $|A| + |B| = 7 \neq 5 = |A \cup B|$ because the two elements in $A \cap B$ would be double-counted.

C: [Two-set inclusion-exclusion]: $|A \cup B| = |A| + |B| - |A \cap B|$.

Q: Why does the inclusion-exclusion formula subtract $|A \cap B|$?
A: Because elements in $A \cap B$ appear in both $A$ and $B$ and are counted twice in $|A| + |B|$. Subtracting $|A \cap B|$ removes exactly the double-counting, leaving each union element counted once. The full principle of inclusion-exclusion generalizes this to more sets.

## 1.8 Cartesian Product

C: The [Cartesian product] $A \times B = \{(a, b) : a \in A, b \in B\}$ is the set of ordered pairs with first coordinate from $A$ and second from $B$.

Q: How does an ordered pair $(a, b)$ differ from the set $\{a, b\}$?
A: Order matters for pairs: $(1, 2) \neq (2, 1)$ as ordered pairs, but $\{1, 2\} = \{2, 1\}$ as sets. Also, $(a, a)$ is a valid ordered pair (two equal coordinates), while $\{a, a\} = \{a\}$ collapses to a one-element set.

Q: If $|A| = m$ and $|B| = n$ (both finite), what is $|A \times B|$?
A: $|A \times B| = mn$. Each ordered pair is formed by an independent choice of first coordinate ($m$ options) and second coordinate ($n$ options), so the multiplication rule applies.

Q: How does the Cartesian product generalize to $k$ sets $A_1 \times A_2 \times \dots \times A_k$, and what is its cardinality?
A: Elements are $k$-tuples $(a_1, a_2, \dots, a_k)$ with $a_i \in A_i$, and $|A_1 \times \dots \times A_k| = |A_1| \cdot |A_2| \cdots |A_k|$ for finite sets. In particular $A^k = A \times A \times \dots \times A$ ($k$ copies) has size $|A|^k$.

## 1.9 Power Set

C: The [power set] $\mathcal{P}(A)$ is the set of all subsets of $A$: $\mathcal{P}(A) = \{S : S \subseteq A\}$.

Q: List $\mathcal{P}(\{a, b, c\})$ and verify its cardinality.
A: $\mathcal{P}(\{a, b, c\}) = \{\emptyset, \{a\}, \{b\}, \{c\}, \{a, b\}, \{a, c\}, \{b, c\}, \{a, b, c\}\}$ — eight subsets, matching $|\mathcal{P}(A)| = 2^{|A|} = 2^3 = 8$.

P: Prove that $|\mathcal{P}(A)| = 2^{|A|}$ for any finite set $A$.

S:
**IDENTIFY**: Counting identity relating subsets to binary choices.

**PLAN**:
- Exhibit a bijection between $\mathcal{P}(A)$ and the set of functions $A \to \{0, 1\}$.
- Count the functions by the multiplication rule.

**EXECUTE**:
1. Let $A = \{a_1, \dots, a_n\}$. For each subset $S \subseteq A$, define $\chi_S : A \to \{0,1\}$ by $\chi_S(a_i) = 1$ if $a_i \in S$, else $0$ (the indicator function).
2. $S \mapsto \chi_S$ is a bijection: each function is the indicator of exactly one subset.
3. There are $2^n$ functions $A \to \{0,1\}$ — each of the $n$ elements chooses independently from two values.
4. So $|\mathcal{P}(A)| = 2^n = 2^{|A|}$.

**EVALUATE**: Check small cases: $n = 0$ gives $\mathcal{P}(\emptyset) = \{\emptyset\}$ with $1 = 2^0$ subset; $n = 1$ gives $2 = 2^1$. The bijective counting argument is how combinatorics proves $|\text{thing}|$ equals a specific number — find a bijection to something with a known count; the indicator-function bijection is the canonical tool for subset counting.

## 1.10 Disjoint Union and Partitions

C: Sets $A$ and $B$ are [disjoint] if $A \cap B = \emptyset$.

C: A [partition] of a non-empty set $A$ is a collection of non-empty, pairwise disjoint subsets $\{A_1, A_2, \dots\}$ whose union is $A$.

Q: Why are partitions fundamental in combinatorics?
A: Because counting problems often reduce to partitioning: "count the elements by splitting them into disjoint groups." If $A = A_1 \sqcup A_2 \sqcup \dots \sqcup A_k$ is a partition, then $|A| = |A_1| + \dots + |A_k|$. Many counting identities are obtained by partitioning the same set two ways and equating totals.

## 1.11 Universes, Complements, and Venn Diagrams

C: When a [universe] $U$ is fixed, the complement $A^c = U \setminus A$.

Q: Why does every set identity have a "dual" obtained by swapping $\cup \leftrightarrow \cap$ and $\emptyset \leftrightarrow U$?
A: Because complementation is an involution ($(A^c)^c = A$) that exchanges $\cup$ and $\cap$ via De Morgan, and maps $\emptyset$ to $U$ and vice versa. Applying complementation to any true identity yields another true identity. This duality halves the work of memorizing set identities.

## 1.12 Writing Set Proofs

P: Prove $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$.

S:
**IDENTIFY**: Set distributivity; prove set equality via mutual inclusion or biconditional chain.

**PLAN**: Use a biconditional chain on membership.

**EXECUTE**:
$x \in A \cap (B \cup C)$
$\Leftrightarrow x \in A \land (x \in B \lor x \in C)$
$\Leftrightarrow (x \in A \land x \in B) \lor (x \in A \land x \in C)$ (propositional distributivity)
$\Leftrightarrow x \in (A \cap B) \lor x \in (A \cap C)$
$\Leftrightarrow x \in (A \cap B) \cup (A \cap C)$.

**EVALUATE**: Every step is reversible, so a single chain of biconditionals establishes equality. This proof is essentially propositional distributivity lifted to sets — a recurring pattern throughout set theory.
