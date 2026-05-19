# Shortest Paths

## What are Shortest Paths?
Given a directed, weighted graph $G=(V,E)$ and a source vertex $s$, the **shortest path problem** aims to find the path with the minimum total weight (or length) from $s$ to all other vertices in $G$.

The weight of a path is the sum of the weights of its constituent edges.

### Shortest Path Tree
The collection of all shortest paths from a single source $s$ to all other reachable vertices forms a **shortest path tree**. This tree is rooted at $s$, and every path from $s$ to any other vertex $v$ in the tree is a shortest path in $G$.

### Assumptions
For simplicity, when discussing shortest path algorithms, we often assume:
- All vertices are reachable from the source vertex $s$.
- Consequently, a shortest path to each vertex always exists.

### Subpath Property
Any subpath of a shortest path is itself a shortest path.

**Proof:**
Consider a shortest path $P$ from $s$ to $t$. Let $P$ be composed of three segments: $P_1$ from $s$ to $u$, $P_2$ from $u$ to $v$, and $P_3$ from $v$ to $t$. So, $P = P_1 \to P_2 \to P_3$.
Assume, for contradiction, that $P_2$ is not a shortest path from $u$ to $v$. This means there exists a shorter path, say $Q_2$, from $u$ to $v$.
If we replace $P_2$ with $Q_2$ in the original path $P$, we would form a new path $P' = P_1 \to Q_2 \to P_3$.
The total weight of $P'$ would be $w(P_1) + w(Q_2) + w(P_3)$. Since $w(Q_2) < w(P_2)$, it follows that $w(P') < w(P)$.
This contradicts our initial assumption that $P$ was a shortest path from $s$ to $t$. Therefore, $P_2$ must be a shortest path from $u$ to $v$. This logic applies to any subpath.

## Types of Shortest Path Problems
Shortest path problems can be categorized based on various factors:

| Category | Description |
| --- | --- |
| **Source/Target** | Single source (to all others), Single source-single target, All-pairs (between all pairs of vertices) |
| **Edge Weights** | Non-negative, Arbitrary (can be negative), Euclidean distances |
| **Cycles** | No cycles (DAGs), No negative cycles (general graphs), Cycles allowed (but no negative cycles for most algorithms) |

## Related
- [[Graphs]]
- [[Dijkstra's Algorithm]]
- [[Shortest Paths on DAGS]]