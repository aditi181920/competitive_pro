**DFS TREE:**
---
-> Bacially the tree that we obtain on dfs traversal of a graph\


-> The bold edges are called span edges/ treee edges\
-> Other are all back edges
Observation 1. The back-edges of the graph all connect a vertex with its descendant in the spanning tree. This is why DFS tree is so useful.

**Finding bridges (or articulation points)**
--
-> a span-edge uv is a bridge if and only if there is no back-edge that "passes over" uv. A back edge is def never a bridge\
This gives rise to the classical bridge-finding algorithm. Given a graph G:
1. find the DFS tree of the graph;
2. for each span-edge uv, find out if there is a back-edge "passing over" uv, if there isn't, you have a bridge.
Can find this thing using dp on trees
dp[u] as the number of back-edges passing over the edge between u and its parent. 
dp[u]=(# of back-edges going up from u)−(# of back-edges going down from u)+∑dp[v](where v is a child of u.).
edge (u,p[v]) is a bridge iff dp[u]=0


**Directing edges to form a strongly connected component**
--

-> Given an undirected graph create a digraph such that the graph is SCC\
-> If G contain bridges then obviously it is impossible\
-> Otherwise direct all span edges down and all back edges up\

**CACTUS:**
--
-> A cactus is a graph where every edge (or sometimes, vertex) belongs to at most one simple cycle. The first case is called an edge cactus, the second case is a vertex cactus.\

-> You are given a connected vertex cactus with N vertices. Answer queries of the form "how many distinct simple paths exist from vertex p to vertex q?".\
-> Since atmost 1 simple cycle in a cactus...therefore there exists like 2 different paths through a cacuts ... so if we know the number of cactuses in the path from a root we can find it easily using lca.\
-> The main part about this problem is compressing cactus nodes... which is easy to be done using the concept of back edges


**BIPARTITE GRAPH:**
--

-> This problem we can remove only 1 edge to make a graph bipartite is it is not. Again use back edges:)


**DIRECETD GRAPH:**
--

-> Edges visited in dfs traversal are tree/span edges\
-> Edges going from child to its ancestor is back edge\
-> Edges going from some node to its descendant is forward edge\
-> Edge between two nodes such that none is ancestor or descendant is cross edge
