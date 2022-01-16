**BREADTH FIRST SEARCH:**
---

-> gives the shortest path from the source node\
-> applicable only on unweighted graphs (or weighted with same weight)\
-> applicable on both undirected and directed graph(without any cycle)\
-> searches in a breadth first manner that is first searches for all nodes at level k(nodes having paths from source not less than k) before moving to level k+1\
-> somewhat like dijkstra, bfs just can't have weights \
-> can again use predecessor array to get the shortest path

**COMPLEXITY:**
---
**O(V+E)**


**IMPLEMENTATION:**
---

-> Considering adjacency list has been created and visited list has been set to false initially and an empty queue is created
```cpp

    q.push(s);
    visited[s]=true;
    while(!q.empty()){
        char v=q.front();
        cout<<v<<",";
        q.pop();
        for(auto x:adj[v]){
            if(!visited[x]){
                q.push(x);
                visited[x]=true;
            }
        }
    }
 ```
 
 **APPLICATIONS:**
 ---
 
-> finding all the vertices reachable from a given vertex, \
-> finding if an undirected graph is connected, \
-> finding (in an unweighted graph) the shortest path from a given vertex to all other vertices,\
-> determining if a graph is bipartite,\
-> bounding the diameter of an undirected graph,\
-> partitioning graphs, \
-> and as a subroutine for finding the maximum flow in a flow network (using Ford-Fulkerson’s algorithm)
