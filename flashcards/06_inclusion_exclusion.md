+++
order = 6
subject = "Mathematics"
tags = ["math", "discrete-math", "inclusion-exclusion", "derangements", "combinatorics"]
+++

# Discrete Math — Inclusion-Exclusion

## 6.1 Two-Set Inclusion-Exclusion (Review)

C: [Two-set IE]: $|A \cup B| = |A| + |B| - |A \cap B|$.

Q: Why must we subtract $|A \cap B|$?
A: Because elements in $A \cap B$ appear in both $A$ and $B$, so they are counted TWICE in $|A| + |B|$. Subtracting once reduces the count for these elements from $2$ to $1$ — exactly the correct amount for the union.

## 6.2 Three-Set Inclusion-Exclusion

C: [Three-set IE]: $|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|$.

Q: Why does the three-set formula ADD back the triple intersection?
A: An element in all three sets is counted $3$ times by $|A| + |B| + |C|$, then subtracted $3$ times (once for each pair), giving a net count of $0$. Adding $|A \cap B \cap C|$ restores the count to $1$. The signs alternate precisely to fix over- and under-counting at each layer.

P: In a class of $100$ students, $55$ take math, $40$ take physics, $25$ take chemistry. $20$ take math+physics, $15$ math+chem, $10$ physics+chem, and $5$ take all three. How many take at least one?
S:
**IDENTIFY**: Three-set inclusion-exclusion.

**PLAN**: Apply the formula directly.

**EXECUTE**:
$|M \cup P \cup C| = 55 + 40 + 25 - 20 - 15 - 10 + 5 = 80$.

**EVALUATE**: Double-check: $100 - 80 = 20$ take none. If we'd forgotten to add back $|M \cap P \cap C|$, we'd have undercounted the triple-takers — classic IE pitfall.

## 6.3 The General Principle

C: [Inclusion-exclusion (general)]: $\left| \bigcup_{i=1}^{n} A_i \right| = \sum_{k=1}^{n} (-1)^{k+1} \sum_{|S| = k} \left| \bigcap_{i \in S} A_i \right|$.

Q: How do you read the general inclusion-exclusion formula?
A: Sum $|A_i|$ (singletons), subtract sum of $|A_i \cap A_j|$ over all pairs, add sum of triple intersections, subtract quadruples, and so on. Signs alternate starting from $+$ at $k = 1$. The inner sum runs over all $k$-subsets of $\{1, \dots, n\}$ — there are $\binom{n}{k}$ terms at layer $k$.

Q: Why is the alternating-sign pattern in IE necessary?
A: Because an element in exactly $m$ of the sets is counted $\sum_{k=1}^{m} (-1)^{k+1} \binom{m}{k}$ times by the formula. This equals $1 - (1-1)^m = 1$ for $m \geq 1$ (by the binomial theorem), so every element of the union is counted exactly once — the signs are calibrated to achieve this.

## 6.4 Complementary Form

Q: How does inclusion-exclusion extend to counting elements in NO set?
A: If $U$ is the universe, $\left| \overline{A_1} \cap \dots \cap \overline{A_n} \right| = |U| - |A_1 \cup \dots \cup A_n|$. Expanding using IE: $|U| - \sum|A_i| + \sum|A_i \cap A_j| - \cdots$ — every sign flips, and $|U|$ heads the sum. This form appears often in "how many fail property $P_i$ for every $i$" counting problems.

## 6.5 Derangements

C: A [derangement] of $\{1, 2, \dots, n\}$ is a permutation $\sigma$ with $\sigma(i) \neq i$ for all $i$ — no fixed points.

Q: Why is counting derangements a natural inclusion-exclusion problem?
A: Let $A_i$ be the set of permutations that DO fix $i$ (i.e., $\sigma(i) = i$). Derangements are permutations in NO $A_i$: $\overline{A_1} \cap \dots \cap \overline{A_n}$. Counting the complement is easy ($|A_{i_1} \cap \dots \cap A_{i_k}|$ is the number of permutations fixing a specified $k$-subset $= (n-k)!$), and IE assembles the total.

C: [Derangement formula]: $D_n = n! \sum_{k=0}^{n} \frac{(-1)^k}{k!}$.

Q: Why is $D_n \approx n!/e$ for large $n$?
A: Because $\sum_{k=0}^{\infty} (-1)^k / k! = e^{-1}$, so the truncated series $\sum_{k=0}^{n} (-1)^k / k!$ converges to $1/e$ rapidly. Hence $D_n / n! \to 1/e$, and $D_n$ is the nearest integer to $n!/e$. Surprising: the proportion of fixed-point-free permutations approaches a constant, about $36.8\%$, regardless of $n$.

P: Compute $D_4$ (derangements of $4$ elements).
S:
**IDENTIFY**: Apply the derangement formula.

**PLAN**: $D_4 = 4! \sum_{k=0}^{4} (-1)^k / k!$.

**EXECUTE**:
$D_4 = 24 \left(1 - 1 + \frac{1}{2} - \frac{1}{6} + \frac{1}{24}\right) = 24 \cdot \frac{9}{24} = 9$.

**EVALUATE**: Sanity check: $4!/e \approx 8.83$, so $D_4 = 9$ matches "nearest integer." The $9$ derangements of $\{1,2,3,4\}$ can also be enumerated directly as a cross-check.

## 6.6 Counting Surjections

Q: How many surjections are there from an $n$-set to a $k$-set?
A: By inclusion-exclusion (excluding functions that miss each target element): $\sum_{j=0}^{k} (-1)^j \binom{k}{j} (k - j)^n$. Here $\binom{k}{j}$ chooses which $j$ elements are "missed," and $(k-j)^n$ counts functions into the remaining $k - j$ targets. Alternating signs correct for overcounting by IE.

Q: What does the surjection count reduce to when $n = k$?
A: $k!$, the number of bijections between two $k$-sets — because every surjection between sets of equal size is a bijection. Verifying this from the IE formula is a nice check.

## 6.7 Size of the Union — Warnings and Tips

Q: Why is inclusion-exclusion often the ONLY efficient approach for union counts?
A: Because direct enumeration of the union's elements is usually infeasible (elements may satisfy multiple $A_i$'s in complicated patterns), but intersections $A_{i_1} \cap \dots \cap A_{i_k}$ are often easy to count individually (shared constraints shrink the set cleanly). IE trades "hard big union" for "easy pattern of intersections."

Q: When does inclusion-exclusion become computationally expensive?
A: When $n$ is large — the formula has $2^n - 1$ terms. For large $n$, IE is only useful when intersections have closed forms, or the problem has structure that makes most terms vanish. For general $n = 20$, $2^{20} - 1 \approx 10^6$ terms is borderline; for $n = 40$, IE alone is infeasible without extra structure.

## 6.8 An IE Example with Divisibility

P: How many integers in $\{1, 2, \dots, 100\}$ are divisible by $2$, $3$, or $5$?
S:
**IDENTIFY**: Three-set IE on divisibility sets.

**PLAN**: $|A_2|, |A_3|, |A_5|$, their pairwise intersections ($A_6, A_{10}, A_{15}$), and the triple intersection ($A_{30}$).

**EXECUTE**:
- $|A_2| = \lfloor 100/2 \rfloor = 50$; $|A_3| = 33$; $|A_5| = 20$.
- $|A_6| = 16$; $|A_{10}| = 10$; $|A_{15}| = 6$.
- $|A_{30}| = 3$.
- $|A_2 \cup A_3 \cup A_5| = 50 + 33 + 20 - 16 - 10 - 6 + 3 = 74$.

**EVALUATE**: The pairwise intersection $A_i \cap A_j$ is "divisible by $\text{lcm}(i,j)$" — we use $\text{lcm}(2,3)=6$, etc. Without IE, you'd enumerate tediously. With IE, one line of arithmetic.

## 6.9 Euler's Totient Function via IE

C: [Euler's totient] $\varphi(n)$ counts the positive integers $\leq n$ that are coprime to $n$.

Q: How does inclusion-exclusion yield $\varphi(n) = n \prod_{p \mid n} \left(1 - \frac{1}{p}\right)$?
A: Let $A_p$ be the multiples of $p$ in $\{1, \dots, n\}$. Integers coprime to $n$ are those in NO $A_p$ for primes $p \mid n$. Applying IE (with $|A_{p_1} \cap \dots \cap A_{p_k}| = n/(p_1 \cdots p_k)$) and factoring gives $n \prod_{p \mid n}(1 - 1/p)$. IE explains why the totient has a multiplicative product structure.

Q: Compute $\varphi(12)$.
A: $12 = 2^2 \cdot 3$, so $\varphi(12) = 12 \cdot (1 - 1/2)(1 - 1/3) = 12 \cdot \frac{1}{2} \cdot \frac{2}{3} = 4$. Coprime values: $\{1, 5, 7, 11\}$. Confirmed.
