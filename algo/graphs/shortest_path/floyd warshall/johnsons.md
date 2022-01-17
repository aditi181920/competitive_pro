**JOHNSON'S ALGORITHM:**
---
-> apsp\
-> In the beginning let's assume there are no negative cycles in the graph\
-> If the graph is sparse (|E|<<Emax)[edges actually present very less than edges than can be present at max] then this algo works more efficiently than Floyd-Warshall

**1. STEPS:**
---
-> 1. Compute a potential p for the graph G\
-> 2. Create a new weighting w of the graph where w(u->v)=w(u->v)+p(u)-p(v)\
-> 3. Compute all pairs shortest path dist with the new weighting\
-> 4. Convert the distances back to the original problem, with the eq dist(u->v) = dist(u->v) - p(u) + p(v)\

**STEP 3:**
--
-> Since the weights are now are non negative so we can use Dijkstra's algorithm to get correct distances\
-> We run Dijkstra's algo for every vertex u to get distance d[u][j] j=[1..n] \
-> Single run of Dijkstra takes O(mlogn)\
**COMPLEXITY:** O(nmlogn)  [Again this can be improved if u use Fibonacci heaps]

**STEP 1:**
--
-> The shortest path values themselves satisfy the requirement of a potential!
-> Proof:
```sh
Fix some vertex s:
  Assign p(v) = dist(s->v) for all vertices v

Assume that p is not a potential
Then by definition of potentials there is some edge u->v s.t. w(u->v)+p(u)-p(v)<0
=>   w(u-v) + dist(s->u)-dist(s->v)<0
=>   w(u-v) + dist(s->u) < dist(s-v) 
this is a contradiction 
as this implies that dist(s-v) is not the shortest path anymore since we can reach v from u in less cost
==> p is a potential

But careful this proof is only correct if chosen vertex s can reach all vertices v
Otherwise we would have infinite potentials which is not allowed by the definition.
```
-> So now if we have some unreachable vertices how to find potential!!\
-> It turns out that we can create a new vertex s' and create edge s->v with weight 0 for every vertex v [since no incoming edges added no chance of creation of negative cycle]\
-> And now we can define potential based on shortest distance from s'\
-> since we have taken weight 0 of all newly create edges it won't mess up with our original graph values\
-> the property of potential is still valid if we delete some vertices and edges, so it not a problem to remove s' after we compute the potential\
-> So we can just run Bellman-Ford once on the graph with the new vertex s to find shortest distance which will give potential\
**COMPLEXITY:** O(mn)

-> Step 3 is the bottleneck and overall complexity of Johnson's algorithm


**OVERALL COMPLEXITY:** O(nmlogn) [O(n^2 logn+nm) if using Fibonacci heap]
