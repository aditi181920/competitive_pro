**GRAPHS:**
--

**DEF:**
---
non empty set of vertices and possibly empty set of edges

**TERMS:**
---
**DEGREE:** Number of connections to particular edge in undirected graph\
**IN-DEGREE:** Number of incoming edges\
**OUT-DEGREE:** Number of outgoing edges\
**CONNECTED GRAPH:** Every node is reachable is reachable from every other node\
**COMPLETE GRAPH:** Every node has an edge to every other node\
**ACYCLIC:** Presence of no cycles\
**DIRECTED GRAPH:** Unidirectional edges\
**UNDIRECTED GRAPH:** Bidirectional edges

**PATHS AND CIRCUITS:**
---
**EULER PATH:** Visits every edge exactly once (for undirected graph: exists when connnected graph with zero or two vertices with odd degree in the graph, for directed graph: all vertices are in one strongly connected component (you can reach from one vertex to every other vertex of the graph) and in-degree is equal to out degree for each vertex else there exists one vertex with in-degree = out-degree-1 and one with in-degree=out-degree+1 and rest all have same in-degree's and out degrees)\
**EULER CIRCUIT:** Euler path with same starting and ending vertex (for undirected graph: exists when connected graph with all vertices with even degree,  for directed graph: all vertices are in one strongly connected component (you can reach from one vertex to every other vertex of the graph) and in-degree is equal to out degree for each vertex)\
**HAMILTONIAN PATH:** Visits every vertex exactly once\
**HAMILTONIAN CIRCIUT:** Hamiltonian path with same starting and ending vertex
