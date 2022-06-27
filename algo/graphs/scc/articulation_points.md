**ARTICULATION POINTS:**
--

Like bridges refer to cut edges, llly articulation points refer to cut vertices.\

**Idea:**
--

-> Idea is a lot similar to bridge finding. Here the only difference is the end points. If (v,to) if none of to or descendant of to has any back edge to ancestor of v then v is an articulation point.\

**ALGORITHM:**
--

-> Run a dfs\
-> tin[v] be the entry time of node v\
-> low[v]= min(tin[v],low[p](p is node connected through back edge),low[to](to is adj to v))\
-> If any low[to]<=tin[v] => there is a back edge\
-> Articulation point will have low[to]>=tin[v] always 
