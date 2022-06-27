**BRIDGES:**
--

This is a edge which if removed increases the number of connected components in the graph

**Idea:**
--

An edge (v,to) is a bridge if none of the descendants of to and to itself has back edge going to v or any ancestor of v 


**Algorithm:**
--

-> Run a dfs\
-> tin[v] be the entry time of node v\
-> low[v]= min(tin[v],low[p](p is node connected through back edge),low[to](to is adj to v))\
-> If any low[to]<=tin[v] => there is a back edge\
-> Bridges will have low[to]>tin[v] always 

**Terminologies:**
--
-> **k edge connected component:** These are connected components which still remain connected if u remove less than k edges \
-> **online Bridge finding:** U are allowed to add edges to the graph and everytime while adding it u return the bridges in the new graph\


**Online cycle finding algorithm:**
--

-> This consists of some case work steps and includes concepts like DSU, LCA, etc. \
**Details can be found at cp algo.com
