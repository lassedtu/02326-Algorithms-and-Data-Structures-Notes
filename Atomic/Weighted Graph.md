In a weighted graph $G$, each edge $e$ has an associated weight $w(e)$ that represents some measurable quantity of the connection between its two vertices. Depending on the problem, this weight can model distance, cost, time, capacity, or risk. The weights make the graph more informative than an unweighted graph, because algorithms can then optimize for total weight, such as finding the shortest path or the minimum-cost way to connect all vertices.

![[weighted-graph.png]]

## Representation of a Weighted Graph
A weighted graph can be represented using the same core structures as unweighted or directed graphs, but each stored edge also includes a weight value. The two most common representations are an adjacency matrix and an adjacency list. Both represent the same graph, but they differ in memory usage and which operations are fast.

![[weighted-graph-1.png]]
### Adjacency Matrix
An adjacency matrix is a $V \times V$ table where rows and columns correspond to vertices. The entry at row $i$, column $j$ stores the weight of the edge between vertices $i$ and $j$. If no edge exists, the entry is typically set to $0$ (or sometimes $\infty$, depending on convention). For an undirected weighted graph, the matrix is symmetric, so $M[i][j] = M[j][i]$.

This representation is useful when you need very fast edge lookups, since checking whether an edge exists (and getting its weight) is $O(1)$. The trade-off is memory: the matrix uses $O(V^2)$ space even when the graph is sparse.

|       | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- |
| **0** | 0   | 6   | 8   | 2   | 0   | 0   | 0   | 0   |
| **1** | 6   | 0   | 3   | 0   | 4   | 0   | 0   | 0   |
| **2** | 8   | 3   | 0   | 4   | 2   | 6   | 0   | 0   |
| **3** | 2   | 0   | 4   | 0   | 0   | 0   | 7   | 0   |
| **4** | 0   | 4   | 2   | 0   | 0   | 1   | 0   | 1   |
| **5** | 0   | 0   | 6   | 0   | 1   | 0   | 2   | 7   |
| **6** | 0   | 0   | 0   | 7   | 0   | 2   | 0   | 5   |
| **7** | 0   | 0   | 0   | 0   | 1   | 7   | 5   | 0   |

### Adjacency List
An adjacency list stores, for each vertex, a list of its neighboring vertices together with edge weights. For example, if vertex $u$ is connected to $v$ with weight $w$, then the list for $u$ contains an entry like $(v, w)$. In an undirected graph, each edge appears in two lists: once for each endpoint.

This representation is usually preferred for sparse graphs, because it uses $O(V + E)$ space and allows efficient traversal of neighbors. Many graph algorithms, including Prim's algorithm (with a priority queue) and Dijkstra's algorithm, are commonly implemented with adjacency lists for this reason.

![[adjecency-list.png]]