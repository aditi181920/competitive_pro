**GAMES:**
--

-> Game played by 2 players on an arbitrary graph G.\
-> current state of game is arbitrary vertex\
-> move by turns-> move from current vertex to an adjacent vertex using an edge\
-> unable to move then lose or win\
-> if directed graph with cycles. Determine given an initial state, who will win the game if both players play optimally or tell if draw.

**DESCRIPTION OF ALGO:**
--

-> Winnning vertex: if player starting at this state will win the game if they play optimally (regardless of what other player does)\
-> Losing vertex: player starting here loses, if opponent plays optimally\
-> Vertices that don't have any outgoing edges -> we already know their whether they are winning or losing\
-> Rules:
1. If vertex-> losing vertex then vertex is a winning vertex
2. If all vertex-> winning vertex then vertex is a losing vertex 
3. The vertices that don;t fit this category are draw

We can now check in O(mn) for all vertices as starting vertex.

But we can smartly reduce this complexity down to O(m) using the rules defined above:
1. Start from some losing edge -> we know any edge before this is an winning edge \
2. If we encouter some node from winning node-> check whether the encountered nodes all adjacencies are winning vertex (can be checked in O(1) using some counters) ) then this is loosing
3. If some vertices state cannot be defined (useless to do dfs there so we don't proceed further on such nodes)
