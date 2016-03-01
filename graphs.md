# Graph Algorithms

G = (V, E)
  V is set of vertices (a.k.a. nodes)
  E is set of edges.
    Edges can be two-way or one-way directed edges
  The number of nodes, n, is the cardinality of V.
    |V| = n

Types of graphs:
1. undirected --> edges go both ways
2. directed --> edges are directed (one way)
3. mixed --> some edges are directed while others go both ways

## Representation of Graphs
1. Adjacency Matrix
   * 2-dimentional array
   * Memory: O( |V| + |E| )

  adj(n) for each *u* ∈ *V* contains a pointer to all vertices *v* such that (*u*, *v*) ∈ E

## Breadth First Search (BFS)
Given G = (V, E), directed or undirected and as a distinguished vertex *S*, BFS explores all vertices that are neighbors at distance *z* and so on.

** BFS uses F.I.F.O.

## Depth First Search (DFS)
DFS explores most recently discovered vertex *v* that still has unexplored edges leaving it.
When all of its edges have been explored, it _back tracks_ to explore edges leaving the vertex from which *v* was discovered.

** DFS uses F.I.L.O.

## Color Scheme Organization for Traversal
* All nodes are white initially.
* A visited node/vertex will become gray.
* A node stays gray until we visit it again and it has no more neighbors to go to in which case we color it black.

We have 2 arrays corresponding to vertices to record timestamps or order.
d[v], f[v]
d[*v*] = first time *v* is discovered
f[*v*] = last time *v* is examined

### Parenthases Theorem
Suppose *u*, *v* are 2 different vertices.
[ d[*u*], f[*u*] ]
[ d[*v*], f[*v*] ]

One interval must be contained within the other or be separate. The two intervals cannot only _**partly**_ overlap.

## Types of edges
1. Tree Edges
  edges in DFS trees
2. Back Edges:
  an edge from descendant to an ancestor
3. Forward Edges:
  non-tree edges from ancestor to descendant
4. Cross Edges:
  All other edges
