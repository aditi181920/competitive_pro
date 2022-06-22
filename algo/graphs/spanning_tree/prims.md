**PRIMS ALGORITHM:**
--

-> Given n vertices and m edges\
-> choose arbitrary vertex\
-> Select min weight edge from this vertex and add to tree\
-> Similarly for every iteration we pick an edge with minimal weight that connects one selected vertex and one unselected vertex

**PROOF:**
--

-> Say S is a min spanning tree and T is a spanning tree created by our algo\
-> At some point our algo selected an edge e with ends a and b which is not part of S\
-> In our min spanning tree these 2 vertices must then be connected by some vertex f whose one end lies in selected vertices and the other end does not\
-> Our algo choose f over e => e is less or eq to f\
-> Resulting spanning tree cannot have a larger total weight since e was not larger than f.\
-> Also since S is min spanning tree it cannot be smaller\
-> This implies that e=f \
-> So prims algo choose the optimal edge

**Complexity:**
--

O(mn) and O(n^2 +mlogn)

**IMPLEMENTATION:**
--

Kind of like dijkstra, u need to update adjacent vertices (we won't need to care about things becoming invalid here since we will get min edge in the beginning and then the endpoints will get included in seleted vertices so after this they will become invalid anyways)
