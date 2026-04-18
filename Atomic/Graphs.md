## What is a Graph?
A graph is a mathematical and algorithmic model for representing relationships between objects. We write a graph as $G=(V,E)$, where $V$ is the set of vertices (or nodes) and $E$ is the set of edges connecting pairs of vertices. In other words, vertices represent entities and edges represent how those entities are related.

Graphs are useful whenever the structure of connections matters more than the objects in isolation. Typical examples include cities connected by roads, users connected in social networks, web pages connected by links, and tasks connected by prerequisite constraints.

## Main Types of Graphs
The same graph concept appears in several variants depending on what kind of relationships we need to model.

An [[Undirected Graph]] has edges without direction, so a connection between $u$ and $v$ can be traversed both ways. A [[Directed Graph (Digraph)]] has directed edges, so $(u,v)$ and $(v,u)$ are different relationships. A [[Weighted Graph]] assigns each edge a numerical value such as distance, cost, or time. In an [[Unweighted Graph]], all edges are treated equally, so only connectivity matters.

## Common Terminology
Two vertices are adjacent if an edge exists between them. In an undirected graph, the degree of a vertex is the number of incident edges. In a directed graph, in-degree counts incoming edges and out-degree counts outgoing edges.

A path is a sequence of vertices where consecutive vertices are connected by edges. A cycle is a path that starts and ends at the same vertex without repeating edges. An undirected graph is connected if every pair of vertices has a path between them.

## How Graphs Are Represented
Two standard representations are used in algorithms: adjacency lists and adjacency matrices.

An adjacency list stores, for each vertex, the set or list of its neighbors. It is memory-efficient for sparse graphs and uses $O(|V|+|E|)$ space. This is often the preferred representation for traversal algorithms such as BFS and DFS.

An adjacency matrix stores edge information in a $|V|\times|V|$ table, where entry $(i,j)$ indicates whether (or with what weight) an edge from $i$ to $j$ exists. It supports constant-time edge lookup but uses $O(|V|^2)$ space, so it is usually better for dense graphs.

## Why Graphs Matter in Algorithms
Many important algorithmic problems are naturally graph problems. Reachability and traversal are handled by BFS and DFS, shortest-path problems model routing and navigation, connectivity problems capture component structure, and DAG-based models are used for dependency scheduling and ordering tasks.

Because so many structures can be encoded as graphs, mastering graph representations and terminology is a foundation for understanding advanced algorithms.

## Related
- [[Undirected Graph]]
- [[Directed Graph (Digraph)]]
- [[Unweighted Graph]]
- [[Weighted Graph]]
- [[Minimum Spanning Tree (MST)]]
- [[Searching Algorithms]]
