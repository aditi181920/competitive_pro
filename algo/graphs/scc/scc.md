**STRONGLY CONNECTED COMPONENTS:**
--

-> These don't intersect=> they are a partition of provided vertices\
-> Condensation graph: contains all SCC as one vertex . There is an edge b/w Ci and Cj of condensation graph if and only if there exists some edge (u,v) such that u belongs to Ci and v belongs to Cj\
-> Condensation graoh is always acyclic. 
  
**Theorem:**
--

-> Let C and C' are 2 different strongly connected components and there is an edge (c,c') in the condensation graph between these two components. Then tout [c]>tout[c']

**Kosaraju's algo for finding SCC:**
--

-> Do a dfs, keep track of exit times\
-> Sort vertices in decreasing order of exit times\
-> reverse the edges and construct a reverse graph\
-> Now dfs on this reverse graph in the order of obtained exit array\
-> The components we recieve here are strongly connected \

**Proof:**
--
 One proof for this algo can be\
 -> Since we topsorted the vertices, the vertex from which we start the second dfs is always visited first and all other vertices are always reachable from this\
 -> Now we need to check reverse reachability, so we use reverse graph, whosoever vertices now are reachable (they were also reachable in normal graph). So these form SCC
 
 
 **Constructing condensation graph:**
 --
 
 -> After creating connected component, find some vertex in each component, to represent that component.\
 -> Then we connect SCC nodes if there exists some edge between any nodes of these SCC.
