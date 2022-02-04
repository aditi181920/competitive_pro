**LOWEST COMMON ANCESTOR:**
---

Given a tree G.
For any two vertices v1,v2 the LCA of these is a vertex v that lies on the path from the root to v1 and the path from the root to v2, and the vertex should be the lowest.\
It is obvious that their lowest common ancestor lies on the shortest path from v1 to v2. \
Also if v1 is the ancestor of v2, v1 is their lowest common ancestor and vice-versa.

**IDEA OF ALGO:**
---

-> Euler tour of the tree: Make a DFS traversal starting at the root and build a list euler which stores the order of the vertices that we visit (a vertex is added to the list when we first visit it, and after the return of the DFS traversals to its children)\
-> first[0...n-1] = for each vertex i its first occurrence in euler tour\
-> height[0...n-1] = height of each node (distance from root to it) \
-> if we clearly look at the mechanism of vertex occuring in the given euler tour then we can easily see that LCA will be node with least height in euler tour between first(v1) and first(v2)\
-> we can find the node with min height in:\
---> O(sqrt(n)) with preprocessing in O(n) time using sqrt decomposition\
---> O(log n) with preprocessing in O(n) time using seg tree\
---> O(1) with O(nlogn) build time using sparse table\
