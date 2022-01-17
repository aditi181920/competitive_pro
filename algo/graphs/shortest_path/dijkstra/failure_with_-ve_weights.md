**DIJKSHTRA ALGORITHM ACTUALLY FAILS ON GRAPHS HAVING NEGATIVE EDGE WEIGHTS:**
---

**REASONING [MY UNDERSTANDING]:**
---
-> Since in dijkstra we are popping out vertices on sorted order let's say some vertex having negative egde has not been relaxed yet \
-> let x-> y be this edge then lets say y was already marked by finding smallest path through some positive edges from source \
-> **PROBLEM 1**: but due to negative weight x->y it will have to be visited again and then it will defy the prop of dijkstra and behave somewhat like ford in case of directed edges and may enter in an infinte loop in case of undirected edges (if we don't keep check of marked vertices)\
-> **PROBELM 2**: if we keep a check of marked vertices then dijkstra will definitely give wrong answer if we already mark y then encounter x 

-> maybe some other problems are also there ....\
-> anyways dijkstra must never be used in case of negative edges / negative weight cycle
