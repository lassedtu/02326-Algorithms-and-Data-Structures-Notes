## What is a Tree?
A tree is a special type of graph. It consists of nodes (or vertices) connected by edges, and it satisfies two key structural properties:

- The graph is connected.
- The graph is acyclic (it contains no cycles).

Because of these properties, there is exactly one simple path between any two vertices in a tree.

![[tree-example.png | 300]]

## Rooted Trees
A rooted tree is a tree where one vertex is chosen as the **root**. This gives the tree a hierarchical structure, where relationships are viewed relative to the root.

In other words, a rooted tree is:
- A connected and acyclic graph
- With a designated root node

## Terminology
Given a rooted tree:

- **Parent**: If a node $u$ is directly above node $v$, then $u$ is the parent of $v$.
- **Child**: If $u$ is the parent of $v$, then $v$ is a child of $u$.
- **Ancestor**: Any node on the path from a node to the root (including parent, grandparent, etc.).
- **Descendant**: Any node in the subtree below a node.
- **Leaf**: A node with no children.
- **Internal node**: A node with at least one child.
- **Path**: A sequence of nodes where consecutive nodes are connected by edges.

These concepts let us reason about tree structure as a hierarchy instead of just a generic graph.

## Depth and Height
For a rooted tree, depth and height are defined using path lengths (number of edges):

- **Depth of a node $v$**: length of the path from $v$ to the root.
- **Height of a node $v$**: length of the longest path from $v$ down to a descendant leaf.

For the whole tree $T$:

- **Depth of $T$** = **Height of $T$** = length of the longest path from the root to a leaf.

## Binary Tree
A binary tree is a rooted tree with an additional constraint:

- Each node has at most two children.
- These children are called the **left child** and **right child**.

Binary trees are one of the most important tree classes in algorithms and data structures.

![[binary-tree-example.png | 400]]
## Complete and Almost Complete Binary Trees
### Complete Binary Tree
A complete binary tree is a binary tree where all levels are full.

### Almost Complete Binary Tree
An almost complete binary tree is a complete binary tree with $0$ or more rightmost leaves deleted.

## Related
- [[Graphs]]
- [[Minimum Spanning Tree (MST)]]
