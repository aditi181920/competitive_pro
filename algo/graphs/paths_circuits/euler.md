**EULER CIRCUIT:**
---

**ALGORITHMS TO SOLVE EULER PATH/CIRCUIT:**
--

1.**FLEURY'S ALGORITHM:**
--

--> Make sure that graph has either 0 or 2 odd vertices\
--> If there are 0 odd vertices, start anywhere. If there are 2 odd vertices, start at one of them\
--> Follow edges one at a time. If you have a choice between a bridge and a non-bridge, always choose the non-bridge  \
--> This is quite an inefficient solution though (as finding bridges takes up extra time increasing time complexity)\
--> This algorithm always work becoz it won't terminate on small eulerian graphs present inside ever as if it does then that node will get disconnected from rest of the graph hence making that edge as bridge so that edge won't be deleted at all.\
--> Naive approach of finding bridges is running dfs from the latest reach node and see if all other graph components are connected\
--> There is a linear algorithm for this though [Tarjan's bridge-finding algo](https://www.wikiwand.com/en/Bridge_(graph_theory))

2.**HIERHOLZER'S ALGORITHM:**
--

--> Choose any starting vertex v, and push it onto a stack. Initially all edges are unmarked.\
--> While the stack is non-empty, look at the top vertex, u, on the stack. If u has an unmarked incident edge, say, to a vertex w, then push w onto the stack and mark the edge uw. If u has no unmarked incident edge, then pop u off the stack and print it.\
--> When the stack is empty, u will have printed a sequence of vertices that corresponds to an Eulerian circuit\
--> The time complexity comes out to be O(M)\
--> Can find euler path by : adding an edge (v1,v2) such that v1 and v2 have odd number of edges then we can apply this algo and in the edge remove (v1,v2) to get required path




**PROBLEM LINK:**
--

[CF 770 DIV2](https://codeforces.com/contest/1634/problem/E)
