+++
order = 5
subject = "mathematics"
tags = ["math", "discrete-math", "permutations", "combinations", "binomial-theorem", "pascal"]
+++

# Discrete Math — Permutations and Combinations

## 5.1 Permutations

C: A [permutation] of a set is an arrangement of its elements in a specific order.

Q: Why is the number of permutations of $n$ distinct objects equal to $n!$?
A: By the multiplication rule: the first position has $n$ choices, the second has $n-1$ (one taken), the third $n-2$, and so on down to $1$. The product is $n \cdot (n-1) \cdots 2 \cdot 1 = n!$. Each permutation is a sequence of these independent slot choices.

Q: How many ways can $5$ books be arranged on a shelf?
A: $5! = 120$. Classic permutation count.

## 5.2 $k$-Permutations

C: A [$k$-permutation] of $n$ objects is an ordered arrangement of $k$ of the $n$ objects, with no repetition; the count is $P(n, k) = \frac{n!}{(n-k)!}$.

Q: Why does $P(n, k) = n(n-1)(n-2)\cdots(n-k+1)$?
A: The first of $k$ positions has $n$ options, the second $n-1$, …, the $k$-th has $n-k+1$. This is $k$ consecutive descending factors starting at $n$. Writing as $n!/(n-k)!$ cancels the trailing factors we didn't use.

P: How many ways to award gold, silver, and bronze among $8$ runners?
S:
**IDENTIFY**: Ordered selection of $3$ from $8$, no repetition.

**PLAN**: $P(8, 3)$.

**EXECUTE**: $P(8, 3) = 8 \cdot 7 \cdot 6 = 336$.

**EVALUATE**: Order matters — gold $\neq$ silver $\neq$ bronze — so we use permutations, not combinations. If the three medals were interchangeable, we'd divide by $3!$.

## 5.3 Combinations

Q: A problem says "select $k$ people from $n$." Is it permutation or combination?
A: Combination — "select" implies unordered. If the problem says "arrange" or specifies distinct roles (gold/silver/bronze, president/VP/treasurer), it's permutation.

C: A [combination] $C(n, k) = \binom{n}{k} = \frac{n!}{k!(n-k)!}$ is the number of $k$-element subsets of an $n$-element set.

Q: Why does $\binom{n}{k} = P(n, k)/k!$?
A: Because each $k$-element subset can be ordered in $k!$ ways, so permutations overcount subsets by a factor of $k!$. Dividing recovers unordered counts. Equivalently: first pick the $k$ elements ($\binom{n}{k}$ ways), then order them ($k!$ ways) — the product equals $P(n, k)$.

Q: How many $5$-card poker hands are there from a standard $52$-card deck?
A: $\binom{52}{5} = \frac{52!}{5! \cdot 47!} = 2{,}598{,}960$. Unordered selection — the cards in a hand aren't ordered.

## 5.4 Symmetry of Binomial Coefficients

C: [Symmetry]: $\binom{n}{k} = \binom{n}{n-k}$.

Q: Why is $\binom{n}{k} = \binom{n}{n-k}$?
A: Because choosing $k$ elements to include is equivalent to choosing $n-k$ elements to EXCLUDE. The bijection "subset $\leftrightarrow$ complement" between $k$-subsets and $(n-k)$-subsets proves the identity without algebra.

## 5.5 Pascal's Identity

C: [Pascal's identity]: $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$ for $1 \leq k \leq n-1$.

Q: Why does Pascal's identity hold combinatorially?
A: Fix one element $x$ in the $n$-element set. Every $k$-subset either contains $x$ (then the remaining $k-1$ elements come from the other $n-1$: $\binom{n-1}{k-1}$ ways) or not (all $k$ come from the other $n-1$: $\binom{n-1}{k}$ ways). The cases are disjoint and exhaustive, so their counts sum to $\binom{n}{k}$.

Q: How does Pascal's identity generate Pascal's triangle?
A: Each entry is the sum of the two directly above it. Row $n$ has entries $\binom{n}{0}, \binom{n}{1}, \dots, \binom{n}{n}$; each interior entry is built by applying Pascal's identity to the row above. The boundaries $\binom{n}{0} = \binom{n}{n} = 1$ anchor the recursion.

## 5.6 The Binomial Theorem

C: [Binomial theorem]: $(x + y)^n = \sum_{k=0}^{n} \binom{n}{k} x^{n-k} y^k$.

Q: Why does the binomial theorem hold combinatorially?
A: Expanding $(x + y)^n = (x+y)(x+y)\cdots(x+y)$ produces a sum over all ways to pick $x$ or $y$ from each factor. The term $x^{n-k} y^k$ arises from choosing $y$ in exactly $k$ of the $n$ factors — there are $\binom{n}{k}$ such choices. Collecting gives the stated formula.

Q: What is the coefficient of $x^3 y^5$ in the expansion of $(x + y)^8$?
A: $\binom{8}{5} = \binom{8}{3} = 56$. The general rule: coefficient of $x^{n-k} y^k$ in $(x+y)^n$ is $\binom{n}{k}$.

P: Compute $\sum_{k=0}^{n} \binom{n}{k}$ using the binomial theorem.
S:
**IDENTIFY**: Evaluate a binomial sum by a clever substitution.

**PLAN**: Set $x = y = 1$ in the binomial theorem.

**EXECUTE**:
$(1 + 1)^n = \sum_{k=0}^{n} \binom{n}{k} 1^{n-k} 1^k = \sum_{k=0}^{n} \binom{n}{k}$.
So $\sum_{k=0}^{n} \binom{n}{k} = 2^n$.

**EVALUATE**: The sum of row $n$ of Pascal's triangle is $2^n$ — matching $|\mathcal{P}(\{1,\dots,n\})| = 2^n$, since summing $\binom{n}{k}$ over all $k$ counts all subsets regardless of size.

Q: What is the combinatorial meaning of $\sum_{k=0}^{n}\binom{n}{k} = 2^n$?
A: The left side counts subsets of each size $k$ separately; the right side counts all subsets at once. Both count $|\mathcal{P}(\{1,\dots,n\})|$, partitioned by subset size vs. not partitioned. Equality of counts = two ways to count the same thing.

## 5.7 Permutations with Repetition

C: [Permutations of a multiset]: the number of distinct arrangements of $n$ objects with $n_1$ of type $1$, $n_2$ of type $2$, …, $n_k$ of type $k$ ($n_1 + \dots + n_k = n$) is $\frac{n!}{n_1! \, n_2! \cdots n_k!}$.

Q: Why divide $n!$ by each $n_i!$?
A: Because $n!$ treats identical objects as distinct. Each of the $n_i!$ orderings among type-$i$ objects produces the same visible arrangement, so we divide by $n_i!$ for each type to remove the overcounting.

P: How many distinct arrangements of the letters in MISSISSIPPI?
S:
**IDENTIFY**: Permutations of a multiset.

**PLAN**: $n = 11$; M: $1$, I: $4$, S: $4$, P: $2$.

**EXECUTE**: $\frac{11!}{1! \cdot 4! \cdot 4! \cdot 2!} = \frac{39{,}916{,}800}{1 \cdot 24 \cdot 24 \cdot 2} = 34{,}650$.

**EVALUATE**: Without divisions, we'd count $11!$ sequences; the divisions remove identical rearrangements of each letter type. Sanity check: $34{,}650$ is much less than $11! = 39{,}916{,}800$, reflecting the heavy repetition.

## 5.8 Combinations with Repetition (Stars and Bars)

C: [Combinations with repetition]: the number of ways to choose $k$ objects from $n$ types with repetition allowed is $\binom{n + k - 1}{k}$.

Q: Why does "stars and bars" give this formula?
A: Represent a selection as $k$ stars (objects chosen) separated by $n-1$ bars (dividers between types). This is a sequence of $n + k - 1$ symbols; choose which $k$ are stars: $\binom{n+k-1}{k}$. The bijection between selections and star-bar strings gives the count.

P: How many ways to distribute $10$ identical candies among $4$ children?
S:
**IDENTIFY**: Combinations with repetition — $n = 4$ types (children), $k = 10$ objects.

**PLAN**: $\binom{n + k - 1}{k} = \binom{4 + 10 - 1}{10} = \binom{13}{10}$.

**EXECUTE**: $\binom{13}{10} = \binom{13}{3} = \frac{13 \cdot 12 \cdot 11}{6} = 286$.

**EVALUATE**: The candies are identical, so selections are unordered; children can receive zero, so repetition is allowed — exactly the stars-and-bars setting. If every child had to receive at least one, give one candy to each first and distribute the remaining $6$: $\binom{9}{6} = 84$.

## 5.9 Which Formula Applies?

Q: How do you decide between permutations, combinations, multiset permutations, and stars-and-bars?
A: Ask two questions. (1) Order matters? Yes → permutations; no → combinations. (2) Repetition allowed? Yes → multinomial / stars-and-bars; no → standard $P(n,k)$ or $\binom{n}{k}$. The $2 \times 2$ table: ordered+no rep = $P(n,k)$; ordered+rep = $n^k$; unordered+no rep = $\binom{n}{k}$; unordered+rep = $\binom{n+k-1}{k}$.

Q: What is the count for ordered selections WITH repetition of $k$ items from $n$?
A: $n^k$. Each of the $k$ positions has $n$ choices independently; the multiplication rule gives $n^k$ (example: $k$-letter strings over an $n$-letter alphabet).

## 5.10 Binomial Identities via Combinatorial Proof

P: Prove the Vandermonde identity $\binom{m+n}{k} = \sum_{j=0}^{k} \binom{m}{j} \binom{n}{k-j}$.
S:
**IDENTIFY**: Combinatorial proof — count one set two ways.

**PLAN**: Count $k$-subsets of $\{1, \dots, m+n\}$ by splitting into two buckets of sizes $m$ and $n$.

**EXECUTE**:
- LHS: total $k$-subsets of a $(m+n)$-element set.
- RHS: partition by how many come from the first $m$ elements. Choose $j$ from the first $m$ ($\binom{m}{j}$), then $k - j$ from the remaining $n$ ($\binom{n}{k-j}$). Summing over $j = 0, \dots, k$ covers all cases.
- Both count the same object, so they are equal.

**EVALUATE**: Vandermonde generalizes Pascal's identity ($m = 1$ gives Pascal). Combinatorial proofs reveal WHY an identity holds — the algebra is often opaque, but the set-being-counted makes the identity obvious.
