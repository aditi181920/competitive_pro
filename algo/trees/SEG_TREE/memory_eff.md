**MEMORY EFFICIENT IMPLEMENTATION:**
--

-> Segment tree only has 2n-1 useful nodes out of 4*n nodes that are allocated to it.. this is because when we do standard implementation of segment tree then if n is not a power of 2 then last levels are not completely occupied\
-> Why 2n-1? last level having n nodes (then in a full binary tree we will have internal nodes n-1)\


-> Notice that standard implementation is bfs order implementation (level wise)\
-> What we can do is do a dfs order/euler order implementation which will consume 2\*n-1 nodes only\
-> So like if current node is v then let's say it covers segment [l,r]\
-> 2\*v must cover [l,mid] and 2*v+1 must cover [mid+1,r]\
-> left child has (l-mid+1)*2-1 nodes \
-> therefore if v+1 is left child then right child must be v+(l-mid+1)*2 \
-> this way we can contruct a memory efficient segment tree
