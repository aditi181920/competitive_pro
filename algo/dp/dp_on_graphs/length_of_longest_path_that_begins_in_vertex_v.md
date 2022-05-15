**LENGTH OF LONGEST PATH THAT BEGINS IN VERTEX V:**
--

Given a directed (or maybe undirected) we need to find the length of the longest path that begins in vertex v

**DP:**

-> Sort the array topologically \
-> now the nodes are arranged in the order they are encountered \
-> we can do dp on this\
-> initialize the last nodes by value 1\
-> now we can traverse the topological sorted array in reverse direction and do for every vertex v:\
  dp[v]=max(dp[v],dp[vn]+1)
  
  
 **PROBLEM LINKS:**
 --
 
 [CF 791 DIV 2](https://codeforces.com/contest/1679/problem/D)
