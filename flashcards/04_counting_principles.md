+++
order = 4
subject = "Mathematics"
tags = ["math", "discrete-math", "counting", "pigeonhole", "multiplication-rule", "bijection"]
+++

# Discrete Math — Counting Principles

## 4.1 Why Counting Is Hard

Q: Why is counting — which seems simple — a major subfield of discrete math?
A: Because "how many ways" questions quickly become intractable by naive enumeration: "how many passwords of length 8?", "how many rearrangements of MISSISSIPPI?", "how many subsets of $\{1,\dots,20\}$ sum to $50$?" Listing them all is infeasible. Combinatorics supplies principles that compute sizes without enumeration — the raw material of probability, algorithms analysis, and cryptography.

## 4.2 The Addition Rule

C: [Addition rule]: if a task can be done in one of $m$ ways OR one of $n$ DIFFERENT ways, then it can be done in $m + n$ ways.

Q: What is the set-theoretic form of the addition rule?
A: If $A$ and $B$ are disjoint finite sets, $|A \cup B| = |A| + |B|$. Extended to $k$ pairwise disjoint sets: $|A_1 \cup \dots \cup A_k| = |A_1| + \dots + |A_k|$. The "disjoint" hypothesis is essential — if sets overlap, we overcount (fixed by inclusion-exclusion).

Q: How many ways are there to choose a single letter or digit?
A: $26 + 10 = 36$. Letters ($26$) and digits ($10$) are disjoint; addition rule applies.

## 4.3 The Multiplication Rule

C: [Multiplication rule]: if a task consists of $k$ independent steps with $n_1, n_2, \dots, n_k$ options for each step, the total number of ways is $n_1 \cdot n_2 \cdots n_k$.

Q: What is the set-theoretic form of the multiplication rule?
A: $|A_1 \times A_2 \times \dots \times A_k| = |A_1| \cdot |A_2| \cdots |A_k|$. Each element is a $k$-tuple whose coordinates are chosen independently.

P: How many license plates of the form LLL-DDD exist, where L is a letter and D is a digit?

S:
**IDENTIFY**: Sequential choices with fixed alphabet at each slot.

**PLAN**: Multiply options for each position.

**EXECUTE**:
- $3$ letters: $26 \cdot 26 \cdot 26 = 26^3$.
- $3$ digits: $10 \cdot 10 \cdot 10 = 10^3$.
- Total: $26^3 \cdot 10^3 = 17{,}576{,}000$.

**EVALUATE**: Each slot is an independent choice; the multiplication rule combines them. If repetition were disallowed, we'd use permutations (next chapter).

## 4.4 Combining Addition and Multiplication

P: How many strings of length $8$ over $\{A, B, C\}$ begin with either $AA$ or $BBB$?

S:
**IDENTIFY**: Mixed conditions; split into disjoint cases.

**PLAN**:
- Case 1: starts with $AA$ ($2$ fixed, $6$ free positions).
- Case 2: starts with $BBB$ ($3$ fixed, $5$ free positions).
- Cases are disjoint (string can't start with both prefixes).

**EXECUTE**:
- Case 1: $3^6 = 729$.
- Case 2: $3^5 = 243$.
- Total: $729 + 243 = 972$.

**EVALUATE**: Case splits + multiplication rule inside each case — a recurring pattern. Verify cases are disjoint before adding; if they overlap, switch to inclusion-exclusion.

## 4.5 Bijective Counting

Q: What is "bijective counting"?
A: Proving $|A| = |B|$ by constructing a bijection $f: A \to B$. When $|B|$ is known, this immediately gives $|A|$. The technique sidesteps direct enumeration — useful when $A$ is complicated but has a clean correspondence with a simpler structure.

P: Use bijective counting to prove that the number of subsets of $\{1, \dots, n\}$ equals the number of binary strings of length $n$.

S:
**IDENTIFY**: Construct a bijection between subsets and binary strings.

**PLAN**: Map subset $S$ to the string whose $i$-th bit is $1$ iff $i \in S$ (indicator function).

**EXECUTE**:
1. Define $\varphi: \mathcal{P}(\{1,\dots,n\}) \to \{0,1\}^n$ by $\varphi(S)_i = 1$ if $i \in S$, else $0$.
2. $\varphi$ is injective: distinct subsets have distinct indicators.
3. $\varphi$ is surjective: every binary string $(b_1, \dots, b_n)$ is the indicator of $\{i : b_i = 1\}$.
4. So $|\mathcal{P}(\{1,\dots,n\})| = |\{0,1\}^n| = 2^n$.

**EVALUATE**: The bijection doesn't just equate cardinalities — it transports questions about one object to the other. Counting antichains, counting subsets of given size, etc., all translate to string properties.

## 4.6 The Pigeonhole Principle

C: [Pigeonhole principle]: if $n + 1$ or more objects are placed into $n$ boxes, then at least one box contains at least $2$ objects.

Q: Why is the pigeonhole principle "obvious" but surprisingly powerful?
A: Because its applications are non-obvious: clever choices of "objects" and "boxes" prove striking results. The principle itself is just "more items than slots means some slot has multiple items," but finding the right partition is an art — seemingly unrelated questions reduce to pigeonhole in one step.

P: Prove: in any group of $13$ people, at least two share a birth month.

S:
**IDENTIFY**: Classic pigeonhole.

**PLAN**: Identify pigeons and pigeonholes.

**EXECUTE**:
1. Pigeons: $13$ people.
2. Pigeonholes: $12$ months.
3. $13 > 12$, so at least one month contains $\geq 2$ people.

**EVALUATE**: Choosing pigeons and holes IS the proof. The hard part is spotting the right partition — after that, pigeonhole delivers immediately.

## 4.7 Generalized Pigeonhole

C: [Generalized pigeonhole]: if $n$ objects are placed into $k$ boxes, at least one box contains at least $\lceil n/k \rceil$ objects.

Q: Why $\lceil n/k \rceil$ and not $\lfloor n/k \rfloor$?
A: If every box had at most $\lfloor n/k \rfloor$ objects, the total would be at most $k \cdot \lfloor n/k \rfloor$. When $k \nmid n$, this is strictly less than $n$ — contradicting the total. So some box must exceed, reaching $\lceil n/k \rceil$. When $k \mid n$, $\lceil n/k \rceil = n/k$ exactly.

P: In a class of $100$ students, what is the minimum number guaranteed to share a birth month?

S:
**IDENTIFY**: Generalized pigeonhole.

**PLAN**: $n = 100$, $k = 12$.

**EXECUTE**:
$\lceil 100/12 \rceil = \lceil 8.33 \rceil = 9$. At least $9$ students share a month.

**EVALUATE**: This bound is tight — we could have $9$ students in $4$ months and $8$ in $8$ months (total $36 + 64 = 100$), which has exactly $9$ sharing. Without pigeonhole, you'd have to argue by cases; with it, one calculation finishes.

## 4.8 The Subtraction (Complement) Rule

C: [Subtraction rule]: if $A \subseteq U$ and $|U|$ is known, then $|A| = |U| - |A^c|$.

Q: When is it easier to count $A^c$ than $A$?
A: Whenever "not in $A$" has simpler structure. Classic: counting strings of length $n$ over $\{0,1\}$ that contain at least one $0$. The direct count handles many subcases (exactly one $0$, two $0$s, etc.); the complement count is $2^n - 1$ (total minus the all-$1$ string). Complementary counting trades "messy conditions" for "clean universe minus simple cases."

## 4.9 The Division Rule

C: [Division rule]: if a task of counting $A$ is done by a bijection from $A$ to the set of outcomes of another task that counts each element of $A$ exactly $k$ times, then $|A| = |\text{outcomes}|/k$.

P: How many ways to seat $5$ people around a round table, where rotations are considered the same arrangement?

S:
**IDENTIFY**: Circular arrangement — rotations overcounted.

**PLAN**:
- Count arrangements in a line: $5!$.
- Every circular arrangement corresponds to $5$ rotationally-equivalent linear ones.
- Divide by $5$.

**EXECUTE**:
Linear arrangements: $5! = 120$. Rotations per circular arrangement: $5$. Circular arrangements: $120/5 = 24$.

**EVALUATE**: Equivalently, fix one person's seat (say, person $1$) and count arrangements of the other $4$: $4! = 24$. The division rule and "fix a reference" give the same answer.

## 4.10 Counting Checklist

P: How do you approach a "count the number of ways" problem?

S:
**IDENTIFY**: Translate the problem into a well-defined set whose elements are to be counted.

**PLAN**:
- Is it a product of independent choices? Multiplication rule.
- Is it a union of disjoint cases? Addition rule after case analysis.
- Is the complement simpler? Subtraction rule.
- Is there symmetry / overcounting? Division rule.
- Is "some box crowded" enough? Pigeonhole.
- Is it a bijection to a known count? Bijective counting.

**EXECUTE**: Draw small cases by hand to check your formula on $n = 1, 2, 3$. If the formula disagrees with enumeration, the reasoning has a bug — usually overcounting or miscategorization.

**EVALUATE**: Every combinatorial problem has MANY correct approaches. Two different techniques giving the same answer is a strong correctness check.
