**SPANNING TREE:**
---

-> In a weighted undirected graph, a spanning tree is such a subset of the given graph such that it contains all the vertices \
-> A spanning tree is not necessarily unique\
-> An undirected connected graph always has atleast 1 spanning tree

**MINIMUM SPANNING TREE:**
---

-> Minimum spanning tree is a spanning tree such that is has the minimum sum of its edge weights

**1. PROPERTIES OF MINIMUM SPANNING TREE:**
---

-> It is unique if weight of all edges are different. Otherwise may not necessarily\
-> Min spanning tree = min. product spanning tree (if weights are all positive ; also if non-distinct positive weights then the spanning trees may be diff but values will be same)
(this can be proved as : if we take the log of edge weights then the sum of min sum spanning tree will be the value of corresponding product spanning tree and since log is monotonic like sums of positive value it will also be min product spanning tree)\
-> In min spanning tree, the max. weight of an edge is minimized [this follows validity of Kruskal's algorithm]\
-> The max. spanning tree of a graph can be obtained by changing the signs of all the weights to opposite and then applying any MST algorithm
