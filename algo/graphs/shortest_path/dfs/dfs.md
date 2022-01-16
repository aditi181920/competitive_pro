**DEPTH FIRST SEARCH:**
--

-> directed/undirected unweighted graph (or weighted graph having same weights)\
-> mostly used for finding reachability or when our goal is to reach all the nodes in graph through adjacent nodes\
-> searches in a depth first manner that is keeps goind deeper(next level) until can't go any further and then recurses back to again go deep from some other path

**COMPLEXITY:**
---
**O(V+E)**

**IMPLEMENTATION:**
---

```cpp
void dfs(map<int,list<int>> adj,map<int,bool> visited,int node){
    visited[node]=true;
    for(auto i:adj[node]){
        if(!visited[node]){
            cout<<i<<" ";
            dfs(adj,visited,i);
        }
    }
}
```
