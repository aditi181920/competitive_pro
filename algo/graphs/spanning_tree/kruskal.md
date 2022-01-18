**KRUSKAL'S ALGORITHM:**
---

-> used for finding min spanning tree (spanning tree with min weighted sum)

**ALGO:**
---

-> Sort the edges by their weights in non-decreasing order\
-> Now start processing edges from smallest weight\
-> If the edges don't belong to the same componenet then add that edge to our min spanning tree and combine the edge nodes to same component\

**COMPLEXITY ANALYSIS:**
---

-> Sorting : O(ElogE)\
-> Creating initial empty compo : O(V)\
-> Iterating over edges and combining : O(ElogV)\
-> Overall Complexity : O(ElogE + ElogV) \
-> Since in sparse graph |E|==|V| and in dense graph |E|==|V^2|\
-> FINAL COMPLEXITY :  **O(ElogE)**\
-> Note for dense graph Prim's algorithm performs much better

**IMPLEMENTATION:**
---

-> Efficient implementation of this algorithm can be done with the help of DSU\
-> We just need to sort then check check parents for checking components and union for combining them


**PROBLEM LINKS:**
---

[ABC 235 E](https://atcoder.jp/contests/abc235/tasks/abc235_e)
