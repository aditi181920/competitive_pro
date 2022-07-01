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
**UNDIRECTED GRAPH:** Bidirectional edges\
**CONNECTED COMPONENTS:** When u can reach from one vertex to every other vertex in an undirected graph then it is said to be one connected component\
**STRONGLY CONNECTED COMPONENTS:** For directed graph, every vertex reachable from every other\
**WEEKLY CONNECTED COMPONENT:** For directed graph, every vertex connected in a component but not every vertex is reachable from every other\
**BRIDGES:** Edge of a graph whose deletion increases the number of components

**PATHS AND CIRCUITS:**
---

**EULER PATH:**
                
    Visits every edge exactly once 
    --> existence: 
    ----> for undirected graph:
    1. connnected graph
    2. zero or two vertices with odd degree in the graph
    ----> for directed graph:
    1. all vertices are in one strongly connected component (you can reach from one vertex to every other vertex of the graph) 
    2. in-degree = out-degree for each vertex or there exists one vertex with in-degree = out-degree-1 and one with 
    in-degree=out-degree+1 and rest all have same in-degree's and out degrees
    
**EULER CIRCUIT:** 

    Euler path with same starting and ending vertex
    --> existence:
    ----> for undirected graph:
    1. connected graph
    2. all vertices with even degree
    ----> for directed graph:
    1. all vertices are in one strongly connected component (you can reach from one vertex to every other vertex of the graph)
    2. in-degree is = out-degree for each vertex
    
**HAMILTONIAN PATH:** Visits every vertex exactly once\
**HAMILTONIAN CIRCIUT:** Hamiltonian path with same starting and ending vertex


**HANDSHAKING THEOREM:**
---
-> if there are n vertices vertices V1,....,Vm with degrees d1,d2,...,dn and there are e edges, then -- d1+d2+d3+....+dn = 2e\
-> called handshaking becoz we can state it as if n people shake hands, and the ith person shakes hands d1 times, then the total number of handshakes that take place is (d1+d2+....+dn-1+dn)/2\
-> A consequence result of this theorem is :\
-> (d1+d2+d3....+dn) must be even => every graph has an even of odd vertices


**FUNCTIONAL GRAPH:**
--
-> Graphs having all vertices with outdegree 1 are functional graphs. One of the most useful property is that every component has only 1 cycle.

**PERMUTATION GRAPH:**
--
-> Graphs with vertices - elements of vertices, and edges - represent inversions in permutation
![image](https://user-images.githubusercontent.com/94597499/176885147-3a9efb7f-5045-4cde-9131-fd38dd30f287.png)

