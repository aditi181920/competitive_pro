**REROOTING:**
--

This technique is generally used when we calculate some dp on a given tree. Then we are required to change the root and our dp value also changes according to the change in the root.\
Using re-rooting technique we can use the dp values of a node x and calculate for nodes y adjacent to x if they were made the roots

**Steps:**
--

1. Calculate dp values using the initial root
2. Now do dfs from that root
3. For each adjacent node we reroot the tree
4. Can the dp values of the parent as if current node was not its child
5. Calculate dp values of the child as if parent was one of its child
6. We have successfully rerooted our tree 
7. Note that when we come back to this node after dfs we also need to roll back the changes that we made earlier 



**PROBLEM LINKS:**
--

[ABC 160 F](https://atcoder.jp/contests/abc160/tasks/abc160_f?lang=en)
