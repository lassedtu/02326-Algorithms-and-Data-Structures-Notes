# Running Time Analysis
> Determine how the running time (or other resource usage) of an algorithm grows as a function of the input size.

## Measuring Running Time

### Algorithm Breakdown
The running time of an algorithm depends on multiple factors:
- The number of primitive operations executed
- The speed of the computer executing the algorithm
- The quality of the compiler/interpreter

For analyzing algorithms, we focus on counting **primitive operations** (comparisons, assignments, arithmetic operations) rather than wall-clock time.

### Common Time Complexities

**Linear Time** - O(n)
- Iterates through array once
```c
for (int i = 0; i < n; i++) {
    // Constant time operation
    process(A[i]);
}
```
- Time grows proportionally with input size

**Quadratic Time** - O(n²)
- Nested loops iterating through array
```c
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        // Constant time operation
        process(A[i], A[j]);
    }
}
```
- Time grows with the square of input size

**Logarithmic Time** - O(log n)
- Problem size reduced by constant factor each step (e.g., binary search)
- Very efficient for large inputs

---

# Asymptotic Notation

> Use mathematical notation to describe the efficiency of algorithms independent of constant factors and lower-order terms.

## Big-O Notation (O)

### Definition & Intuition
Big-O notation provides an **upper bound** on the growth rate of a function.

**Formal Definition**: $f(n) = O(g(n))$ if there exist positive constants $c$ and $n_0$ such that:
$$f(n) \leq c \cdot g(n) \text{ for all } n \geq n_0$$

- Use Big-O to describe worst-case running time
- Examples:
	- $5n + 10 = O(n)$ (constant factors ignored)
	- $n^2 + 100n = O(n^2)$ (lower-order terms ignored)
	- $n = O(n^2)$ (linear is bounded by quadratic)

### Analysis
Big-O is the most commonly used notation in algorithm analysis because:
- **Worst-case guarantee**: Provides certainty that algorithm won't exceed this bound
- **Simplicity**: Ignores constant factors and lower-order terms that are implementation-dependent
- **Comparative analysis**: Makes it easy to compare algorithms at scale

---

## Big-Omega Notation (Ω)

### Definition & Intuition
Big-Omega notation provides a **lower bound** on the growth rate of a function.

**Formal Definition**: $f(n) = \Omega(g(n))$ if there exist positive constants $c$ and $n_0$ such that:
$$f(n) \geq c \cdot g(n) \text{ for all } n \geq n_0$$

- Use Big-Omega to describe best-case running time
- Examples:
	- $5n + 10 = \Omega(n)$ 
	- $n^2 + 100n = \Omega(n^2)$ 
	- $n^2 = \Omega(n)$ (quadratic grows faster than linear)

---

## Big-Theta Notation (Θ)

### Definition & Intuition
Big-Theta notation provides a **tight bound** on the growth rate - both upper and lower bounds are the same.

**Formal Definition**: $f(n) = \Theta(g(n))$ if $f(n) = O(g(n))$ and $f(n) = \Omega(g(n))$

Equivalently: there exist positive constants $c_1$, $c_2$, and $n_0$ such that:
$$c_1 \cdot g(n) \leq f(n) \leq c_2 \cdot g(n) \text{ for all } n \geq n_0$$

- Use Big-Theta when best-case and worst-case have the same growth rate
- Examples:
	- Merge sort: both best and worst case are $\Theta(n \log n)$
	- Linear search on random data: $\Theta(n)$ on average

### Analysis
- **Tightest description**: Provides the most precise asymptotic bound
- **Indicates balanced behavior**: Algorithm has similar performance across different inputs of the same size
- **Most useful for comparison**: When two algorithms have the same Big-Theta complexity, other factors determine which is better

---

# Growth Rate Hierarchy

The following functions are ordered by their growth rates (slowest to fastest):

$$\log n \ll n \ll n \log n \ll n^2 \ll n^3 \ll 2^n \ll n!$$

Key observations:
- **Logarithmic** functions grow much slower than any polynomial
- **Polynomial** functions grow much slower than exponential functions
- **Exponential** functions grow much faster than polynomial functions
- **Factorial** grows faster than exponential

Practical implications:
- An O(n²) algorithm can be millions of times slower than O(n) for large inputs
- An O(2^n) algorithm is only feasible for very small inputs (n < 20-30)
- An O(log n) algorithm can handle extremely large inputs efficiently

---

# Recurrence Relations

> Recursive algorithms are analyzed using recurrence relations that express running time in terms of smaller subproblems.

## Common Recurrence Patterns

### Pattern 1: Linear Recurrence (Divide in half, process one half)
$$T(n) = T(n/2) + O(n)$$
**Solution**: $\Theta(n)$

Example: Linear search with binary elimination

### Pattern 2: Divide and Conquer (Divide in half, process both halves, merge)
$$T(n) = 2T(n/2) + O(n)$$
**Solution**: $\Theta(n \log n)$

Example: Merge sort

### Pattern 3: Quadratic Recurrence (Process all pairs)
$$T(n) = nT(n-1) + O(n)$$
**Solution**: $\Theta(n!)$

Example: Generating all permutations

### Pattern 4: Linear Recurrence (Process next element)
$$T(n) = T(n-1) + O(1)$$
**Solution**: $\Theta(n)$

Example: Linear iteration through array

### Master Theorem (for $T(n) = aT(n/b) + f(n)$)
- If $f(n) = O(n^{\log_b a - \epsilon})$, then $T(n) = \Theta(n^{\log_b a})$
- If $f(n) = \Theta(n^{\log_b a})$, then $T(n) = \Theta(n^{\log_b a} \log n)$
- If $f(n) = \Omega(n^{\log_b a + \epsilon})$, then $T(n) = \Theta(f(n))$

---

# Experimental Analysis

> Verify theoretical complexity bounds by running the algorithm on inputs of increasing size and observing how running time scales.

## The Doubling Technique

### Algorithm Breakdown
1. Run algorithm on input of size $n_1$, measure time $T_1$
2. Run algorithm on input of size $n_2 = 2n_1$, measure time $T_2$
3. Compute ratio $r = T_2 / T_1$
4. Estimate complexity based on ratio:
	- If $r \approx 2$: algorithm is $O(n)$ (linear)
	- If $r \approx 4$: algorithm is $O(n^2)$ (quadratic)
	- If $r \approx 8$: algorithm is $O(n^3)$ (cubic)
	- If $r \approx 1$: algorithm is $O(\log n)$ (logarithmic)

### Example
Running a sorting algorithm:
- Size n=1000: 100 milliseconds
- Size n=2000: 410 milliseconds
- Ratio: 410/100 = 4.1 ≈ 4

**Conclusion**: The algorithm likely runs in $O(n^2)$ time (consistent with insertion sort or bubble sort)

### Analysis
- **Advantages**:
	- Validates theoretical analysis with real-world data
	- Reveals constant factors hidden by Big-O notation
	- Simple and practical to implement
	
- **Limitations**:
	- Results depend on implementation and hardware
	- May not be accurate for small input sizes
	- Cache effects and system factors can distort results
	- Expensive to run for very large inputs (O(n²) algorithms may be too slow)

---

# Properties of Asymptotic Notation

## Transitivity
If $f(n) = O(g(n))$ and $g(n) = O(h(n))$, then $f(n) = O(h(n))$

## Addition
If $f(n) = O(g(n))$ and $h(n) = O(g(n))$, then $f(n) + h(n) = O(g(n))$

This justifies focusing on the **dominant term** in an algorithm's complexity.

## Multiplication by Constants
For any constant $c > 0$:
- $c \cdot O(f(n)) = O(f(n))$

This explains why we ignore constant factors.

## Logarithm Base Equivalence
For any bases $a$ and $b > 1$:
$$\log_a n = \Theta(\log_b n)$$

All logarithms have the same asymptotic growth, so we typically write just $O(\log n)$ without specifying the base.

---

# Summary

Algorithm analysis focuses on understanding how running time scales with input size:

- **Big-O**: Upper bound, typically used for worst-case analysis
- **Big-Omega**: Lower bound, typically used for best-case analysis  
- **Big-Theta**: Tight bound, when best and worst cases coincide
- **Constant factors and lower-order terms**: Ignored in asymptotic analysis
- **Growth hierarchy**: logarithmic < polynomial < exponential
- **Recurrence relations**: Tool for analyzing recursive algorithms
- **Experimental verification**: Doubling technique confirms theoretical bounds
