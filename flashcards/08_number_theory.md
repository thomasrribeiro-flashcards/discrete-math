+++
order = 8
subject = "mathematics"
tags = ["math", "discrete-math", "number-theory", "gcd", "euclidean-algorithm", "modular-arithmetic", "crt"]
+++

# Discrete Math — Number Theory

## 8.1 Why Number Theory in a Discrete Math Course?

Q: Why is number theory part of a discrete math curriculum for CS?
A: Because modular arithmetic is the mathematical foundation of cryptography (RSA, Diffie–Hellman, elliptic curves), hashing, error-correcting codes, and pseudo-random generators. Without number theory, none of modern public-key crypto or data integrity works.

## 8.2 Divisibility

C: For integers $a, b$ with $a \neq 0$, $a$ [divides] $b$ (written $a \mid b$) iff $\exists k \in \mathbb{Z}\, (b = ak)$.

Q: Why is the divisibility relation transitive on $\mathbb{Z}$?
A: If $a \mid b$ and $b \mid c$, then $b = ak_1$ and $c = bk_2 = a(k_1 k_2)$, so $a \mid c$. Transitivity follows from the ring structure of $\mathbb{Z}$ — composition of scalings stays a scaling.

## 8.3 The Division Algorithm

C: [Division algorithm]: for any integers $a, b$ with $b > 0$, there exist UNIQUE integers $q$ (quotient) and $r$ (remainder) such that $a = bq + r$ and $0 \leq r < b$.

Q: Why is the division algorithm a theorem, not a definition?
A: Because the existence and uniqueness of $(q, r)$ require proof — the well-ordering principle applied to $\{a - bq : q \in \mathbb{Z}, a - bq \geq 0\}$ gives existence (pick $q$ minimizing this set's element $r$), and uniqueness follows by a short contradiction argument. It's the foundation of every subsequent division-based theorem.

## 8.4 GCD and Bézout

C: The [greatest common divisor] $\gcd(a, b)$ is the largest positive integer dividing both $a$ and $b$ (with $\gcd(0, 0)$ undefined).

Q: What is $\gcd(48, 36)$?
A: $12$. Divisors of $48$: $\{1, 2, 3, 4, 6, 8, 12, 16, 24, 48\}$; of $36$: $\{1, 2, 3, 4, 6, 9, 12, 18, 36\}$. Intersection's max is $12$. For larger numbers, use the Euclidean algorithm instead of enumeration.

C: [Bézout's identity]: for integers $a, b$ not both zero, there exist integers $x, y$ with $\gcd(a, b) = a x + b y$.

Q: Why is Bézout's identity so central?
A: Because it says the gcd is the SMALLEST positive integer expressible as an integer linear combination of $a$ and $b$. This single fact implies: (i) divisibility properties of gcd, (ii) existence of modular inverses, (iii) the structure of ideals in $\mathbb{Z}$, (iv) the validity of RSA decryption.

## 8.5 The Euclidean Algorithm

C: The [Euclidean algorithm] computes $\gcd(a, b)$ by iteratively replacing $(a, b)$ with $(b, a \bmod b)$ until the second term is $0$; the first term is then the gcd.

Q: Why does the Euclidean algorithm work?
A: Because $\gcd(a, b) = \gcd(b, a \bmod b)$: any common divisor of $a, b$ divides $a \bmod b = a - qb$, and conversely. Each step strictly decreases the second argument (guaranteeing termination) while preserving the gcd.

P: Compute $\gcd(1071, 462)$ using the Euclidean algorithm.
S:
**IDENTIFY**: Apply the algorithm.

**PLAN**: Iterate the $\bmod$ step until one term is $0$.

**EXECUTE**:
1. $1071 = 2 \cdot 462 + 147$.
2. $462 = 3 \cdot 147 + 21$.
3. $147 = 7 \cdot 21 + 0$.

$\gcd(1071, 462) = 21$.

**EVALUATE**: Three steps — the algorithm's running time is $O(\log \min(a, b))$ (Lamé's theorem). Scales to 1000-digit numbers effortlessly, which is why cryptography relies on it.

## 8.6 Extended Euclidean Algorithm

C: The [extended Euclidean algorithm] finds $\gcd(a, b)$ AND integers $x, y$ with $ax + by = \gcd(a, b)$ by back-substituting through the Euclidean steps.

Q: Why do we need the extended version?
A: Because many applications need the coefficients $x, y$, not just the gcd — particularly modular inverses: to invert $a$ mod $m$, find $x$ with $ax + my = 1$; then $x \equiv a^{-1} \pmod m$. Standard ingredient in RSA key generation.

## 8.7 Congruences (Review)

C: [Congruence modulo $n$]: $a \equiv b \pmod n$ iff $n \mid (a - b)$.

Q: Why is working in $\mathbb{Z}/n\mathbb{Z}$ the natural setting for modular arithmetic?
A: Because $\equiv \pmod n$ is an equivalence relation whose equivalence classes form a quotient set $\mathbb{Z}/n\mathbb{Z} = \{[0], [1], \dots, [n-1]\}$ with well-defined addition and multiplication inherited from $\mathbb{Z}$. Reducing mod $n$ is then computing in this $n$-element "ring."

Q: Under what condition does $a$ have a multiplicative inverse mod $n$?
A: Iff $\gcd(a, n) = 1$ (i.e., $a$ and $n$ are coprime). Proof: if coprime, Bézout gives $ax + ny = 1$, so $ax \equiv 1 \pmod n$; conversely, if $ax \equiv 1$, then $ax - 1 = kn$, so any common divisor of $a$ and $n$ divides $1$.

## 8.8 Fermat's Little Theorem

C: [Fermat's little theorem]: if $p$ is prime and $\gcd(a, p) = 1$, then $a^{p-1} \equiv 1 \pmod p$.

Q: Why does Fermat's little theorem hold?
A: Because multiplication by $a$ is a bijection on $\{1, 2, \dots, p-1\}$ mod $p$ (inverse exists by Bézout). So $\{a, 2a, \dots, (p-1)a\} \equiv \{1, 2, \dots, p-1\} \pmod p$ as sets. Multiplying both sides gives $a^{p-1} (p-1)! \equiv (p-1)! \pmod p$, and cancelling $(p-1)!$ (invertible) gives the theorem.

Q: How is Fermat's theorem used in primality testing?
A: If $a^{n-1} \not\equiv 1 \pmod n$ for some $a$ coprime to $n$, then $n$ is composite (contrapositive of Fermat). Quick to check for random $a$; often proves compositeness in one step. Miller–Rabin is a refined version that handles "Fermat liars."

## 8.9 Euler's Theorem and the Totient

C: [Euler's theorem]: if $\gcd(a, n) = 1$, then $a^{\varphi(n)} \equiv 1 \pmod n$, where $\varphi(n)$ is Euler's totient.

Q: How does Euler's theorem generalize Fermat's?
A: When $n = p$ is prime, $\varphi(p) = p - 1$, so Euler's becomes Fermat's. Euler's extends to composite moduli, which is essential for RSA (modulus is a product of two primes).

Q: What does Euler's theorem imply for RSA?
A: If $n = pq$ and $\gcd(m, n) = 1$, then $m^{\varphi(n)} \equiv 1 \pmod n$ with $\varphi(n) = (p-1)(q-1)$. Choosing $e, d$ with $ed \equiv 1 \pmod{\varphi(n)}$ ensures $(m^e)^d = m^{ed} = m^{1 + k\varphi(n)} \equiv m \pmod n$ — decryption reverses encryption. The whole RSA protocol hinges on this.

## 8.10 The Chinese Remainder Theorem

C: [Chinese Remainder Theorem (CRT)]: if $m_1, m_2, \dots, m_k$ are pairwise coprime and $a_1, a_2, \dots, a_k$ are any integers, there exists a unique $x \pmod{m_1 m_2 \cdots m_k}$ satisfying $x \equiv a_i \pmod{m_i}$ for all $i$.

Q: What's the intuition behind CRT?
A: That congruences modulo coprime moduli are "independent" — knowing $x \bmod m_i$ for each $i$ pins down $x$ modulo the product $m_1 \cdots m_k$ uniquely. The map $\mathbb{Z}/(m_1 m_2) \to \mathbb{Z}/m_1 \times \mathbb{Z}/m_2$ is a bijection when moduli are coprime, and ring-structured.

P: Find $x$ with $x \equiv 2 \pmod 3$, $x \equiv 3 \pmod 5$, $x \equiv 2 \pmod 7$.
S:
**IDENTIFY**: Classic CRT problem, three coprime moduli.

**PLAN**: Use constructive CRT: $M = 3 \cdot 5 \cdot 7 = 105$; $M_i = M/m_i$; invert $M_i$ mod $m_i$; combine.

**EXECUTE**:
1. $M_1 = 35$; $35 \equiv 2 \pmod 3$; inverse $2^{-1} \equiv 2 \pmod 3$; contribution $2 \cdot 35 \cdot 2 = 140$.
2. $M_2 = 21$; $21 \equiv 1 \pmod 5$; inverse $1$; contribution $3 \cdot 21 \cdot 1 = 63$.
3. $M_3 = 15$; $15 \equiv 1 \pmod 7$; inverse $1$; contribution $2 \cdot 15 \cdot 1 = 30$.
4. $x \equiv 140 + 63 + 30 = 233 \equiv 23 \pmod{105}$.

**EVALUATE**: Check: $23 = 7 \cdot 3 + 2$ ($\equiv 2 \pmod 3$); $23 = 4 \cdot 5 + 3$ ($\equiv 3 \pmod 5$); $23 = 3 \cdot 7 + 2$ ($\equiv 2 \pmod 7$). All three satisfied. CRT appears whenever you want parallel modular computation (e.g., accelerating RSA decryption by working mod $p$ and mod $q$ separately).

## 8.11 Primes and the Fundamental Theorem

C: [Fundamental theorem of arithmetic]: every integer $n > 1$ factors UNIQUELY (up to ordering) as a product of primes.

Q: Why is unique factorization nontrivial?
A: Because it fails in some number systems! In $\mathbb{Z}[\sqrt{-5}]$, $6 = 2 \cdot 3 = (1 + \sqrt{-5})(1 - \sqrt{-5})$ is two distinct factorizations into irreducibles. For $\mathbb{Z}$, uniqueness follows from Euclid's lemma ($p \mid ab \Rightarrow p \mid a$ or $p \mid b$), which itself uses Bézout.

Q: Why are there infinitely many primes?
A: Euclid's proof: if $p_1, \dots, p_n$ were all primes, then $N = p_1 p_2 \cdots p_n + 1$ is not divisible by any $p_i$ (remainder $1$), so $N$ has a prime factor not in our list — contradiction. An infinite supply of primes is the bedrock of cryptography.

## 8.12 Modular Exponentiation

Q: How do you compute $a^b \bmod n$ efficiently?
A: [Repeated squaring]: represent $b$ in binary $b = b_{k-1} \dots b_1 b_0$; compute $a, a^2, a^4, \dots, a^{2^{k-1}}$ mod $n$ by squaring; multiply together those $a^{2^i}$ where $b_i = 1$. Cost: $O(\log b)$ modular multiplications. Making RSA practical for $2048$-bit keys.

P: Compute $7^{13} \bmod 11$ using repeated squaring.
S:
**IDENTIFY**: Modular exponentiation.

**PLAN**: $13 = 1101_2$; squares $7, 7^2, 7^4, 7^8$ mod $11$.

**EXECUTE**:
- $7^1 \equiv 7$.
- $7^2 = 49 \equiv 5$.
- $7^4 = 5^2 = 25 \equiv 3$.
- $7^8 = 3^2 = 9$.
- $13 = 8 + 4 + 1$: $7^{13} = 7^8 \cdot 7^4 \cdot 7^1 \equiv 9 \cdot 3 \cdot 7 = 189 \equiv 189 - 17 \cdot 11 = 189 - 187 = 2 \pmod{11}$.

**EVALUATE**: $7^{13} \equiv 2 \pmod{11}$. Sanity check via Fermat: $7^{10} \equiv 1$, so $7^{13} \equiv 7^3 = 343 = 31 \cdot 11 + 2 \equiv 2$ ✓.
