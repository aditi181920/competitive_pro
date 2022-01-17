**FLOYD WARSHALL:**
--

-> apsp\
-> directed/undirected graph find shortest path dij between each pair of vertices i and j\
-> The graph may have negative weight edges(only in directed graph) but no negative weight cycles [shortest path becomes undefined as path keeps reducing in every cycle and becomes arbitrarily small]\
-> the above statement automatically means that an undirected graph cannot have any negative weight edges as that single edge alone forms a negative weight cycle and u can move back and forth along that edge as long as you like\
-> this algo can be used to detect the presence of negative cycles\
-> the graph has a negative cycle if at the end of the algo, the distance from a vertex v to itself is negative

**ALGO:**
---

-> d[][]: matrix of distances\
-> d[i][j] = shortest distance between i to j such that only [1 ... k]  nodes can be included as internal nodes where k is the last phase executed \
-> So before the kth phase internal nodes are restricted to be smaller than k (beginning and end have no such restriction)
-> dp state and transitions:
```cpp
   BASE CASES:  d[i][j] = wij if edges exists between i and j else infinity in 0th phase
   TRANSITION: d[i][j] = min(d[i][j], d[i][k]+d[k][j])
   k=[0....n]
```
-> In each kth phase we have to iterate over all pairs of vertices and recalculate the length of the shortest path between them\
-> After nth phase, d[i][j] contains length of the shortest path between i and j and infinity if path does not exist

**COMPLEXITY:**
---
**O(n^3)**\
-> this is quite effective for dense graph but for sparse graph Johnshon's algo is much more effective

**IMPLEMENTATION:**
---
```cpp
//intialize with base values.....

for (int k = 0; k < n; ++k) {
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (d[i][k] < INF && d[k][j] < INF)        //to avoid computations of inf-1,inf-2,inf-3 so goes on...
                d[i][j] = min(d[i][j], d[i][k] + d[k][j]); 
        }
    }
}
```
**RETRIEVING THE SEQ OF VERTICES IN THE SHORTEST PATH:**
---
-> p[][]: number of the phase where the shortest distance between any two given vertices was last modified which is nothing but just the vertex coming in between somewhere in the shortest path from i and j \
-> therefore to find path i->j we need to find i->p[i][j] and p[i][j]->j \
-> we can construct this process recursively

**THE CASE OF REAL WEIGHTS:**
---
-> real numbers lead to some errors while computation always\
-> Floyd-Warshall algo accumulates errors very quickly ... if delta error in the first place, then this error may propagate to the second iteration as 2delta then to 3rd iteration as 4delta and so on.\
-> to avoid this:
```sh
if (d[i][k] + d[k][j] < d[i][j] - EPS)
    d[i][j] = d[i][k] + d[k][j]; 
```

**THE CASE OF NEGATIVE CYCLES:**
---
-> For all pairs of vertices i and j for which there does not exist a path starting at i, visiting a negative cycle, and end at j, the algorithm will still work correctly\
-> for the pair of vertices for which answer does not exist (due to presence of a negative cycle in path between them) then d[i][j]<0\
-> be careful of integer overflows as it can go beyond some -inf... better to limit min dist by some defined -inf


