**FLOWS:**
--
-> Given a digraph with source and sink and capacity for every edge \
-> We have to find maximum flow that can reach from source to sink\
-> Some rules are \
--> f(u,v) <=c(u,v)\
--> $\sum$ f(in)= $\sum$ f(out)
-> An st cut is a partition(A,B) into 2 sets such that s belongs to one and t belongs to other\
-> Capacity(A,B) = $\sum$ capacity of edges from A to B\
-> Min cut- Cut of min capacity

**Why greedy algorithm fails in flows:**
--

-> Because of we choose a bad path\
-> Then there is no going back\
-> This choice of bad path will lead to non optimal solution in the end

