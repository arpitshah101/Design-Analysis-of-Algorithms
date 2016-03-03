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

DFS(G):
  for each *u* ∈ V
    _do_
      color[*u*] <-- white
      time <-- 0
      for each *u* ∈ V
        _do_
          if color[*u*] = white
          then DFS-visit(*u*)

DFS-visit(*u*):
  color[*u*] <-- Gray
  d[*u*] <-- time, time <-- time + 1
  for each *v* ∈ Adj[*u*]
    do
      if color[*v*] = white
      then DFS-visit(*v*)
  color[*v*] <-- Black
  f[*u*] <-- time, time <-- time + 1

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

Edge(u, v) ∈ E is a **tree edge** or **forward edge** iff d[u] < d[v] < f[v] < f[u]

Edge(u, v) ∈ E is a **back edge** iff d[v] < d[u] < f[u] < f[v]

Edge(u, v) ∈ E is **cross edge** iff d[v] < f[v] < d[u] < f[v]

**Diameter** of a graph = longest distance between two vertices.

Suppose G is connected and undirected.
The **diameter** of G is the longest possible path between a pair of vertices.

How do you find the diameter?
BFS from any vertex, pick the furthest leaf and BFS from there next.

## Topological Sort
Given a DAG (directed acyclic graph = graph with no cycle)

_**Lemma: **_ G is a DAG <==> there are no back edges in any DFS of G.

Given a DAG G = (V, E), a topological sort is a linear ordering of its vertices such that if (u, v) ∈ E, then *u* < *v*.
This can be viewed as ordering of its vertices along a line so that all directed edges go from left to right.

**Topological-Sort(G):**
1. Call DFS(G) to compute f[*v*] for each *v*
If ∃ a back edge, G is not a DAG. STOP.
2. Place the vertices on a horizontal line based on decreasing order of their f values.
3. Then all edges go from left to right.

## Connected Components
Assume G = (V, E) is a directed graph.
We define a relation on its vertices *u* --^--> *v* if *v* can be reached from *u* via a directed path.
We assume *u* --^--> *v*
The equivalence classes under this relation *u* --^--> *v* and *v* --^--> *u* are called strongly connected components.

_**Lemma: **_ Suppose *u*, *v* are in the same connected components.
Then any vertex along a path from *u* to *v* stays in the same component.

_**Theorem: **_ In any DFS, all vertices in the same strongly connected component are placed in the same DFS tree.

Assume we have done a DFS on G.
For each vertex *u* ∈ V, define forefather of *u*, Φ(*u*) to be the vertex *w* such that *u* --^--> *w* and f[*w*] is maximized.

_**Theorem: **_ Given *u* ∈ V and any DFS, Φ(*u*) is an ancestor of *u* (with regards to DFS)

_**Proof: **_ If DFS had visited any vertex in between *u* and Φ(*u*) and there is no path Φ(*u*) to *u*, then DFS would have finished Φ(*u*) before *u*.
