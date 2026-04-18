
Growth rate hierarchy ranks common complexity classes by how fast they grow as $n \to \infty$.

---

## Natural Explanation

When input size gets very large, some algorithms scale gently (like logarithmic), while others explode (like exponential or factorial). The hierarchy is a way to compare this long-run behavior.

If $f(n)$ is lower in the hierarchy than $g(n)$, then eventually $f(n)$ is much smaller than $g(n)$, and algorithms with runtime $f(n)$ are typically more scalable.

---

## Academic View

A standard way to state strict asymptotic separation is:

$$
f(n) = o(g(n)) \iff \lim_{n \to \infty} \frac{f(n)}{g(n)} = 0.
$$

So when we write one class below another in the hierarchy, we usually mean the lower function is little-o of the higher one.

---

## Common Hierarchy (Small to Large)

For sufficiently large $n$:

$$
1 \prec \log\log n \prec \log n \prec (\log n)^k \prec n^\varepsilon \prec n \prec n\log n \prec n^2 \prec n^3 \prec n^k \prec c^n \prec n! \prec n^n
$$

Typical assumptions:
- $k > 1$ is a constant.
- $0 < \varepsilon < 1$ is a constant.
- $c > 1$ is a constant.

Read this left to right as increasing growth.

![[big-o-complexity.jpg]]

---

## Useful Pairwise Facts

- $\log n = o(n^\varepsilon)$ for every constant $\varepsilon > 0$.
- $n^a = o(n^b)$ when $0 < a < b$.
- Any polynomial is asymptotically smaller than any exponential with base $> 1$:
  $$
  n^k = o(c^n).
  $$
- Exponential is asymptotically smaller than factorial:
  $$
  c^n = o(n!).
  $$

---

## Why This Matters in Algorithms

- It helps compare algorithms without machine-dependent constants.
- It highlights which designs remain practical as data grows.
- It explains why an $O(n\log n)$ algorithm is preferred over $O(n^2)$ for large inputs.

---

## Common Pitfalls

- Comparing runtimes only for small $n$ and drawing asymptotic conclusions.
- Forgetting that constants and lower-order terms can matter in practice for moderate input sizes.
- Treating classes as equal when one is only an upper bound and not tight.

---

## Related

- [[Atomic/Big-O, Big-Omega, Big-Theta]]
- [[Lectures/Week 4]]
