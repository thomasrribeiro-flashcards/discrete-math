+++
order = 7
subject = "mathematics"
tags = ["math", "discrete-math", "recurrences", "fibonacci", "characteristic-equation", "closed-form"]
+++

# Discrete Math — Recurrence Relations

## 7.1 What Is a Recurrence?

C: A [recurrence relation] for a sequence $(a_n)$ expresses $a_n$ as a function of earlier terms: $a_n = f(a_{n-1}, a_{n-2}, \dots, a_{n-k})$, with $k$ [initial conditions] to fix the sequence.

Q: Why do recurrences show up everywhere in algorithm analysis?
A: Because divide-and-conquer algorithms naturally produce recurrences: if a problem of size $n$ splits into subproblems and takes $T(n-1)$ or $T(n/2)$ etc., its running time satisfies a recurrence. Solving the recurrence gives asymptotic running time.

Q: What recurrences define the arithmetic, geometric, and Fibonacci sequences?
A: Arithmetic: $a_n = a_{n-1} + d$. Geometric: $a_n = r a_{n-1}$. Fibonacci: $F_n = F_{n-1} + F_{n-2}$ with $F_0 = 0, F_1 = 1$. The first two have simple closed forms; Fibonacci's is more involved.

## 7.2 Solving by Iteration

P: Solve $a_n = 2 a_{n-1} + 3$ with $a_0 = 1$ by iteration.
S:
**IDENTIFY**: Linear first-order nonhomogeneous recurrence; iterate and spot the pattern.

**PLAN**: Expand a few terms, identify the geometric structure, prove by induction.

**EXECUTE**:
- $a_1 = 2 \cdot 1 + 3 = 5$.
- $a_2 = 2 \cdot 5 + 3 = 13$.
- $a_3 = 2 \cdot 13 + 3 = 29$.
- Differences: $a_n + 3 = 2(a_{n-1} + 3)$, so $a_n + 3$ is geometric with ratio $2$ and initial value $a_0 + 3 = 4$.
- $a_n + 3 = 4 \cdot 2^n = 2^{n+2}$, so $a_n = 2^{n+2} - 3$.

**EVALUATE**: Check: $a_0 = 4 - 3 = 1$ ✓; $a_3 = 32 - 3 = 29$ ✓. Iteration surfaces structure; solving adds the algebraic trick (here: shifting to make it geometric).

## 7.3 Linear Homogeneous Recurrences

Q: You see a recurrence $a_n = c_1 a_{n-1} + \dots + c_k a_{n-k}$ (linear homogeneous, constant coefficients). What's the standard solution path?
A: Form the characteristic equation $r^k - c_1 r^{k-1} - \dots - c_k = 0$, find roots, write $a_n$ as a linear combination of $r_i^n$ (or $n^j r_i^n$ for repeated roots), fix constants from initial conditions.

C: A [linear homogeneous recurrence with constant coefficients] has the form $a_n = c_1 a_{n-1} + c_2 a_{n-2} + \dots + c_k a_{n-k}$, with $c_k \neq 0$; "order $k$" refers to the depth of the look-back.

Q: Why does the ansatz $a_n = r^n$ work for linear homogeneous recurrences?
A: Because substituting $a_n = r^n$ into $a_n - c_1 a_{n-1} - \dots - c_k a_{n-k} = 0$ and dividing by $r^{n-k}$ gives $r^k - c_1 r^{k-1} - \dots - c_k = 0$, a polynomial equation in $r$ (the [characteristic equation]). Its roots yield geometric solutions; linearity means sums of solutions are solutions.

C: The [characteristic equation] of $a_n = c_1 a_{n-1} + \dots + c_k a_{n-k}$ is $r^k - c_1 r^{k-1} - \dots - c_k = 0$.

## 7.4 Distinct Roots

C: If the characteristic equation has $k$ distinct roots $r_1, \dots, r_k$, then $a_n =$ [$\alpha_1 r_1^n + \alpha_2 r_2^n + \dots + \alpha_k r_k^n$], with constants $\alpha_i$ fixed by the initial conditions.

P: Solve the Fibonacci recurrence $F_n = F_{n-1} + F_{n-2}$ with $F_0 = 0$, $F_1 = 1$.
S:
**IDENTIFY**: Linear homogeneous, order $2$.

**PLAN**: Characteristic equation $r^2 - r - 1 = 0$; distinct roots give $F_n = \alpha \phi^n + \beta \psi^n$.

**EXECUTE**:
1. Roots: $\phi = (1 + \sqrt{5})/2$, $\psi = (1 - \sqrt{5})/2$ (golden ratio and conjugate).
2. General: $F_n = \alpha \phi^n + \beta \psi^n$.
3. Use initial conditions: $F_0 = \alpha + \beta = 0$ and $F_1 = \alpha \phi + \beta \psi = 1$.
4. From first: $\beta = -\alpha$. Substitute: $\alpha (\phi - \psi) = 1$, and $\phi - \psi = \sqrt{5}$, so $\alpha = 1/\sqrt{5}$.
5. [Binet's formula]: $F_n = \frac{\phi^n - \psi^n}{\sqrt{5}}$.

**EVALUATE**: Since $|\psi| < 1$, $\psi^n \to 0$, so $F_n \approx \phi^n/\sqrt{5}$ — Fibonacci grows geometrically with base $\phi \approx 1.618$. Binet's formula is the crown jewel of elementary recurrence solving.

## 7.5 Repeated Roots

C: If the characteristic equation has a root $r$ of [multiplicity] $m$, the corresponding solutions are $r^n, n r^n, n^2 r^n, \dots, n^{m-1} r^n$ (polynomial times geometric).

Q: Why do repeated roots introduce $n^k$ factors?
A: Because a repeated root means $r^n$ by itself doesn't span enough solutions to fix $k$ initial conditions. Supplementing with $n r^n, n^2 r^n, \dots$ restores linear independence — analogous to repeated roots in linear differential equations producing $x^k e^{rx}$ solutions.

P: Solve $a_n = 4 a_{n-1} - 4 a_{n-2}$ with $a_0 = 1, a_1 = 4$.
S:
**IDENTIFY**: Repeated-root case.

**PLAN**: Characteristic $r^2 - 4r + 4 = (r-2)^2 = 0$, so $r = 2$ with multiplicity $2$.

**EXECUTE**:
1. General solution: $a_n = (\alpha + \beta n) 2^n$.
2. $a_0 = \alpha = 1$.
3. $a_1 = (1 + \beta) \cdot 2 = 4 \Rightarrow \beta = 1$.
4. $a_n = (1 + n) 2^n$.

**EVALUATE**: Check $a_2 = 3 \cdot 4 = 12$; recurrence: $4 \cdot 4 - 4 \cdot 1 = 12$ ✓.

## 7.6 Nonhomogeneous Recurrences

C: A [nonhomogeneous] linear recurrence has form $a_n = c_1 a_{n-1} + \dots + c_k a_{n-k} + g(n)$; the general solution is $a_n = a_n^{(h)} + a_n^{(p)}$, a sum of the homogeneous solution and any particular solution.

Q: How do you find a particular solution $a_n^{(p)}$?
A: Guess a form based on $g(n)$. If $g(n)$ is polynomial, try polynomial of the same degree. If $g(n) = c \cdot s^n$ with $s$ NOT a characteristic root, try $A s^n$; if $s$ IS a root, try $A n s^n$ (or higher power). This [method of undetermined coefficients] resembles the ODE technique.

P: Solve $a_n = 3 a_{n-1} + 2^n$ with $a_0 = 1$.
S:
**IDENTIFY**: Nonhomogeneous, exponential forcing.

**PLAN**:
- Homogeneous: $a_n^{(h)} = C \cdot 3^n$.
- Particular: guess $a_n^{(p)} = A \cdot 2^n$ (since $2$ is NOT a root of $r - 3 = 0$).
- Solve for $A$, then apply initial condition.

**EXECUTE**:
1. Plug guess: $A \cdot 2^n = 3 A \cdot 2^{n-1} + 2^n \Rightarrow 2 A = 3 A + 2 \Rightarrow A = -2$.
2. General: $a_n = C \cdot 3^n - 2 \cdot 2^n = C \cdot 3^n - 2^{n+1}$.
3. $a_0 = C - 2 = 1 \Rightarrow C = 3$.
4. $a_n = 3^{n+1} - 2^{n+1}$.

**EVALUATE**: Verify $a_1 = 9 - 4 = 5$; recurrence: $3 \cdot 1 + 2 = 5$ ✓.

## 7.7 Generating Functions (Brief)

C: The [ordinary generating function] of a sequence $(a_n)$ is $A(x) = \sum_{n=0}^{\infty} a_n x^n$.

Q: How do generating functions help solve recurrences?
A: Multiply both sides of the recurrence by $x^n$ and sum over $n$. Standard manipulations turn the recurrence into an algebraic equation for $A(x)$. Solving for $A(x)$ and expanding as a power series recovers a closed form for $a_n$. Generating functions are especially powerful for nonlinear or non-constant-coefficient recurrences where characteristic equations fail.

## 7.8 Divide-and-Conquer Recurrences

C: A [divide-and-conquer recurrence] has the form $T(n) = a T(n/b) + f(n)$, with $a$ subproblems of size $n/b$ each and combining cost $f(n)$.

Q: What does the [Master Theorem] say (informally)?
A: $T(n) = a T(n/b) + f(n)$: compare $f(n)$ to $n^{\log_b a}$. (i) $f \ll n^{\log_b a}$: $T(n) = \Theta(n^{\log_b a})$. (ii) $f \asymp n^{\log_b a}$: $T(n) = \Theta(n^{\log_b a} \log n)$. (iii) $f \gg n^{\log_b a}$ (with a regularity condition): $T(n) = \Theta(f(n))$. The exponent $\log_b a$ is the [critical exponent] — it measures how fast the recursion tree grows.

Q: Apply the Master Theorem to mergesort: $T(n) = 2 T(n/2) + n$.
A: $a = 2, b = 2, f(n) = n$. Critical exponent $\log_2 2 = 1$. $f(n) = n = n^1$ matches the critical rate, so case (ii) applies: $T(n) = \Theta(n \log n)$. Mergesort's $O(n \log n)$ running time falls out in one line.

## 7.9 Choosing a Method

Q: When do you pick iteration vs. characteristic equation vs. generating functions?
A: Iteration: first-order recurrences or "guess and check" for simple patterns. Characteristic equation: linear constant-coefficient homogeneous/nonhomogeneous. Generating functions: nonlinear, variable coefficients, or when extracting an exact closed form matters (e.g., number-theoretic identities). For algorithm analysis, Master Theorem handles most divide-and-conquer cases directly.

## 7.10 Catalan Numbers

C: The [Catalan numbers] $C_n$ count many things — binary-tree shapes on $n$ nodes, balanced parenthesizations of $n$ pairs, triangulations of a convex $(n+2)$-gon. Formula: $C_n = \frac{1}{n+1} \binom{2n}{n}$ satisfies $C_{n+1} = \sum_{k=0}^{n} C_k C_{n-k}$.

Q: Why is the Catalan convolution recurrence surprising?
A: Because it's NONLINEAR (product of terms), so it doesn't yield to characteristic equations. Generating functions handle it: setting $C(x) = \sum C_n x^n$, the recurrence gives $C(x) = 1 + x \cdot C(x)^2$, a quadratic you can solve for $C(x)$. The closed form for $C_n$ comes from the binomial-series expansion.
