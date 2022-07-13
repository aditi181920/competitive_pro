
**Ford Fulkerson method:**
--

-> Residual graph: The same graph with opposite edges added which undo the flow, for ex: if forward edge stores +f (capacity of flow taken) then -f for reverse edge, else if we store capacity remaining in the forward edge then we store capacity consume in the reverse edge\
-> Augmenting path: Any path such that min flow that can be directed is >0\
-> Ford fulkerson just says to maintain a residual graph and find argumenting path and keep directing flow until you can \
-> Complexity: O(EF)(since each path increases the capacity by atmost 1) -> this can turn out to be very bad


-> **Flow value lemma:** If f is any flow and (A,B) is any cut. val(f)=$\sum_{e out of A}$ f(e)-$\sum_{e out of A}$ f(e)\
-> **Weak duality theorem:** If f is any flow and (A,B) is any cut. val(f) <=cap(A,B) \
val(f)=$\sum_{e out of A}$ f(e)-$\sum_{e out of A}$ f(e)\
      <= $\sum_{e out of A}$ f(e)\
      <= $\sum_{e out of A}$ c(e)\
      =cap(A,B)\
->**Max flow-min cut theorem:** Max flow f= Capacity of min cut 

-> Flow methods greatly depend on the way of choosing augmenting paths\
-> Good augmenting path:
1. Max bottleneck capacity
2. Sufficiently large bottleneck capacity
3. Fewest edge
