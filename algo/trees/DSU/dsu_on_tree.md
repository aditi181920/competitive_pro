**DSU ON TREE:**
--

-> This technique incorporates the idea of small to large technique of dsu on trees (thereby the name given )\
-> Let's consider the problem that in a tree compute some cnt of things in subtree of v and answer q queries \
-> The technique for this is for a given vertex v when we compute the answer for its subtrees we don;t remember the answer for small subtrees.. we only remember the asnwer for the last (compute this in end to avoid mixing up info of subtree)\
-> Then we just combine the compute answer for other smaller subtrees with the biggest and we have our answer \

--> Time complexity :O(nlogn) \
-> Why such a nice time complexity ?\
-> Because every node can have max logn light edges connecting it to the root ... this implies every node is visited atmost logn times only=> so the complexity comes out to be O(nlogn)




```cpp

int cnt[maxn];
void dfs(int v, int p, bool keep){
    int mx = -1, bigChild = -1;
    for(auto u : g[v])
       if(u != p && sz[u] > mx)
          mx = sz[u], bigChild = u;
    for(auto u : g[v])
        if(u != p && u != bigChild)
            dfs(u, v, 0);  // run a dfs on small childs and clear them from cnt
    if(bigChild != -1)
        dfs(bigChild, v, 1);  // bigChild marked as big and not cleared from cnt
    for(auto u : g[v])
	if(u != p && u != bigChild)
	    for(int p = st[u]; p < ft[u]; p++)
		cnt[ col[ ver[p] ] ]++;
    cnt[ col[v] ]++;
    //now cnt[c] is the number of vertices in subtree of vertex v that has color c. You can answer the queries easily.
    if(keep == 0)
        for(int p = st[v]; p < ft[v]; p++)
	    cnt[ col[ ver[p] ] ]--;
}


```

Note: HLDA uses the same concept of light and heavy weight edges. The difference i
