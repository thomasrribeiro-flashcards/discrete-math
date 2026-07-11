+++
order = 3
subject = "mathematics"
tags = ["math", "discrete-math", "functions", "injective", "surjective", "bijective", "inverse"]
+++

# Discrete Math — Functions

## 3.1 Functions as Relations

C: A [function] $f: A \to B$ is a relation from $A$ to $B$ such that for every $a \in A$ there exists EXACTLY ONE $b \in B$ with $(a, b) \in f$; we write $f(a) = b$.

Q: Why is "every $a$ has exactly one $b$" the defining property of a function?
A: Because functions model DETERMINISTIC mappings: given an input, the output is uniquely determined. Allowing multiple outputs would give a general relation (or a "multi-function"); allowing no output for some inputs would give a partial function. Total, single-valued — that's what we call a function.

C: For $f: A \to B$, $A$ is the [domain] and $B$ is the [codomain].

C: For $f: A \to B$, the [range] (or image) is $f(A) = \{f(a) : a \in A\} \subseteq B$.

Q: Why must the codomain be distinguished from the range?
A: Because the codomain is a design choice (what type of output is allowed), while the range is the actual set of outputs produced. Function $f: \mathbb{Z} \to \mathbb{Z}$ with $f(n) = n^2$ has codomain $\mathbb{Z}$ but range $\{0, 1, 4, 9, 16, \dots\}$ — the non-negative squares. Two functions with the same formula but different codomains are considered different functions (this matters for surjectivity).

## 3.2 Injective (One-to-One)

C: $f: A \to B$ is [injective] (one-to-one) if $\forall a_1, a_2 \in A\, (f(a_1) = f(a_2) \rightarrow a_1 = a_2)$.

Q: What is the contrapositive form of injectivity?
A: $\forall a_1, a_2 \in A\, (a_1 \neq a_2 \rightarrow f(a_1) \neq f(a_2))$ — "distinct inputs produce distinct outputs." Both forms are used interchangeably; the first is usually easier in proofs, the second captures the intuition.

P: Prove that $f: \mathbb{R} \to \mathbb{R}$ defined by $f(x) = 3x + 7$ is injective.

S:
**IDENTIFY**: Injectivity proof — assume $f(a) = f(b)$, deduce $a = b$.

**PLAN**: Algebraic manipulation.

**EXECUTE**:
1. Suppose $f(a) = f(b)$.
2. $3a + 7 = 3b + 7$.
3. $3a = 3b$, so $a = b$.

**EVALUATE**: Linear functions with non-zero slope are injective — each output comes from exactly one input. The proof is short because the algebra is easy; the pattern (assume equality of outputs, derive equality of inputs) generalizes to any injectivity proof.

## 3.3 Surjective (Onto)

C: $f: A \to B$ is [surjective] (onto) if $\forall b \in B\, \exists a \in A\, (f(a) = b)$.

Q: What does surjectivity mean geometrically on a graph?
A: Every horizontal line at height $y \in B$ hits the graph of $f$ somewhere. Equivalently, the range equals the codomain — nothing in $B$ is "missed" by $f$.

P: Prove that $f: \mathbb{Z} \to \mathbb{Z}$ defined by $f(n) = n + 5$ is surjective.

S:
**IDENTIFY**: Surjectivity — given $b \in B$, produce $a \in A$ with $f(a) = b$.

**PLAN**: Solve $f(a) = b$ for $a$ and verify $a \in A$.

**EXECUTE**:
1. Let $b \in \mathbb{Z}$ be arbitrary.
2. Set $a = b - 5$. Then $a \in \mathbb{Z}$.
3. $f(a) = a + 5 = (b - 5) + 5 = b$.
4. So $f$ is surjective.

**EVALUATE**: Showing surjectivity means producing a pre-image for every possible output. "Set $a = b - 5$" was the guess — justified by solving the equation — and the check $f(a) = b$ confirms it works.

## 3.4 Bijective

C: $f: A \to B$ is [bijective] if it is both injective and surjective — every $b \in B$ has exactly one pre-image $a \in A$.

Q: Why are bijections called "one-to-one correspondences"?
A: Because a bijection pairs each element of $A$ with exactly one element of $B$ and vice versa — a perfect matching. For finite sets, $|A| = |B|$ if and only if a bijection exists between them; this is the foundation of combinatorial counting.

Q: Give a bijection from $\mathbb{N}$ to $\mathbb{Z}$.
A: $f(n) = \begin{cases} n/2 & \text{if } n \text{ even} \\ -(n+1)/2 & \text{if } n \text{ odd} \end{cases}$, giving $0 \mapsto 0, 1 \mapsto -1, 2 \mapsto 1, 3 \mapsto -2, 4 \mapsto 2, \dots$ — a zig-zag that hits every integer exactly once. This shows $\mathbb{N}$ and $\mathbb{Z}$ have the same cardinality.

## 3.5 Composition of Functions

C: If $f: A \to B$ and $g: B \to C$, the [composition] $g \circ f : A \to C$ is defined by $(g \circ f)(a) = g(f(a))$.

Q: Why does composition require the codomain of $f$ to match the domain of $g$?
A: Because $g$ can only be applied to elements of its domain. If $f: A \to B$ and $g: B \to C$, then $f(a) \in B$ is a valid input to $g$. Writing $g \circ f$ when $f$'s range overlaps but doesn't lie entirely in $g$'s domain is undefined.

Q: For injective $f: A \to B$ and $g: B \to C$, why is $g \circ f$ injective?
A: Suppose $(g \circ f)(a_1) = (g \circ f)(a_2)$, i.e., $g(f(a_1)) = g(f(a_2))$. By $g$ injective, $f(a_1) = f(a_2)$. By $f$ injective, $a_1 = a_2$. Composition preserves injectivity.

Q: For surjective $f: A \to B$ and $g: B \to C$, why is $g \circ f$ surjective?
A: Let $c \in C$. By $g$ surjective, there's $b \in B$ with $g(b) = c$. By $f$ surjective, there's $a \in A$ with $f(a) = b$. Then $(g \circ f)(a) = g(b) = c$. Composition preserves surjectivity (and therefore bijectivity).

## 3.6 Inverse Functions

C: A function $f: A \to B$ has an [inverse] $f^{-1}: B \to A$ iff $f$ is bijective; $f^{-1}$ satisfies $f^{-1}(f(a)) = a$ for all $a \in A$ and $f(f^{-1}(b)) = b$ for all $b \in B$.

Q: Why does only a bijection have an inverse function?
A: Because $f^{-1}$ must assign to every $b \in B$ a unique $a \in A$ with $f(a) = b$ — which requires $f$ to be surjective (at least one pre-image) and injective (at most one). Both conditions together: bijective. Without bijectivity, $f^{-1}$ is at best a partial or multi-valued relation, not a function.

P: Find the inverse of $f: \mathbb{R} \to \mathbb{R}$, $f(x) = 3x + 7$.

S:
**IDENTIFY**: $f$ is bijective (linear with nonzero slope), so inverse exists.

**PLAN**: Solve $y = 3x + 7$ for $x$ in terms of $y$; rename.

**EXECUTE**:
1. $y = 3x + 7 \Rightarrow x = (y - 7)/3$.
2. So $f^{-1}(y) = (y - 7)/3$.
3. Check: $f^{-1}(f(x)) = (3x + 7 - 7)/3 = x$ and $f(f^{-1}(y)) = 3(y-7)/3 + 7 = y$. Both hold.

**EVALUATE**: Finding an inverse is just solving $y = f(x)$ for $x$. The check step is important — it verifies bijectivity by construction.

## 3.7 Identity Function

C: For any set $A$, the [identity function] $\text{id}_A : A \to A$ is defined by $\text{id}_A(a) = a$.

Q: What are the composition identities involving $\text{id}_A$?
A: For $f: A \to B$: $f \circ \text{id}_A = f$ and $\text{id}_B \circ f = f$. For inverses: $f^{-1} \circ f = \text{id}_A$ and $f \circ f^{-1} = \text{id}_B$. The identity plays the role of "do nothing" — it's the neutral element under composition.

## 3.8 Image and Preimage of a Set

C: For $f: A \to B$ and $S \subseteq A$, the [image] $f(S) = \{f(a) : a \in S\}$.

C: For $T \subseteq B$, the [preimage] (or inverse image) $f^{-1}(T) = \{a \in A : f(a) \in T\}$.

Q: Why is the notation $f^{-1}(T)$ defined even when $f$ has no inverse function?
A: Because $f^{-1}(T)$ is not the inverse of $f$ applied to $T$ — it's the set of all $a$ whose image lies in $T$. This is well-defined for any function $f$, not just bijections. The overloaded notation is standard but confusing; context disambiguates.

Q: If $f: \mathbb{R} \to \mathbb{R}$ is $f(x) = x^2$, what is $f^{-1}([0, 4])$?
A: $\{x \in \mathbb{R} : 0 \leq x^2 \leq 4\} = [-2, 2]$. Preimage captures "all inputs whose output lies in the target set" — even when $f$ isn't invertible, because $f(x) = x^2$ is not injective.

## 3.9 Functions and Cardinality

Q: How do injections, surjections, and bijections between finite sets relate to cardinalities?
A: If $|A| = m$ and $|B| = n$: an injection $A \to B$ exists iff $m \leq n$; a surjection $A \to B$ exists iff $m \geq n$; a bijection exists iff $m = n$. Cardinality comparisons reduce to function existence — the key to the pigeonhole principle next chapter.

## 3.10 Floor, Ceiling, and Common Discrete Functions

C: The [floor function] $\lfloor x \rfloor$ gives the greatest integer $\leq x$; the [ceiling function] $\lceil x \rceil$ gives the least integer $\geq x$.

Q: What is $\lfloor 3.7 \rfloor$, $\lceil 3.7 \rceil$, $\lfloor -2.3 \rfloor$, $\lceil -2.3 \rceil$?
A: $\lfloor 3.7 \rfloor = 3$, $\lceil 3.7 \rceil = 4$, $\lfloor -2.3 \rfloor = -3$ (round DOWN toward $-\infty$), $\lceil -2.3 \rceil = -2$ (round UP toward $+\infty$). Beware: floor and ceiling handle negatives differently from truncation-toward-zero.

Q: Why is $\lfloor \cdot \rfloor: \mathbb{R} \to \mathbb{Z}$ not invertible?
A: Because floor is not injective: $\lfloor 3.1 \rfloor = \lfloor 3.9 \rfloor = 3$. Infinitely many real numbers map to the same integer. Floor and ceiling discard fractional information — a one-way projection.
